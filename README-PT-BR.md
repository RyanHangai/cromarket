<h1 align="center">CroMarket</h1>

<p align="center">
  <a href="README.md">🇺🇸 English</a> | 🇧🇷 Português
</p>

Um assistente de compras, feito com Python e SQL, que acompanha o que a sua casa compra, prevê quando cada produto vai acabar ou vencer e avisa a tempo de você planejar a ida ao mercado.

## O problema

Muita gente ainda monta a lista de compras à mão e só percebe que algo acabou, ou venceu, quando já é tarde. O CroMarket troca a lista de papel por uma que se mantém sozinha.

## Como funciona

1. **Registre uma compra.** Informe o produto, a quantidade, a marca e, se quiser, a data de validade impressa na embalagem.
2. **O CroMarket cria um lote.** Cada compra vira um lote com sua própria data de vencimento, calculada a partir de uma validade padrão do produto (ajustável).
3. **O estoque diminui todo dia** de acordo com o consumo da sua casa, sempre usando primeiro o lote que vence antes.
4. **Você é avisado a tempo.** Os alertas chegam 2 dias e 1 dia antes de o produto acabar ou de um lote vencer. O produto entra automaticamente na sua lista de próximas compras.

**Exemplo:** você compra uma caixa com 6 leites e a sua casa toma 1 por dia. O CroMarket calcula que ele acaba em 6 dias, envia alertas 2 dias e 1 dia antes e coloca o leite na sua lista. Se você comprar outra caixa antes disso, ele recalcula a data para você.

## Funcionalidades

- **Controle por lote:** cada compra tem sua própria marca, estoque e data de vencimento.
- **Dois tipos de notificação:** reposição e vencimento. Os alertas (push) são para o que é urgente; os avisos ficam dentro do app.
- **Agendamento de consumo:** mude o consumo para visitas, férias ou festas, por um período ou a partir de uma data.
- **Espaço de trabalho compartilhado:** a família divide o mesmo estoque e a mesma lista, com perfis para adultos, adolescentes e crianças.
- **Validades padrão** baseadas em pesquisa em várias fontes, que você pode ajustar para o que realmente comprou.
- **Unidades, peso e volume:** os produtos podem ser controlados em unidades, kg/g ou L/mL.
- **Histórico:** lotes esgotados e vencidos ficam registrados em uma visão de calendário.

## Plataformas

O plano é construir primeiro um **aplicativo mobile**, seguido de um **site** para uso no computador. Os dois usam o mesmo backend em Python, que roda em um contêiner **Docker** na nuvem. Assim, seus dados ficam sincronizados entre o celular e o computador, e o processamento pesado fica no servidor, deixando os dois aparelhos mais leves.

A ideia é permitir o uso parcial sem internet, por exemplo para consultar a lista de compras.

## Tecnologias

| Camada | Escolha |
| --- | --- |
| Linguagem | Python |
| Banco de dados | SQL (motor a definir) |
| Infraestrutura | Docker, em nuvem (provedor a definir) |
| API | A definir |
| Aplicativo mobile | A definir |
| Site | A definir |

## Documentação

- [Regras de negócio](docs/business-rules/business-rules.md) ([pt-BR](docs/business-rules/regras-de-negocio.md)): como funcionam estoque, consumo, lotes e notificações.
- [Roadmap](ROADMAP.md): o plano de desenvolvimento passo a passo.

## Contribuidores

- **Renan** ([@Renanzinhu](https://github.com/Renanzinhu))
- **Ryan** ([@RyanHangai](https://github.com/RyanHangai))

## Licença

Veja o arquivo [LICENSE](LICENSE).
