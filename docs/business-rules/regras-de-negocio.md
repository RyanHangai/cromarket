<h1 align="center">Regras de negócio </h1>

<p align="center">
    <a href="../business-rules/business-rules.md">🇺🇸 English</a>
</p>

## 1. Objetivo

Muita gente ainda monta a lista de compras à mão, no papel, e só percebe que algo acabou ou venceu quando já é tarde. O CroMarket registra o que a casa compra, calcula quando cada produto vai acabar ou vencer e avisa com antecedência, para que toda a família organize a ida ao mercado.

## 2. Glossário

| Termo | Definição | Exemplo |
|---|---|---|
| **Espaço de trabalho** (workspace) | Espaço de uma casa/família, compartilhado por seus membros. Estoque, consumo, validades, fuso horário e lista de compras pertencem a ele. Qualquer alteração vale para o espaço inteiro e todos os membros a veem. | A família Silva usa um único espaço. |
| **Membro** | Pessoa que participa de um espaço de trabalho. Tem um perfil. | Ana, João e Pedro. |
| **Perfil** | Define o que o membro pode fazer: **adulto** edita tudo; **adolescente** edita, mas a mudança só vale depois da validação de um adulto; **criança** só visualiza. | Ana é adulta; João é adolescente. |
| **Responsável** | Adulto que gerencia o espaço: o criador e, se ele quiser, mais um adulto designado por ele. Acompanha, na aba de notificações, tudo o que acontece no espaço. | Ana (criadora) é responsável. |
| **Produto** | Tipo de coisa que se compra e acompanha. | Leite. |
| **Item** | Uma unidade de um produto, na medida em que ele é contado (unidade, kg ou litro). | 1 caixinha de leite. |
| **Embalagem** | Forma em que o produto é comprado, com a quantidade de itens que ela traz. Cada produto tem uma embalagem padrão, editável. | Caixa com 12 leites (padrão); caixa com 6 (outra marca). |
| **Lote** | Conjunto de itens de um mesmo produto comprados juntos. Tem data de compra, marca, data de vencimento e estoque próprios. | A caixa de leite comprada em 12/10. |
| **Estoque** | Quantidade de itens de um lote (ou de um produto) que ainda existe em casa. | O lote de 12/10 está com 5 caixinhas. |
| **Consumo** | Quanto do produto o espaço de trabalho usa por dia. Pode ser informado direto ou como "dura N dias". Aceita decimais em qualquer medida. | 130 g de shampoo por dia. |
| **Disponibilidade** | Por quantos dias o estoque dura: estoque ÷ consumo por dia. | 6 leites ÷ 1 por dia = 6 dias. |
| **Data de esgotamento** | Dia em que o último item do produto é consumido (o estoque chega a zero no fim desse dia). | Começou a consumir em 12/10 com disponibilidade de 6 dias: esgota em 17/10. |
| **Prazo de validade padrão** | Quantos dias, em média, um produto dura até vencer. Vem de pesquisa em várias fontes e pode ser ajustado. | Leite: 120 dias. |
| **Data de vencimento** | Último dia em que o lote é próprio para consumo: data da compra + prazo de validade (ou a data impressa na embalagem). | 12/10 + 120 dias = 09/02. |
| **Antecedência** | Quantos dias antes de um evento (esgotamento ou vencimento) o app envia cada alerta. Padrão: 2 dias e 1 dia, com um terceiro opcional. | Avisar 2 dias e 1 dia antes de acabar. |
| **Alerta** | Notificação push no dispositivo, para o que é urgente; também aparece como aviso na aba de notificações do app. Prioridade 1. | "Seu leite acaba em 2 dias." |
| **Aviso** | Notificação que aparece só dentro do app, na aba de notificações; só aconselha e deixa registrado. Prioridade 2. | "O leite acabou e foi para a lista de compras." |
| **Lista de próximas compras** | Lista dos produtos que precisam ser comprados, com um checklist para marcar o que foi comprado. | Leite, arroz, shampoo. |

