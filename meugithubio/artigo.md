[//]: # (data-criacao:2020-04-28)
[//]: # (resumo:Após uns 7 anos sem mexer com web, resolvi fazer o meu GitHub Pages e compartilho o que aprendi e como fiz.)
[//]: # (hashtags:web .net)
[//]: # (#imagem:header.jpg)
# GitHub.io: ideias para fazer seu próprio site

Não sei se você sabe, mas o GitHub.com tem um recurso chamado [GitHub Pages](https://pages.github.com/). Ele permite que você disponibilize conteúdos estáticos de página da web (html, css, javascript, imagens etc) de forma gratuita armazendo tudo no seu repositório público.

Com uma conta criada no GitHub, a URL do seu site no GitHub Pages fica assim: https://oliveira-michel.github.io/

Para publicar, basta criar e colocar todo o conteúdo em um repositório público, por exemplo, o meu: https://github.com/oliveira-michel/oliveira-michel.github.io.

Como são apenas conteúdos estáticos não rodam código servidor (.net, Java etc.) para gerar as páginas dinamicamente. Apesar disso, pensei: eu poderia organizar e distribuir meus conteúdos em um ambiente mais personalizado do que apenas compartilhá-los via respositórios públicos como eu vinha fazendo até então! Na hora me vieram dois problemas: não posso fazer em ASP.net - que eu já conhecia bem - e faz uns 7 anos que não mexia em nada web. Um probleminha por vez fui solucionando e compartilho alguns insights.

## Markdown

Markdown é uma notação de texto que permite itens básicos de formatação e pra mim acho rápido de escrever com ela. Me atende em 90% dos cenários e quando não, faço algum contorno com HTML. Conteúdos em Markdown são convertidos para HTML ao serem exibidos na tela, por exemplo, como nos README.md do GitHub.

Faz tempo que já escrevo todos os meus conteúdos em Markdown e armazeno em algum dos meus repositórios do GitHub.

O primeiro editor que tive contato e meu preferido ainda é o [stackedit.io](https://stackedit.io/app).

## Geração dos HTMLs à partir dos Markdowns com .NET Core

Você vai precisar de alguma ferramenta que gere o conteúdo estático à partir de algum lugar. A primeira ideia foi usar o [Jekyll](https://jekyllrb.com).

O Jekyll lê conteúdos em Markdown e gera em HTML em algum dos vários templates que existem para esta plataforma. Como eu gosto muito mais de fazer do que usar as coisas, optei por gastar o tempo me atualizando com web ao invés de aprender Jekyll. Assim, fiz o meu próprio template pro site e um gerador de HTML pra ele.

O gerador encontra-se no repositório https://github.com/oliveira-michel/GeradorGithub e o fiz sem pretenções de reuso ou extensão. O código ficou todo em uma função só na Main e funciona assim:

- coloco no começo de cada markdown comentários chave/valor como data-criacao, resumo, hashtags e imagem para metadados importantes na hora de eu gerar o HTML;
- clono na máquina o repositório com os templates HTML;
- clono na máquina todos os repositórios com os conteúdos em Markdown;

Executo o GeradorGitHub direto no Visual Studio mesmo e ele:

- lê templates HTML do site, cujo caminho defino em variáveis na aplicação;
- lê os arquivos .md, cujo caminho eu defino em um array;
- percorre cada um dos markdowns armazenando os metadados e conteúdo;
- para cada um deles, converte o markdown em HTML usando a biblioteca [Markdig](https://github.com/lunet-io/markdig);
- faz replaces e injeções de tags nos templates HTML com o apoio da biblioteca [HtmlAgilityPack](https://html-agility-pack.net);
- copia as imagens (ilustração no header) + arquivo HTML gerado pelo Markdig em diretórios no repositório local do GitHub Pages;
- copia o index, já com referências para todos os artigos, no repositório local do GitHub Pages;

Reviso o conteúdo gerado e faço push no repositório do GitHub Pages.

## O Template HTML

Quando pensei em montar o site, vislumbrei algo como o Pinterest. Comecei a pesquisar e descobri que o nome da forma como os cards no Pinterest são dispostos, se chama Masonry.

Pesquisando por como fazer Masonry, me inspirei neste template:

https://wordpress.org/themes/koji/

![template koji](https://raw.githubusercontent.com/oliveira-michel/artigos/master/meugithubio/koji.jpg)

Para entender o Masonry, estudei estes dois tutoriais:

https://medium.com/@andybarefoot/a-masonry-style-layout-using-css-grid-8c663d355ebb

https://w3bits.com/css-grid-masonry/

No meio de algumas novidades, esbarrei neste tutorial  passei a virar fâ do css-tricks:

https://css-tricks.com/snippets/css/a-guide-to-flexbox/

Fiz o card da esquerda (com informações pessoais) inspirado neste tutorial da W3Schools:

https://www.w3schools.com/howto/howto_css_profile_card.asp

E entendi como funciona o design responsivo neste conteúdo aqui:

https://www.w3schools.com/howto/howto_js_topnav_responsive.asp

A W3Schools era uma das minhas fontes de consulta na época que eu trabalhava com web. Pra mim era apenas para referências, no entanto, descobri uma coleção de práticas atuais de web que ajudam muito na hora de montar o seu site:

https://www.w3schools.com/howto/

Por conta de um detalhe (ícone) no card de informações pessoais, conheci o Font Awesome que entrega uma vasta biblioteca de ícones vertoriais para usar no site:

https://fontawesome.com/

E é importante sempre ter métricas, por isso, acrescentei o Google Analytics no site:

https://analytics.google.com/

## Próximos passos

### Comentários

Tenho vontade de acrescentar uma área de comentários nos artigos. Ainda não investi tempo nisso, mas já esbarrei em algo que me parece promissor.

O Gitment e Gitalk, via Javascript, implementa comentários usando uma página de Issues do GitHub para armezanar as conversas:

https://github.com/imsun/gitment

https://github.com/gitalk/gitalk

Vi que tem a limitação de só permitir usuário logado do GitHub.

Enfim, é isso! Registrei minha trajetória nesta tarefa de fazer o meu GitHub Pages e espero que algumas informações aqui possam ser úteis pra você.
