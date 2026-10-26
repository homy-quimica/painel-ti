# painel-ti

Painel de licenças e custos da TI da Homy Química.

**Nenhum dado de colaborador está neste repositório.** O arquivo `index.html` é só código.
Os nomes, as licenças e os valores da Azure são buscados no momento em que a pessoa abre a
página, com a conta dela, e somem quando a aba fecha.

## Como funciona

1. A pessoa entra com a conta da Homy (MSAL, janela da Microsoft).
2. A página pede dois tokens em nome dela:
   - **Microsoft Graph** para ler `subscribedSkus` (licenças) e `users` (quem tem cada uma)
   - **Azure Resource Manager** para ler o consumo em Cost Management
3. Desenha a tela. Não há servidor, não há banco, não há agendamento.

Quem não tiver permissão de leitura não enxerga nada, mesmo abrindo o endereço. É essa a
proteção, e é por isso que o repositório pode ser público sem expor ninguém.

## Registo de aplicação no Entra

| | |
|---|---|
| Nome | Painel de TI - licencas e custos |
| Client ID | `cd4e6552-0c9d-4586-bdd3-6f23341a3cc2` |
| Tipo | SPA |
| Redirect URI | `https://homy-quimica.github.io/painel-ti/` |

Permissões delegadas:

- `User.Read` (consentimento do próprio utilizador)
- `Directory.Read.All` (**exige consentimento de administrador global**)
- `https://management.azure.com/user_impersonation` (consentimento do próprio utilizador)

A página lê apenas. Não grava nada no Microsoft 365 nem na Azure.

## Preços das licenças

Não existe API pública com o preço que a Homy paga. Os valores em `PRECO`, dentro do
`index.html`, vêm das faturas da Microsoft, já com imposto, e precisam ser conferidos quando
um contrato mudar:

| Licença | Por assento |
|---|---|
| Microsoft 365 Business Standard | R$ 83,50 |
| Microsoft 365 Business Basic | R$ 48,10 |
| Business Standard + Copilot | R$ 183,86 |
| Power BI Pro | R$ 93,50 |
| Power Automate Premium | R$ 117,34 |

## O que a página não consegue mostrar

O **último acesso** de cada conta, que é o que diria quem de fato saiu da empresa. Esse dado
exige a licença **Entra ID P1**, que a Homy não assina: a API responde
`Tenant is not a B2C tenant and doesn't have premium license`.

## Publicação

GitHub Pages, a partir da branch `main`, na raiz.

> O plano Free da organização só publica Pages de repositório público. Como o arquivo não
> contém dado nenhum, isso é aceitável. Se a organização um dia for para o plano Team, o
> repositório pode ser fechado sem derrubar a página.