## 3. Regras

### BR-01: Consumo reduz o estoque

**Regra.** O consumo é contabilizado por dia sobre o estoque total do produto e o reduz diariamente. O consumo é uma taxa e aceita decimais em qualquer medida (por exemplo, 0,6 unidade por dia). O estoque nunca fica abaixo de zero. O consumo começa no dia da compra. Exceção: se o estoque do produto estava zerado, uma compra feita **depois das 16h** (fuso do espaço de trabalho) só começa a ser consumida no dia seguinte. Se ainda havia estoque, o horário da compra não faz diferença. Essa é a única regra que usa horas; o resto do app trabalha só com datas.

**Fórmula.** Estoque no fim do dia D = quantidade comprada − soma do consumo de cada dia contado, do primeiro dia de consumo até D (inclusive).

**Exemplo.** Compra de 6 leites em 12/10 às 10h, consumo de 1 por dia. No fim de 12/10 sobram 5; no fim de 13/10, 4; e assim por diante. Se a compra fosse às 17h com o estoque zerado, o fim de 12/10 ainda teria 6, e o consumo começaria em 13/10.

### BR-02: Lote vencido zera o estoque e mantém o histórico

**Regra.** O dia da data de vencimento ainda vale para consumo. No dia seguinte, o estoque restante do lote vai a zero, o lote recebe o status "vencido" e permanece no histórico. O app recomenda descartar o que sobrou. Lote vencido não é consumido.

**Exemplo.** Lote com vencimento em 09/02 e 2 itens restantes: em 09/02 ainda pode ser consumido; em 10/02 o estoque do lote vai a 0, o status passa a "vencido" e o app avisa para descartar.

### BR-03: Notificações de reposição e de vencimento

**Regra.** Os dois tipos de evento (reposição e vencimento) seguem o mesmo padrão:

1. **Alertas** nas antecedências configuradas (BR-04). Por padrão, 2 dias e 1 dia antes do evento;
2. No dia do evento, apenas um **Aviso**, para não incomodar.

- **Reposição** (por produto): o evento é a data de esgotamento.
- **Vencimento** (por lote): o evento é a data de vencimento, e as notificações só existem se o lote ainda tiver estoque nesse dia. Se o lote acabar antes de vencer, elas deixam de existir.

Todo Alerta é uma notificação push e também aparece como Aviso na aba de notificações do app; o Aviso aparece só no app. Alerta é para o que é urgente; aviso só aconselha e deixa registrado.

Sempre que uma compra ou uma mudança de consumo altera a data de esgotamento, as notificações de reposição são recalculadas.

**Exemplo.** Leite com esgotamento em 17/10 e antecedência de 2 dias: alertas em 15/10 e 16/10, e aviso em 17/10. O lote vence em 09/02 (alertas em 07/02 e 08/02, aviso em 09/02), mas como o lote acabou em 17/10, essas notificações não são enviadas.

### BR-04: Antecedência configurável

**Regra.** A antecedência é sempre em **dias**, tanto para reposição quanto para vencimento, porque os dois eventos são datas. O usuário configura quantos dias antes cada alerta é enviado. Por padrão, o **primeiro alerta é 2 dias antes** e o **segundo é 1 dia antes**, e ele pode adicionar um **terceiro** se quiser. Cada alerta é independente: mudar o primeiro não altera o segundo. Se dois alertas caem no mesmo dia, só um é enviado. Se a data de um alerta já passou quando o esgotamento é calculado (por exemplo, o produto acaba em 3 dias e o primeiro alerta está configurado para 5), esse alerta não é enviado e só volta a valer no próximo lote; os demais continuam normalmente. Como a data de esgotamento depende do consumo, mudar o consumo muda a data dos alertas de reposição.

