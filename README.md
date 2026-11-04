# VITORIA SPOT

Site estático pronto para publicação no GitHub Pages.

## Estrutura

- `index.html`: estrutura da página (HTML).
- `style.css`: todos os estilos (CSS).
- `script.js`: toda a lógica do dashboard (JavaScript).

Os três arquivos precisam ficar na mesma pasta.

## Como usar

- Abra `index.html` para acessar a tela inicial.
- A página inicial direciona para `original/index.html` e `dashboard/index.html`.
- O projeto usa HTML, CSS e JavaScript; não há código Java neste pacote.

## Publicar no GitHub Pages

1. Extraia este ZIP.
2. Envie o conteúdo da pasta `vitoria-spot-site` para um repositório.
3. Nas configurações do repositório, ative o GitHub Pages usando a branch principal e a pasta raiz.

## Situação: dropdown e integração com o dashboard

A lista suspensa da planilha é gerada a partir das mesmas 13 opções coloridas do dashboard. O importador reconhece cabeçalhos iniciados por `Situação`, `Situation`, `Status` ou `Fila` (por exemplo, `Situação (lista clicável)` e `Fila atual`). Se houver mais de uma dessas colunas, prioriza `Situação`/`Status` em vez de `Fila`. Depois de editar a planilha no Excel/OneDrive, importe o arquivo no dashboard por **Anexar planilha de retorno** e confirme com **OK**; não há sincronização automática do OneDrive para o dashboard.

## Aba Análise Base (corrigida)

A aba estava em branco porque o `index.html` não tinha a lógica nem o CSS dessa aba (ela existia só no `script.js`, que a página não carrega). Agora a lógica está no `script.js` e o CSS no `style.css`: filtro por regional e base, calendário De/Até, atalhos de 3/6/12 meses, resumo por mês e, ao clicar no mês, o valor de cada dia. Os dados vêm das planilhas já importadas (arquivos antigos salvos no navegador).

## Regra de Valor Revertido

A configuração oficial do prazo fica no JavaScript do dashboard (`script.js`): na aba **Valor Revertido**, o valor é calculado pacote a pacote: pacote que desaparece até 48 horas entra como **Valor revertido**; pacote que continua presente após 48 horas entra como **Valor não revertido/ofensor**. O **Valor atual** mostra o total real atual. A aba **Pacote Revertido** usa a mesma regra própria de 48 horas.

## Pacotes em Rota também no LOST

Ao anexar uma planilha de **Pacotes em Rota** no painel LOST, ela continua salva e visível na aba **Pacotes em Rota**. Se ainda não existir uma planilha LOST para aquele dia, o dashboard cria automaticamente uma importação provisória com os mesmos pacotes para que ela apareça em **LOST > Todos**. Quando a planilha LOST real for anexada depois, ela substitui a importação provisória do dia. Arquivos cujo nome contém um intervalo de datas, como `2026-10-01_2026-10-31`, não alteram indevidamente o dia do arquivo: nesse caso, o dia selecionado no formulário (ou o dia atual) é usado.

Os campos de planilha de Pacotes em Rota e de LOST/Risco LM aceitam vários arquivos de uma só vez. Cada arquivo é lido e salvo separadamente, respeitando o dia e o turno identificados no nome ou informados no formulário.

No DASH LOST, o primeiro cartão em **Importados** é **LOST · 1) Pacotes perdidos** e reconhece automaticamente tanto o formato LOST/Risco LM quanto o formato Pacotes em Rota. Assim, quando o LOST do dia ainda não estiver disponível, basta anexar a planilha de Pacotes em Rota nesse mesmo cartão.

## Valor Revertido: Ofensores da manhã

O antigo bloco "Selecionar bases / Escolha as regionais" foi removido. No lugar, a aba **Valor Revertido** tem **Ofensores da manhã**:

1. De manhã, com a planilha da manhã aberta, digite o valor (ex.: 10.000) e clique **Classificar como ofensores**. As bases com valor igual ou acima ficam guardadas para aquele dia.
2. À tarde, não digite nada: clique em **Puxar ofensores da manhã (valor atual)**. A tela mostra essas bases com o valor atual de cada uma. Clique de novo (**Voltar para todas as bases**) para sair do filtro.
3. **Limpar lista** apaga a lista do dia. A câmera captura só o nome das bases guardadas.

O bloco permanece na tela **Valor Revertido** do DASH LOST. Ao classificar, o sistema usa a planilha da data selecionada; se essa data não estiver disponível, usa a planilha ativa ou a importação mais recente, evitando o erro de “Não há planilha importada nesta data”.

## Meta semanal (igual em Regional e Base e em Valor Revertido)

As duas abas calculam a meta sobre o valor da **primeira planilha da semana** (segunda-feira) ou, se a meta foi ativada no meio da semana, da primeira planilha a partir do dia da ativação. Na coluna **Meta da semana** do Valor Revertido aparecem: valor no início da semana, meta (quanto reduzir), quanto já reduziu e quanto falta. Pacotes que entraram há menos de 24h não contam na meta.
