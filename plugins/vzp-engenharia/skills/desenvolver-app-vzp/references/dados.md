# Dado: Postgres sem susto

## Pool com ouvinte de erro

Todo `new pg.Pool(...)` precisa de `pool.on('error', ...)`. Quando o banco
derruba uma conexão **parada no pool**, o `pg` emite `error` no Pool; evento
`error` sem ouvinte no Node vira exceção não tratada e **mata o processo**.

Não aparece em teste. Só em produção, e como queda inteira do app — não como
erro de uma requisição.

Os três de uma vez, ao abrir um pool novo:

```js
const pool = new pg.Pool({
  connectionString: process.env.DATABASE_URL,
  idleTimeoutMillis: 30_000,
  connectionTimeoutMillis: 10_000,
});
pool.on('error', (e) => console.error('pool:', e.message));
```

E repique **só** para falha de rede (`08006`, `EAUTHTIMEOUT`, `ECONNRESET`…):
nesses casos a consulta nunca chegou a rodar, então repetir é seguro. Erro de
SQL não se repete. Sem o repique, a primeira conexão fria para o pooler do
Supabase estoura no handshake e um clique certo vira 500.

## Hora: o erro de 4 horas que ninguém vê

`<input type="datetime-local">` manda `2026-10-02T09:30` — **sem fuso**. Jogado
num `timestamptz`, o Postgres interpreta no fuso do **servidor**. No Cloud Run
isso é UTC: a consulta das 09:30 é gravada como 09:30Z e exibida como 05:30 em
Cuiabá.

Ler a hora sem fuso no fuso da **pessoa**:

```sql
CASE WHEN $1 ~ '(Z|[+-][0-9]{2}:?[0-9]{2})$' THEN $1::timestamptz
     ELSE $1::timestamp AT TIME ZONE (SELECT fuso FROM pessoa WHERE id = $2) END
```

O `CASE` não é enfeite: string que já vem com offset (de API, de importação)
convertida de novo erra na outra direção.

Vale para **toda** coluna `timestamptz` alimentada por campo de tela. Coluna
`date` não — dia de calendário não se converte, e `CURRENT_DATE` é o dia do
servidor, não o de quem usa.

## Migração

Migração roda mais de uma vez — por engano, por redeploy, por dois processos
subindo juntos. Escrever para aguentar: `create table if not exists`,
`add column if not exists`, `on conflict do nothing`. O que não aguentar rodar
duas vezes precisa dizer isso em voz alta no cabeçalho.