**Exemplo.** Esgotamento em 23/10 com os padrões: alertas em 21/10 e 22/10. Se o usuário mudar só o primeiro para 5 dias, os alertas saem em 18/10 e 22/10. Se ele adicionar um terceiro, de 3 dias, sai também um alerta em 20/10. Se o consumo aumentar e o esgotamento passar para 20/10, os alertas são recalculados a partir da nova data. Se o produto acaba em 3 dias e o primeiro alerta está em 5 dias, o de 5 dias não é enviado (a data já passou) e o de 1 dia antes segue normalmente. Se os dois alertas estiverem em 1 dia, só um é enviado.

### BR-05: Validade padrão do produto e ajuste do usuário

**Regra.** Cada produto traz um prazo de validade padrão, em dias, calculado a partir de várias fontes (as fontes ficam registradas). Cada lote tem sua própria data de vencimento e sua marca. O usuário pode editar a validade de um lote informando a data impressa na embalagem:

- o app converte a data em dias (data de vencimento − data da compra) e esse número passa a ser o novo prazo padrão do produto naquele espaço de trabalho, valendo para os lotes seguintes;
- se o usuário escolher **apenas este lote**, o padrão não muda.

Lotes anteriores nunca mudam. Os ajustes valem só para aquele espaço de trabalho. Se o usuário não editar um lote, ele usa o prazo padrão vigente.

**Exemplo.** O padrão do leite é 120 dias. O usuário compra 3 lotes. O lote 2 vem com validade menor e ele a edita para 100 dias: o lote 3 já nasce com 100. Se o lote 3 vier normal, ele edita de volta para 120. Se, em vez disso, ele tivesse marcado "apenas este lote" no lote 2, o lote 3 continuaria com 120.

### BR-06: Compra de um novo lote com estoque ainda em casa

**Regra.** Cada compra cria um lote novo, com sua própria data de vencimento e marca. Os lotes anteriores não mudam. O estoque do produto é a soma dos lotes. O consumo sai primeiro do lote com **vencimento mais próximo**, mesmo que não seja o mais antigo. A data de esgotamento e os alertas de reposição são recalculados; os alertas de vencimento continuam por lote.

**Exemplo.** Veja a seção 4: a compra de 15/10 move o esgotamento de 17/10 para 23/10, mas não muda o vencimento do lote de 12/10.

### BR-07: Mudança e agendamento de consumo

**Regra.** Todo produto já vem com um consumo predefinido, que só muda quando o usuário edita. O consumo pode ser informado de duas formas:

- **direto**: por exemplo, 130 g por dia;
- **como duração**: "esta quantidade dura N dias", e o app calcula consumo = quantidade ÷ N.

Ao editar, há três opções de vigência:

1. **Sem data:** vale a partir de hoje, até a próxima mudança.
2. **Com data inicial:** vale a partir dessa data, até a próxima mudança.
3. **Com data inicial e final:** vale só nesse período; depois, volta ao consumo anterior.

O passado nunca é alterado: o histórico e o estoque já calculados permanecem. Só os dias a partir da vigência usam o novo consumo. Os agendamentos trabalham com datas, não com horas. Se um agendamento se sobrepõe a outro, vale o mais recente: se os dois começam no mesmo dia, o anterior é removido por inteiro; se o anterior começa antes, ele é mantido só até o dia anterior ao início do novo, e o novo vale dali em diante.

**Exemplo.** Consumo de 1 leite por dia. Visitas de 20/10 a 22/10: o usuário agenda 3 por dia nesse período, e em 23/10 o consumo volta a 1. Outro caso: 1,3 kg de shampoo que dura 10 dias → 1.300 g ÷ 10 = 130 g por dia. Sobreposição: já existe um agendamento de 3 por dia de 20/10 a 25/10 e o usuário cria outro de 1 por dia a partir de 23/10; o primeiro vale de 20/10 a 22/10 e o novo vale de 23/10 em diante. Se o novo começasse em 20/10, o primeiro seria removido.

### BR-08: Medidas, quantidades e embalagem

