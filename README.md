# VITORIA SPOT

Site estático pronto para publicação no GitHub Pages.

## Como usar

- Abra `index.html` para acessar a tela inicial.
- A página inicial direciona para `original/index.html` e `dashboard/index.html`.
- O projeto usa HTML, CSS e JavaScript; não há código Java neste pacote.

## Publicar no GitHub Pages

1. Extraia este ZIP.
2. Envie o conteúdo da pasta `vitoria-spot-site` para um repositório.
3. Nas configurações do repositório, ative o GitHub Pages usando a branch principal e a pasta raiz.

## Situação: dropdown e integração com o dashboard

A lista suspensa da planilha é gerada a partir das mesmas 13 opções coloridas do dashboard. O importador reconhece o cabeçalho `Situação` e também `Situação (lista clicável)`. Depois de editar a planilha no Excel/OneDrive, importe o arquivo no dashboard por **Anexar planilha de retorno** e confirme com **OK**; não há sincronização automática do OneDrive para o dashboard.
