![SerasEmpreendedor](https://pablosandri.github.io/sandbox/Serasa%20Empreendedor.jpg)

Área - Digital Analytics

# Adobe Target

Última atualização: 12/09/2017

Em caso de dúvidas, entrar em contato com: [pablo.sandri@br.experian.com](mailto:pablo.sandri@br.experian.com)

## Implementação Adobe Target

### Dynamic Tag Manager

É uma ferramenta da Adobe onde são inseridas pequenas instruções javascript com a finalidade de estruturar a coleta dados e unificar diversos fornecedores de tags terceiros sem a necessidade de várias implementações complexas de hardcode do projeto. 

- Instalação

  Para instalar o DTM é preciso que o desenvolvedor inclua os códigos abaixo no HTML do site, em todas as páginas do site proposto. Caso o site possua algum template comum que é inserido em todas as páginas, também pode ser utilizado.

Cole o código abaixo após a tag `<head>` do site:

Produção:
```html
<script src="//assets.adobedtm.com/5fb4a4ca2787b58aa33f33d1e808a50cf47cc1e0/satelliteLib-a7d32691cef9933bb94547afb02e06958cd9c968.js"></script>
```

Staging:
```html
<script src="//assets.adobedtm.com/5fb4a4ca2787b58aa33f33d1e808a50cf47cc1e0/satelliteLib-a7d32691cef9933bb94547afb02e06958cd9c968-staging.js"></script>
```

Footer Code:	
				
Para o funcionamento correto do DTM, o seguinte código deve ser inserido antes do fechamento da tag ```</body>``` de todas as páginas do ambientes. Esse código é padrão para todos os ambientes:				

```html
  <script type="text/javascript">_satellite.pageBottom();</script>				
```

### Camada de dados (dataLayer)

Para implementar a audiencia customizada por faixa de score é precisamos informar a faixa de score do usuário no dataLayer e persistir essa informação na session do usuário.

EX:

```javascript
document.DataLayer = {
    custom:{
	bucketScore: "default"   //New
    },pageInfo: {
	pageName: "SA:LG:MEMEI:Institucional:Home",
	siteSection: "LG",
	subSection: "Institucional",
	tipoDeCanal: "WEB",
	url: "https://www.serasaempreendedor.com.br/home",
    },userInfo: {
        businessId: "5bb35ad546e0fb000dcae669",
	clientId: "5a71e736eb1cf54a9c106a8d",
	userId: "5bb35ad546e0fb000dcae66a"
    },rule: "pageLoad",
}
```

| bucketScore | Value |
|--|--|
| 0-5 | 'default' |
| 6-99 | 1 |
| 100-199 | 2 |
| 200-299 | 3 |
| 300-399 | 4 |
| 400-499 | 5 |
| 500-599 | 6 |
| 600-699 | 7 |
| 700-799 | 8 |
| 800-899 | 9 |
| 900-1000 | 10 |

