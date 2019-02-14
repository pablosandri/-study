![CI&T](https://pablosandri.github.io/sandbox/ciandt.png)

# CI&T - Fleet

Última atualização: 28/02/2018

Em caso de dúvidas, entrar em contato com: [psandri@ciandt.com](mailto:psandri@ciandt.com)

# Objetivo

Este documento tem como objetivo documentar a implementação do Google Tag Manager e camada de dados para utilização de recursos de monitoramento do Google Analytics.

# Overview e Descrições Técnicas

## Google Tag Manager 

É uma ferramenta da Google onde são inseridas pequenas instruções javascript com a finalidade de estruturar a coleta dados e unificar diversos fornecedores de tags terceiros sem a necessidade de várias implementações complexas de hardcode do projeto. 

- Instalação

  Para instalar o  Google Tag Manager é preciso que o desenvolvedor inclua os códigos abaixo no HTML do site, em todas as páginas do site proposto. Caso o site possua algum template comum que é inserido em todas as páginas, também pode ser utilizado.

Cole o código abaixo após a tag `<head>` do site:

```html
<!-- Google Tag Manager -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start': new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0], j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src='https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);})(window,document,'script','dataLayer','GTM-TPWCNC9');</script>
<!-- End Google Tag Manager -->
```

Cole o código abaixo, após a tag `<body>` do site:

```html
<!-- Google Tag Manager (noscript) -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?GTM-TPWCNC9" height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<!-- End Google Tag Manager (noscript) -->
```

## Camada de dados (DataLayer)

É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação. 

- Instalação

Inserir a camada de dados antes do snippet de instalação do Google Tag Manager. Exemplo:

			
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'atributo1': 'valor1',
    'atributo2': 'valor2'
  });
</script>
```

## Atributos HTML (Data Attributes)

São atributos customizados inseridos nos elementos HTML da página que permite a inclusão de dados adicionais.

- Instalação

1. Elementos de link: ```<a href="..." class="minha_classe">Link</a>```

Elementos do tipo link que foram mapeados, precisam receber a classe **gtm-link-event** e os data attributes em sua estrutura.

```html
<a href="http://www.meudominio.com.br/page2"
  class="minha_classe gtm-link-event"
  data-gtm-event-category="exemplo valor categoria"
  data-gtm-event-action="exemplo valor acao"
  data-gtm-event-label="exemplo valor rotulo">Texto do link</a>
```

2. Elementos comuns: ```<div class="minha_classe">Elemento</div>``` 

Todos os elementos comuns do html que não são links e que foram mapeados, precisam receber a classe **gtm-element-event** em sua estrutura.
		
```html
<div class="minha_classe gtm-element-event" 
  data-gtm-event-category="exemplo valor categoria"
  data-gtm-event-action="exemplo valor acao"
  data-gtm-event-label="exemplo valor rotulo">Texto do elemento</div>
```

## Eventos <br />

São estruturas de dados que muitas vezes são consideradas como conversões ou micro conversões e servem para identificar as interações do usuário que foram mapeadas para coleta. Esses eventos podem ser implementados através de Data Atributos ou Camada de Dados conforme descrito acima.


> **Observação**
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />
> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais.

---


# Implementação

## Monitorando os pageviews

Para cada tela da aplicação, é necessário enviar um push no dataLayer informando que a página carregou.

> **Observação**
> É importante carregar em todas as páginas e nas trocas via ajax.
> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais.


```javascript
<script>
	window.dataLayer = window.dataLayer || [];
	dataLayer.push({
	  'event': 'virtual-pageview', //fixo
	  'pageViewName': '[[Nome da página]]'
	})
</script>
```

### Login

Essa seção deve estar presente em todas as páginas do site. 

Descrição: Disparar as informações no dataLayer no callback da função de login.

```javascript
  window.dataLayer = window.dataLayer || [];
  dataLayer.push({
    'event': 'login', // fixo
    'userId': 'psandri',
    'eventCategory': 'login', // fixo
    'eventAction': 'sucesso', // fixo
    'eventLabel': 'login' //fixo
  });
```

### Logout

Descrição: Disparar as informações no dataLayer no callback da função de logout em caso de sucesso.

```javascript
  window.dataLayer = window.dataLayer || [];
  dataLayer.push({
    'event': 'logout' // fixo
  });
