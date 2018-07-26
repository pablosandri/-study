## Homologação ambiente Piki v1

### Todas as páginas

1) Alterar o objeto pageInfo:

DE:
```javascript
pageInfo: {
	ambiente:"NL"
	pageName:"SA:NL:MEMEI:Institucional:Home"
	sitesection:"Institucional"
	subsection:""
	subsection2:""
	tipoDeCanal:"WEB"
	url:"https://serasa-empreendedor.apikihomolog.com/"
}
```

PARA:
```javascript
pageInfo: {
	"url": "document.url",
	"pageName": "Consultar na aba PageNames",
	"siteSection": "NL",
	"subSection": "Institucional ou Blog",
	"subsection2":"",
	"tipoDeCanal": "WEB",
}
```
2) Não estamos conseguindo monitorar os cliques em links. Favor conferir se está acontecendo a atualização da camada de dados e disparo da trigger *em todos os botões*.

Ex:
```javascript
document.DataLayer.custom =  {
         events: ['cliquesGenericos'],
          itemClicado: 'BTN:MEMEI:Institucional:[LabelDoBotao]:[Local]',
         customLink:  'Institucional | CliquesGenericos',
}

document.dispatchEvent(new CustomEvent("CliquesGenericos",{'detail': document.DataLayer}));
```
3) Observei que no nosso ambiente DEV as trocas de páginas não são assícronas, isso vai pendurar para PROD?

Obs: Caso ocorra a troca de página assícrona devemos atualizar a camada de dados e disparar a seguinte trigger:
```javascript
document.dispatchEvent(new CustomEvent("CustomPageView",{'detail': document.DataLayer}));
```
4) Os valores especificados no TechSpec com `[]` são variáveis e seus valores devem ser substituídos.
Ex:

         itemClicado: 'BTN:MEMEI:Institucional:[LabelDoBotao]:[Local]',

    Como deve ser implementado:


         itemClicado: 'BTN:MEMEI:Institucional:ConsulteAgora:Banner',

5) Só pode existir o `userID` e `businessId` quando o user estiver logado. Caso contrario excluir os atributos.
  
