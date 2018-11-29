## Otimização da implementação Adobe Target

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
