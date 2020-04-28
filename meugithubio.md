# GitHub.io: ideias para fazer seu próprio site

Não se se você sabe, mas o GitHub.com tem um outro domínio chamado GitHub.io. Nele, você pode hospedar conteúdos estáticos de página da web (html, css, javascript, imagens etc). No entanto, são conteúdos estáticos, ou seja, não roda código servidor (.net, Java etc.) para entregar conteúdos dinamicamente.

Aí pensei: eu poderia organizar e distribuir meus artigos em um ambiente mais personalizado do que apenas compartilhar os markdowns renderizados via GitHub faz, que era o que eu vinha fazendo antes.

Problema: não posso rodar ASP.net e faz uns 10 anos que não mexia com web.

Uma coisa de cada vez, fui solucionando e compartilho alguns insights.

## Markdown

Markdown é uma notação de texto que permite itens básicos de formatação e pra mim, acho super rápido de escrever com ela. Me atende em 90% dos cenários e quando não atende, faço algum contorno com HTML. Conteúdos em Markdown são convertidos para HTML ao serem exibidos na tela, por exemplo, como nos README.md do GitHub.

Escrevo todos os meus conteúdos em Markdown e armazeno em algum repositório do GitHub.

Gosto deste editor online: 
<img ...
https://stackedit.io/app

## Como gerar conteúdo dinâmico

No GitHub.io você precisa de algum gerador de conteúdo estático, ou seja, algo precisa pegar seus conteúdos e gerar um site com 100% já renderizado em HTML e tecnologias que toda no navegador. A primeira ideia foi usar [Jekyll](https://jekyllrb.com).

<img src=base64 ...>

O Jekyll lê conteúdos em Markdown e gera em HTMl em algum dos vários templates que existem para esta plataforma. Como eu gosto muito de fazer as coisas optei por não gastar tempo em aprender a usar o Jekyll e fiz o meu próprio template para "tirar a ferrugem" com web

## Próximos passos
GitChat
