<h1 align="center">Escopo do MVP</h1>

<p align="center">
  <a href="mvp-scope.md">🇺🇸 English</a> | 🇧🇷 Português
</p>

## 1. Objetivo

Facilitar a ida ao mercado: o usuário registra o que quer comprar e o que já tem em casa, define por quanto tempo cada produto dura, e o app avisa e coloca o produto na lista. O MVP é para **uma pessoa usando sozinha**.

## 2. Ciclo principal

1. **Lista de compras.** O estoque começa zerado. O usuário adiciona à lista o que quer comprar.
2. **Finalizar a compra.** Ele marca os itens e finaliza a lista. Os itens marcados entram no estoque como lotes (BR-11).
3. **Gerenciar o estoque.** Ele também pode adicionar manualmente itens que já estavam em casa (BR-12). No MVP não há consumo diário: para cada produto, o usuário define um **prazo em dias** (por exemplo, 60), que vale para cada nova compra. Exemplo: uma caixa com 12 leites dura 2 meses, então o prazo é 60 dias. Durante o prazo, o lote fica "parado" no estoque, com a quantidade inteira. No fim do prazo de cada lote, o estoque dele vai a zero.
4. **Receber os alertas.** O alerta de reposição vem do **fim do último lote** do produto, isto é, de quando não sobra nenhum lote. Se existe outro lote, o fim do primeiro não gera alerta. Perto desse dia, o app envia o primeiro alerta (padrão: 2 dias antes, editável pelo usuário) e o segundo (sempre 1 dia antes), e coloca o produto na lista de próximas compras (BR-03, BR-04 e BR-09). No dia, há só um aviso.
5. **Repetir.** O usuário marca os itens na lista, finaliza, e o ciclo recomeça.
6. **Ver o estoque no calendário.** Em visões semanal e mensal, cada lote é uma barra, do dia da compra até o fim do prazo. Os lotes do mesmo produto ficam um embaixo do outro. A quantidade do produto em um dia é a soma dos lotes ativos nesse dia.

**Exemplo da visão semanal:** o lote 1 de leite acaba na quarta; o lote 2, comprado na segunda, dura 60 dias. Aparecem duas barras, uma embaixo da outra: a primeira termina na quarta e a segunda segue por muito mais tempo. Até quarta, a quantidade de leite é a soma dos dois lotes; depois, só a do lote 2. O alerta de reposição só sai perto do fim do lote 2.

O ciclo existe para facilitar a compra e "agendar" a próxima, para que a ida ao mercado seja tranquila e sem pressa.

## 3. O que entra no MVP

| Regra | No MVP | Observação |
|---|---|---|
| BR-03 | Parcial | Só reposição (alertas e aviso), com o alerta vindo do fim do último lote. Sem vencimento. |
| BR-04 | Parcial | O primeiro alerta é editável (padrão: 2 dias antes) e o segundo é sempre 1 dia antes. Sem terceiro alerta. Valem as regras de alertas no mesmo dia e de data já passada. |
| BR-07 | Parcial | Só a forma "dura N dias" (o prazo). Sem consumo diário e sem agendamento. |
| BR-08 | Parcial | Só unidades e embalagem (por exemplo, caixa com 12). Sem peso e volume. |
| BR-09 | Sim | Lista de próximas compras: o produto entra no primeiro alerta, e há um aviso no dia. |
| BR-11 | Parcial | Finalizar a lista cria o estoque. No MVP, cada lote recebe o prazo do produto (no lugar da validade padrão). Sem validação de adolescente. |
| BR-12 | Sim | Entrada manual no estoque do que já estava em casa. |

## 4. Fica para depois

| Regra | O que é |
|---|---|
| BR-01 | Estoque diminuindo todo dia pelo consumo |
| BR-02 | Lote vencido |
| BR-05 | Validade padrão e data de vencimento |
| BR-06 | Ordem de consumo entre lotes |
| BR-07 | Consumo diário e agendamento de consumo |
| BR-10 | Família, perfis e validação |
| Outros | Data fixa do alerta (junto com o consumo), segundo e terceiro alertas configuráveis, alertas de vencimento, peso e volume, uso offline, foto com IA |

Como o MVP evolui: o prazo que o usuário informa hoje passa a ser calculado pelo consumo (BR-01 e BR-07) nas próximas versões, sem mudar o resto do ciclo. Nas regras completas, o alerta já vem da data de esgotamento do produto (quando não sobra estoque), o que é o mesmo que o fim do último lote.

Mesmo com um usuário só, o banco já terá o espaço de trabalho, para que a BR-10 entre depois sem refazer as tabelas.