**Regra.** Existem três famílias de medida: **unidade**, **peso** (kg e g) e **volume** (L e mL). Valem as conversões 1 kg = 1000 g e 1 L = 1000 mL. A **quantidade comprada** aceita decimais em peso e volume; em unidade, é sempre inteira. O **consumo** é uma taxa e pode ser decimal em qualquer medida (BR-01). Cada produto tem uma embalagem padrão (leite: caixa com 12 unidades), que o usuário pode editar na compra. Como na validade (BR-05), a edição vira o padrão dos próximos lotes, ou vale só para aquele lote. O lote grava o total de itens resultante.

**Exibição.** O estoque é exibido em itens inteiros, junto com o consumo e, quando o produto tem medida (g, mL), o total do item. Um item só sai da contagem quando o consumo acumulado completa 1 item inteiro; até lá, continua valendo 1. Não há arredondamento nem decimal de item. Internamente, o cálculo (BR-01) usa o valor com decimais.

**Exemplo.** A marca vem com caixa de 6: o usuário edita a embalagem para 6 e compra 2 caixas, e o lote passa a ter 12 unidades. Comprar 1,5 kg de arroz é válido; comprar 1,5 ovo, não. Já consumir 0,5 ovo por dia (1 a cada 2 dias) é válido, porque é uma taxa. Shampoo de 1.300 g com consumo de 130 g por dia: aparece como "1 frasco" (1.300 g, 130 g por dia) durante 10 dias e só passa a 0 quando os 1.300 g são consumidos. Leite com 6 unidades e consumo de 0,6 por dia: no fim do dia 1 continua 6 (consumiu 0,6); no fim do dia 2 passa a 5 (consumiu 1,2).

### BR-09: Estoque zerado

**Regra.** Quando o estoque do produto chega a zero (data de esgotamento):

- o estoque exibido passa a ser 0;
- o app envia apenas um **Aviso** dentro do app, sem alerta no dispositivo (os alertas já foram enviados antes);
- o lote esgotado permanece no histórico (calendário).

O produto entra na **lista de próximas compras** já no **primeiro alerta** de reposição, para dar tempo de planejar a ida ao mercado. Se a data desse alerta já passou quando o esgotamento é calculado, o produto entra na lista imediatamente.

**Exemplo.** Leite com esgotamento em 23/10: o leite entra na lista em 21/10, junto com o primeiro alerta; em 23/10 o estoque aparece como 0, o aviso chega no app e os lotes ficam no calendário como esgotados.

### BR-10: Espaço de trabalho, membros e permissões

**Regra.** Um espaço de trabalho reúne até 7 membros (limite inicial, que pode mudar). Toda alteração (consumo, validade, embalagem, fuso horário) vale para o espaço inteiro e todos os membros a veem. O fuso horário é definido uma vez no espaço e vale para todos. Os perfis são:

- **Criança:** só visualiza.
- **Adolescente:** pode editar tudo, mas a alteração só passa a valer depois da validação de **qualquer adulto**. Enquanto está pendente, continua valendo o valor atual, até que um adulto aprove ou rejeite a mudança. Marcar itens no checklist da lista de próximas compras não precisa de validação (BR-11).
- **Adulto:** edita tudo.

O **criador** do espaço é responsável e pode designar mais um adulto como responsável. As **pendências de validação** (mudanças e listas finalizadas por adolescentes) aparecem na aba de notificações de **todos os adultos**, sem push: não há problema em demorar para ver. O **registro de atividade** (quem alterou o quê) é visível **só para os responsáveis**, não gera push e aparece apenas na aba. A aba dos responsáveis junta esse registro com os avisos de vencimento e reposição, organizada para que vejam o que está perto de vencer sem precisar rolar a lista.

**Exemplo.** João (adolescente) muda o consumo de leite de 1 para 2 por dia. A mudança fica pendente e aparece na aba de notificações; Ana (adulta, criadora e responsável) ou Carlos (adulto, não responsável) valida; a partir daí o novo consumo vale para todos.

### BR-11: Registro de compra pela lista de próximas compras

