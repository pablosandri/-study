![CI&T](https://pablosandri.github.io/sandbox/ciandt.png)

# CI&T - Fleet

Última atualização: 14/03/2019

Em caso de dúvidas, entrar em contato com: [pablo.sandri@br.experian.com](mailto:pablo.sandri@br.experian.com)

# Objetivo

Este documento tem como objetivo orientar a implementação do Google Tag Manager e camada de dados para utilização de recursos de monitoramento do Google Analytics.

# Overview e Descrições Técnicas

## Google Tag Manager 

É uma ferramenta da Google onde são inseridas pequenas instruções javascript com a finalidade de estruturar a coleta dados e unificar diversos fornecedores de tags terceiros sem a necessidade de várias implementações complexas de hardcode do projeto. 

- Instalação

  Para instalar o  Google Tag Manager é preciso que o desenvolvedor inclua os códigos abaixo no HTML do site, em todas as páginas do site proposto. Caso o site possua algum template comum que é inserido em todas as páginas, também pode ser utilizado.

Cole o código abaixo após a tag `<head>` do site:

```html
<!-- Google Tag Manager (Já implementado) -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start': new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0], j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src='https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);})(window,document,'script','dataLayer','');</script>
<!-- End Google Tag Manager -->
```

Cole o código abaixo, após a tag `<body>` do site:

```html
<!-- Google Tag Manager (noscript) -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?GTM-" height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
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
    'eventCategory': 'login', // fixo
    'eventAction': 'sucesso', // fixo
    'eventLabel': 'login' //fixo
    'userId': 'psandri',
    'tipoUsuario': 'Cadastrado', //identificação se usuário cadastrado ou não cadastrado
    'customerID': 'CUSTOMERID' //informar apenas após o usuário autenticar no site
    'possuiEmpresa': 'sim' //informar apenas após o usuário autenticar no site
    'possuiDivida': 'sim' //informar apenas após o usuário autenticar no site
    'nomeEmpresa': 'sim' //informar apenas após o usuário autenticar no site
    'score': '[array]' //informar apenas após o usuário autenticar no site, essa informação deve ser apresentada de forma criptografada.
    'solicitouCartao': 'sim' //informar apenas após o usuário autenticar no site
    'ocupacao': '[array]' //informar apenas após o usuário autenticar no site
    'profissao': '[array]' //informar apenas após o usuário autenticar no site
    'veiculoProprio': 'sim' //informar apenas após o usuário autenticar no site
    'motivoCredito': '[array]' //informar apenas após o usuário autenticar no site
    'tipoCredito': '[array]' //informar apenas após o usuário autenticar no site
    'valorCredito': 'valor' //informar apenas após o usuário autenticar no site
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