```

<br />

## Eventos

## Reserva

Descrição: Disparar as informações no dataLayer no momento em que a reserva for concluida.

> *Descrição*: é importante que ocorra na pagina de conclusão da compra e que ocorra apenas 1 vez, mesmo que a página seja atualizada, ou vamos ter problemas com transações duplicadas.

Por exemplo:

```javascript
window.dataLayer = window.dataLayer || [];
dataLayer.push({
  'event': 'event',
  'eventCategory': '[[pagina]]',
  'eventAction': 'reservar',              //fixo
  'eventLabel': 'sucesso',               //fixo
  'dimension3' : '[[individual || carona]]',
  'dimension4' : '[[carro]]',
  'dimension5' : '[[area solicitante]]',
  'dimension6' : '[[destino]]',
  'dimension7' : '[[data e hora de retirada]',
  'dimension8' : '[[data e hora de devolucao]]',
  'dimension9' : '[[data do rodizio]]',
  'dimension10' : '[[numero de passageiros]]',
  'dimension11' : '[[disponibilizar carona]',
  'dimension12' : '[[vagas disponiveis]]',
  'metrics1' : '1'                     //fixo
});
```

| CHAVE    | TIPO  | DESCRIÇÃO |
| :------- | :---- | :--- |
| eventCategory | String | Página |
| dimension3 |String | Tipo da reserva concluída, ex.: Individual || Carona |
| dimension4 |String | Nome do carro reservado: Ford Ka |
| dimension5 |String | Nome da área solicitante: Canais Digitais - IT |
| dimension6 |String | Destino da reserva: CEIC |
| dimension7 |String | Data e hora da retirada: 15/2/2018 9:00 |
| dimension8 |String | Data e hora da devolução: 15/2/2018 9:00 |
| dimension9 |String | Dia de rodízio do carro selecionado: Quinta-feira |
| dimension10 |String | Número de passageiros para que a reserva foi feita: 4 |
| dimension11 |String | Disponibilizar carona?: Sim || Não |
| dimension12 |String | Número de vagas disponíveis no carro selecionado: 3 |


## Pesquisa

Descrição: disparar no clique do botão *PESQUISAR*.

```javascript
window.dataLayer = window.dataLayer || [];
dataLayer.push({
  'event': 'event',
  'eventCategory': '[[pagina]]',
  'eventAction': 'filtro',    //fixo
  'eventLabel': 'pesquisar',  //fixo
  'dimension6' : '[[destino]]',
  'dimension7' : '[[data e hora de retirada]',
  'dimension8' : '[[data e hora de devolucao]]',
});
```

| CHAVE    | TIPO  | DESCRIÇÃO |
| :------- | :---- | :--- |
| eventCategory | String | Página |
| dimension6 |String | Destino da reserva: CEIC |
| dimension7 |String | Data e hora da retirada: 15/2/2018 9:00 |
| dimension8 |String | Data e hora da devolução: 15/2/2018 9:00 |

## **Micro-Conversões**: Botões

Quando o usuário interagir com algum elemento da página.

```javascript
window.dataLayer = window.dataLayer || [];
dataLayer.push({
  'event': 'event',
  'eventCategory': '[[pagina]]',
  'eventAction': '[[area-click]]',
  'eventLabel': '[[Texto-do-botão]]'
});
```

OU mapear os elementos HTML com Data Attributes.

```html
<a href="http://www.meudominio.com.br/page2"
  class="minha_classe gtm-link-event"
  data-gtm-event-category="exemplo valor categoria"
  data-gtm-event-action="exemplo valor acao"
  data-gtm-event-label="exemplo valor rotulo">Texto do link</a>
```

```html
<div class="minha_classe gtm-element-event" 
  data-gtm-event-category="exemplo valor categoria"
  data-gtm-event-action="exemplo valor acao"
  data-gtm-event-label="exemplo valor rotulo">Texto do elemento</div>
```

| CHAVE    | TIPO  | DESCRIÇÃO |
| :------- | :---- | :--- |
| eventCategory | String | Página |
| eventAction | String | Area-click ex: pop-up:bem-vindo, footer, header, body e etc. |
| eventLabel |String | Label do botão ex: começar, faq e etc. |

