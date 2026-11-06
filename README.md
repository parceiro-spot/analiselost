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

## REPORT LOST: reconhecimento de XPT

A planilha REPORT LOST (`report_lost_on_route_*.csv`) é a única necessária para Pacotes em Rota / LOST. Ela não tem coluna "XPT": a base XPT vem em **Centro de destino** (códigos iniciados por `E`, ex.: EMG40, ERJ2). Regra aplicada na importação:

- Centro de destino com código `E...` → o pacote entra na **base XPT** (tipo XPT); o SVC de origem continua no campo Origem (ex.: SMG3 → EMG40: "EMG40 XPT de SMG3").
- Destino vazio, `BRN...` ou `BRD...` → o pacote fica na **base SVC** de origem.
- Bahia e São Paulo não têm XPT e ficam sempre em SVC.
- Dados já salvos no navegador antes desta regra são corrigidos automaticamente ao abrir o dash.

A tabela SVC ↔ XPT usada nos rótulos ("SVC de ...") vem da planilha BSC Delivery Success (`SVC_TO_XPT` no `script.js`). Se surgir um XPT novo, basta incluir a linha nessa tabela.

A coluna **Produto** não existe no REPORT LOST; ela só é preenchida quando o mesmo pacote já foi importado em outra planilha que traga o item (SHP_ITEM_DESC).


## Planilhas necessárias
- **REPORT LOST** (`report_lost_on_route_*.csv`): obrigatório e suficiente para o Análise Lost/Pacotes em rota.
- **REPORT DRIVER** (`report_driver_*.xlsx`): opcional; serve apenas para trocar o ID do transportador pelo nome do motorista. O arquivo enviado contém somente a lista de IDs, então não acrescenta nomes.
- **Planilha de retorno**: opcional; só é necessária para registrar situação, justificativa ou foto.

## Distribuição SVC/XPT
No REPORT LOST, se `Centro de destino` começar com `E` (por exemplo `EMG40`, `ERJ2`, `EES8`), o pacote é contado na base de destino como **XPT**. Se o destino estiver vazio ou for `BRN/BRD`, o pacote permanece na base `Centro de origem` como **SVC**.
