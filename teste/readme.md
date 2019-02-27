# Serasa Empreendedor

## Marketplace de crédito

#### Analytics
##### Nova implementação no *Adobe Analytics* para suportar diferentes produtos na simulação.

#### Email Mkt
##### Automação das reguás de email mkt. Dados coletados e enviados para o *Eloqua*:

```html
<!--
  Acesso LP, Início Simulação, Data de início da última simulação, Possui garantia, Tem Nfe ou Cheque, Finalizou simulação, Data de fim da última simulação

  Simulação com oferta, Oferta parcelado, Oferta antecipação, Data da última oferta antecipação ,Data da última oferta parcelado

  Lead parcelado, Data do último lead parcelado, Lead antecipação, Data do último lead antecipação

  Cliente validado, Data do promote, Preencheu formulário Ad

  Simulação sem oferta, Data da última simulação sem oferta
-->
```

## Saúde Financeira

#### Email Mkt
##### Enriquecimento na coleta de dados de compra referente aos produtos Recomendação, Saúde Avulso e Assinatura. Dados coletados:

```html
<!--
  Recomenda: Purchase, Purchase_Last_Date, Payment_Methods
  SF-Avulso: Purchase, Purchase_Last_Date, Payment_Methods
  SF-Assinatura: Purchase, Purchase_Last_Date, Payment_Methods
-->
```


# Consulta Serasa

## Nova arquitetura de mensuração
##### Novo Tag Manager Implementado para garantir a coleta de dados estruturados e interações harmoniosas com aplicações de página única (SPAs).

## Analytcs
##### Novo tagueamento de Purchase e integração com O2C. 
##### Dados disponibilizados:


## Target (teste a/b)
##### Corrigido a implantação do *Adobe Target* que impossibilitava o uso no site. Agora é possivel personalizar a jornada do usuário em todas as páginas, relatórios e pagamento.

## Email Mkt
##### Implantação do *Eloqua* via front-end e duas triggers implementadas.

Cadastro:
Quando o usuário se cadastra na plataforma automaticamente é cadastrado no Eloqua em real-time.

Purchase:
Na compra é gravado todos os detalhes no eloqua.








