# GitHub.io: ideias para fazer seu próprio site

Não sei se você sabe, mas o GitHub.com tem um outro domínio chamado GitHub.io. Nele, você pode hospedar conteúdos estáticos de página da web (html, css, javascript, imagens etc). No entanto, são conteúdos estáticos, ou seja, não roda código servidor (.net, Java etc.) para entregar conteúdos dinamicamente.

Aí pensei: eu poderia organizar e distribuir meus artigos em um ambiente mais personalizado do que apenas compartilhar os markdowns renderizados via GitHub faz, que era o que eu vinha fazendo antes.

Problema: não posso rodar ASP.net e faz uns 10 anos que não mexia com web.

Uma coisa de cada vez, fui solucionando e compartilho alguns insights.

Para publicar, basta colocar conteúdo no repositório xxxx.

## Markdown

Markdown é uma notação de texto que permite itens básicos de formatação e pra mim, acho super rápido de escrever com ela. Me atende em 90% dos cenários e quando não atende, faço algum contorno com HTML. Conteúdos em Markdown são convertidos para HTML ao serem exibidos na tela, por exemplo, como nos README.md do GitHub.

Escrevo todos os meus conteúdos em Markdown e armazeno em algum repositório do GitHub.

Gosto deste editor online: 
<img ...
https://stackedit.io/app

## Como gerar conteúdo dinâmico

No GitHub.io você precisa de algum gerador de conteúdo estático, ou seja, algo precisa pegar seus conteúdos e gerar um site com 100% já renderizado em HTML e tecnologias que toda no navegador. A primeira ideia foi usar [Jekyll](https://jekyllrb.com).

<img src=base64 ...>

O Jekyll lê conteúdos em Markdown e gera em HTML em algum dos vários templates que existem para esta plataforma. Como eu gosto muito mais de fazer as coisas do que usar as coisas optei por não gastar tempo em aprender o Jekyll. Fiz o meu próprio template para "tirar a ferrugem" com web; fiz meu próprio gerador de HTML.

O gerador está disponível no ENDERECO DO GERADOR e o fiz sem pretenções de reuso ou extensão. O código ficou todo em uma função só na Main e funciona assim:

- coloco no começo dos markdowns comentários chave/valor como data-criacao, resumo, hashtags e imagem para metadados importantes na hora de eu gerar o HTML;
- clono na máquina todos os repositórios com os templates;
- clono na máquina todos os repositórios com os markdown;

O GeradorGitHub:

- lê templates de HTML do site, cujo caminho defino na aplicação;
- lê os arquivos .md, cujo caminho eu defino em um array;
- percorro em loop cada um dos markdowns armazenando os metadados e conteúdo;
- para cada um deles, converto o markdown em HTML usando a biblioteca Markdig;
- faço replaces e injeções de tags nos templates HTML com o apoio da biblioteca HtmlAgilityPack;
- copia as imagens (ilustração no header) + arquivo HTML do artigo em diretórios no repositório local do GitHub.io;
- copia o index já com referência par todos os artigos no repositório local do GitHub.io;

Reviso o conteúdo gerado e dou push no repositório do GitHub.io.

## O Template HTML

Quando pensei em montar o site, pensei em algo tipo o Pinteres. Comecei a pesquisar a descobri que o nome da forma como os cards no pinteres são dispostos, se chama Masonry.

Pesquisando por Masonry, achei e me inspirei neste template:

https://wordpress.org/themes/koji/

Para entender o Masonry, estudei estes tutoriais:

https://medium.com/@andybarefoot/a-masonry-style-layout-using-css-grid-8c663d355ebb
https://w3bits.com/css-grid-masonry/

No meio de algumas novidades, esbarrei nestes tutoriais e passei a virar fâ do css-tricks:

https://css-tricks.com/snippets/css/a-guide-to-flexbox/

https://css-tricks.com/a-couple-of-use-cases-for-calc/

Fiz o card da esquerda inpirado neste tutorial da w3Schools:

https://www.w3schools.com/howto/howto_css_profile_card.asp

E entendi como funciona o design responsivo do menu nestes conteúdos aqui:
https://www.w3schools.com/howto/howto_js_topnav_responsive.asp





## Próximos passos
GitChat
