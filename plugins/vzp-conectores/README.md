# vzp-conectores

Conectores MCP remotos da VZP. Instalar este plugin dá, dentro do Claude, as
ferramentas das plataformas do escritório — sem ninguém precisar instalar código
ou guardar a credencial da plataforma. A credencial de cada sistema fica só no
servidor (Render); você só precisa do **token compartilhado da equipe**.

## Conectores incluídos

| Conector | Estado | Ferramentas |
| -------- | ------ | ----------- |
| **Vobi** | ativo | obras, fornecedores, clientes, orçamento, ordens de compra, solicitações, contas a pagar, parcelas, RDO; criar solicitação e OC |
| Sienge   | em breve | empreendimentos, medições, contas a pagar/receber, NF-e (cobre Construpoint e Prevision) |
| WhatsApp | em breve | enviar mensagem/documento pelo número da VZP |

## Como ativar (uma vez, por pessoa)

O plugin lê o token do ambiente, na variável **`VZP_MCP_TOKEN`**. Peça o token ao
Vitor (é o `MCP_TOKEN` gerado no Render) e configure:

**Windows (PowerShell):**
```powershell
setx VZP_MCP_TOKEN "cole-o-token-aqui"
```
(feche e reabra o terminal / o Claude depois de rodar)

**macOS / Linux:**
```bash
echo 'export VZP_MCP_TOKEN="cole-o-token-aqui"' >> ~/.zshrc && source ~/.zshrc
```

Depois disso, o conector Vobi aparece nas ferramentas do Claude. Para testar, peça:
*"lista minhas obras na Vobi"*.

## Segurança

- O token é compartilhado pela equipe: trate como senha, não cole em lugar público.
- Com ele, qualquer pessoa pode **criar OC/solicitação na Vobi** (mexe em dinheiro).
- Se vazar, o Vitor gera outro no Render e redistribui.

## Observação para claude.ai / Claude Desktop

Plugins de marketplace são um recurso do **Claude Code**. Quem usa o conector pelo
**claude.ai** ou **Claude Desktop** adiciona como *Custom Connector* pela URL
`https://vzp-mcp-vobi.onrender.com/mcp` com o header
`Authorization: Bearer <token>` nas configurações de conectores.