**Regra.** Marcar um item no checklist da lista de próximas compras **não altera o estoque**. A compra só é registrada quando o usuário **finaliza a lista**. Nesse momento, cada item marcado vira um lote (BR-06) com os valores padrão (embalagem e validade padrão), e o app abre uma etapa para o usuário editar o que comprou (quantidade, marca, embalagem, validade). Essa etapa pode ser ignorada: o lote pode ser editado depois, direto no estoque. Os itens marcados saem da lista, e os não marcados continuam nela, para todos, porque ainda não foram comprados. Se um adolescente finaliza a lista, ele pode marcar itens e editar marca, quantidade e validade normalmente, mas a entrada no estoque só vale depois da validação de um adulto (BR-10).

**Exemplo.** Ana vai ao mercado, marca leite e arroz e finaliza a lista. O app cria um lote de leite (caixa de 12, validade padrão) e um de arroz, e pergunta se ela quer ajustar algo. A caixa de leite veio com 6, então ela edita; o arroz fica como está. Se João (adolescente) tivesse finalizado a lista, os lotes só entrariam no estoque depois que um adulto validasse.

### BR-12: Entrada manual no estoque

**Regra.** O usuário pode adicionar ao estoque um produto que já estava em casa e não foi comprado pelo app. Ele informa o produto, a quantidade e o prazo em dias, que é o tempo que ainda resta, contado a partir de hoje. O app cria um lote com início na data da entrada e fim no início + prazo. Esse lote funciona como qualquer outro: aparece no estoque e no calendário, gera os alertas e o aviso (BR-03 e BR-04) e entra na lista de próximas compras (BR-09). A entrada manual não passa pela lista de compras, e o lote pode ser editado depois, direto no estoque.

**Exemplo.** Ana já tem uma caixa com 12 leites em casa e acha que dura mais 30 dias. Em 10/11, ela adiciona ao estoque: leite, 12 unidades, prazo de 30 dias. O app cria um lote de 10/11 a 10/12, envia alertas em 08/12 e 09/12 e um aviso em 10/12.

## 4. Exemplo completo

Cenário: leite em caixa de 6, consumo de 1 por dia, validade padrão de 120 dias, antecedência de 2 dias (reposição e vencimento). Estoque no fim de cada dia.

| Data | Evento | Lote A | Lote B | Total |
|---|---|---|---|---|
| 12/10 | Compra do lote A (6 leites, antes das 16h). Vencimento: 09/02. Esgotamento previsto: 17/10. | 5 | – | 5 |
| 13/10 | Consumo | 4 | – | 4 |
| 14/10 | Consumo | 3 | – | 3 |
| 15/10 | Compra do lote B (6 leites). Vencimento: 12/02. O consumo sai do lote A. Esgotamento recalculado para 23/10. | 2 | 6 | 8 |
| 16/10 | Consumo | 1 | 6 | 7 |
| 17/10 | Lote A esgotado (vai para o histórico). O produto ainda tem estoque, então não há notificação de reposição. | 0 | 6 | 6 |
| 21/10 | **Alerta** de reposição (2 dias antes de 23/10). O leite entra na lista de próximas compras. | 0 | 2 | 2 |
| 22/10 | **Alerta** de reposição (1 dia antes) | 0 | 1 | 1 |
| 23/10 | Lote B esgotado. Apenas um **Aviso** no app (BR-09). | 0 | 0 | 0 |

Observações:

- Sem a compra de 15/10, os alertas de reposição teriam saído em 15/10 e 16/10. A compra os recalculou para 21/10 e 22/10.
- As notificações de vencimento (07/02, 08/02 e 09/02 para o lote A; 10/02, 11/02 e 12/02 para o lote B) deixam de existir, porque os dois lotes acabaram antes de vencer (BR-03).

## 5. Questões em aberto

Nenhuma no momento. Novas dúvidas entram aqui.

## 6. Futuro

- Reconhecer o produto, a marca e, se possível, a validade a partir de uma foto, com um modelo de IA. Fora do escopo do MVP.
- Trabalhar com horas nos agendamentos de consumo.
