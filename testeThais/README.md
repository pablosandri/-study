# Pablo

Leandro,

Conforme tínhamos conversado, segue o método de avisar as triggers do DTM:

Com jQuery:
```javascript
document.dispatchEvent(new CustomEvent("CustomPageView",{'detail': document.DataLayer}));
```
Com JS:
```javascript
$(document).trigger("CustomPageView", document.DataLayer);
```

Qualquer dúvida estou a disposição.

Obrigado e abs.





# Correção





