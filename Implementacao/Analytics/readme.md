![CI&T](https://pablosandri.github.io/sandbox/empreendedor.jpg)

# Implementação Adobe Analytics - Audiência 

Última atualização: 14/02/2019

Em caso de dúvidas, entrar em contato com: [pablo.sandri@br.experian.com](mailto:pablo.sandri@br.experian.com)

# Objetivo

Este documento tem como objetivo documentar a implementação do Adobe Launch e camada de dados para utilização de recursos de monitoramento do Adobe Analyics.

# Overview e Descrições Técnicas

## Adobe Launch

É uma ferramenta da Adobe onde são inseridas pequenas instruções javascript com a finalidade de estruturar a coleta dados e unificar diversos fornecedores de tags terceiros sem a necessidade de várias implementações complexas de hardcode do projeto. 

- Instalação

Para instalar o  Launch é preciso que o desenvolvedor inclua os códigos abaixo no HTML do site, em todas as páginas do site proposto. Caso o site possua algum template comum que é inserido em todas as páginas, também pode ser utilizado.

Cole o código abaixo após a tag `<head>` do site:

```html
<!-- Adobe Launch (Development) -->
<script src="//assets.adobedtm.com/launch-EN2f1e0631b5294323815d22c26dsabc35f50-development.min.js" async></script>
<!-- End Adobe Launch -->

<!-- Adobe Launch (Producao) -->
<script src="//assets.adobedtm.com/launch-EN2f1e0631b5294323815d22c26bc35sdf50.min.js" async></script>
<!-- End Adobe Launch -->

```


## Camada de dados (DataLayer)

É um Objeto javascript utilizado pelo Launch para receber em seus atributos dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação. 

- Instalação

Inserir a camada de dados antes do snippet de instalação do Google Tag Manager. Exemplo:

			
```html
<html xmlns="http://www.w3.org/1999/xhtml" lang="pt-br" xml:lang="pt-br" class="no-js">
<head>
<meta http-equiv="X-UA-Compatible" content="IE=edge;requiresActiveX=true">
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<meta http-equiv="cache-control" content="no-cache">
<meta name="language" content="pt-br" />
<script>
document.DataLayer = {
	pageInfo: {
		pageName: "SA:NL:MEMEI:Institucional:Home",
		siteSection: "NL",
		subSection: "Institucional",
		subSection2: "Institucional",
		tipoDeCanal: "WEB",
		url: "https://www.serasaempreendedor.com.br",
	}, userInfo: {
		businessId: "djksahdsdhasd",
		clientId: "5a71e736eb1cf54a9c106a8d",
		userId: "SDAFSDAD"
	}, rule: "pageLoad"
}
</script>
<script src="//assets.adobedtm.com/launch-EN2f1e0631b5294323815d22c26dsabc35f50-development.min.js" async></script>
	
```

| CHAVE    | TIPO  | DESCRIÇÃO |
| :------- | :---- | :--- |
| pageName | String | Nome da sua página ou pathName |
| siteSection |String | NL(não logado) ou LG(logado) |
| subSection |String | Não obrigatório |
| subSection |String | Não obrigatório |
| tipoDeCanal |String | WEB, Msite e etc |
| url |String | document.location.href |
| businessId |String | identificador unico da empresa |
| clientId |String | Id do banco de dados |
| userID |String | Identificador unico do usuário |


## Disparo em páginas com carregamento AJAX ou depois de ação do usuário, como clique.

```javascript
window.analyticsData = {

(...)

};

	window.analyticsData = {

(...)

};
document.dispatchEvent(new CustomEvent("CustomPageView",{'detail': document.DataLayer}));
```
