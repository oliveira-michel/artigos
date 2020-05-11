# Escrevendo APIs melhores com o Jhulis

Linguagens para definição de contratos de REST APIs, como [OpenAPI Specification (aka Swagger)](https://swagger.io/docs/specification/about) servem para gerar um documento que pode ser usado em gateways, middlewares, geração de código, entre outros e, principalmente, gerar documentação para os usuários.

Uma das formas de se iniciar um projeto com APIs é [definindo este documento (contrato)](https://oliveira-michel.github.io/artigos/2020/01/28/definindo-contratos-de-rest-apis.htm) antes de se iniciar a programação da API. O ideal, inclusive, é que este contrato seja definido ainda na fase de concepção do projeto, dado que neste processo muitas dúvidas são levantadas e há maior proximidade com o negócio. É o que chamamos de **contract-first**.

No entanto, sabemos que nem toda API nasce com todo o seu escopo definido e muitas implementações acontecem através de projetos,  principalmente em empresas e sistemas grandes. Ou seja, a cada projeto um pedaço do software vai sendo implementado.

Nesse processo, conhecer e aplicar [boas práticas ao se definir o contrato](https://oliveira-michel.github.io/artigos/2019/07/11/guia-de-design-rest.htm) é essencial para se criar contratos que possam evoluir com o tempo sem quebrar a compatibilidade com os usuários anteriores.

As empresas têm criado times especialistas em APIs para orientar os desenvolvedores e fazer com que todo o ecossistema integrado via API tenha uma convergência à alguns padrões. Com isso, a curva de aprendizagem e automações possíveis melhora, fazendo com que cada vez mais, os consumidores de API gastem menos tempo para usar novas implementações nos sistemas.

> Leia também: [Governança de REST APIs : Por onde começar?](https://www.linkedin.com/pulse/governan%25C3%25A7a-de-rest-apis-por-onde-come%25C3%25A7ar-michel-oliveira-e-oliveira)

## Gargalos e falhas humanas

Dois grandes problemas acontecem em cima disso tudo aí em cima:

* Existem muitos **detalhes / regrinhas** para se fazer uma API Restfull (que adota as práticas básicas do REST) e aderente ao que a empresa considera como boas práticas. Muitos deles **passam desapercebido** pelo desenvolvedor inexperiente e até mesmo pelo especialista que orienta esses desenvolvedores. Minha experiência é de ver usuários reclamando de incoerência no tipo de detalhe que um especialista observava e que outro não. 
* O **acesso aos especialistas pode virar um gargalo** dependendo do tamanho da empresa e do time de especialistas. Aqui novamente surgem reclamações, principalmente quando a modelagem da API do projeto já chega nos especialistas com o projeto atrasado.

## Como o Jhulis ajuda a solucionar esses problemas

A avaliação funcional das APIs, ou seja, análise da granularidade com que as informações são disponibilizadas, a aderência dos recursos disponibilizados na API ao modelo de domínio do negócio entre outros, ainda precisa ficar nas mãos de especialistas em negócio e REST APIs. Conhecer um pouco de [Domain Driven Design](https://oliveira-michel.github.io/artigos/2020/01/28/definindo-contratos-de-rest-apis.htm#entendendo-e-representando-o-neg%C3%B3cio) ajuda nesta hora. No entanto, a parte da análise que é apenas técnica pode ser automatizada. Por exemplo:

* uma propriedade do tipo string cujo valor de exemplo só tem números é uma provável candidata a se tornar uma propriedade do tipo number;
* uma rota de API que não retorna nenhum caso de 2XX (sucesso) provavelmente foi por conta de esquecimento por parte o analista;
* uma rota de API que não retorna nenhum caso de 4XX ou 5XX (erros) provavelmente foi por conta de esquecimento por parte o analista;
* se a empresa define que o versionamento se dá no padrão '/v1/', por exemplo e o analista define no contrato a versão como 1.0.0, provavelmente, ele não conhece o padrão;
* se não há descrições e exemplos, isso pode ser melhorado;
* se existem rotas com recursos do tipo "/gravar-isso", "apagar-aquilo" etc., provavelmente o analista não está utilizando corretamente os verbos HTTP e nomeando corretamente os recursos.

O [Jhulis](https://github.com/oliveira-michel/Jhulis) é  um projeto Open Source, em dotNET Core, capaz de fazer mais de 30 sugestões de ajustes como essas, fazendo com que o contrato da API fique mais aderente às boas práticas sem depender de um especialista em APIs orientando neste tipo de detalhes.

Está na versão beta, mas já pode trazer mais eficiência na criação de bons contratos de API para o seu time de desenvolvimento.

## Proposta de uso do Jhulis com DEVOPS

O Jhulis pode atuar em dois momentos: na etapa de criação do contrato de API e na etapa de se garantir a qualidade dele através da esteira de CI.

![fluxo de uso do jhulis](https://raw.githubusercontent.com/oliveira-michel/artigos/master/jhulis/fluxo-integracao.png)

No ciclo de desenvolvimento, enquanto o contrato ainda se encontra na máquina/branch do desenvolvedor, o desenvolvedor pode usar o Jhulis fazer a [validação dos aspectos técnicos do contrato](https://github.com/oliveira-michel/Jhulis#post-em-validate). A cada sugestão de ajuste, o desenvolvedor tem oportunidade de corrigir ou, minimamente, refletir se aquilo se aplica à sua necessidade atual.

Após fazer os ajustes para passar por todas as [regras](https://github.com/oliveira-michel/Jhulis#regras) ou adicionar *[supressions](https://github.com/oliveira-michel/Jhulis#supressions)* indicando que alguma regra não se aplica a algum item do contrato, o desenvolvedor submete o contrato para que seja validado por analistas "especialistas em API".

Estes especialistas deverão validar se as *supressions* definidas pelo desenvolvedor fazem sentido ou se podem ajudá-lo a ajustar o contrato para contemplar todas as práticas. Também fazem a análise funcional da API: aderência ao negócio que ela expõe, uso de linguagem ubíqua, se a granularidade dos recursos nas APIs está coerente etc.

Os especialistas podem estar associados a alguma role do Git e a aprovação do merge request associada ao Ok de alguém com esta role.

O contrato e arquivo de supression pode estar em um pasta pré-definida no mesmo repositório do código fonte da API.

No processo de CI, a esteira, executando por exemplo em um Jenkins, Git CI, Git Actions etc. identifica o tipo de software, se for API, busca o contrato, o arquivo de supressions e revalida ele no Jhulis. Caso a validação falhe, significa que algum dos passos anteriores falhou ou não foi executado devidamente. Assim, em tempo, antes de algum primeiro deploy, o desenvolvedor tem oportunidade de fazer os ajustes necessários.

## Conclusão

Quando o desenvolvedor usa o Jhulis no momento da criação do contrato, ele já é estimulado e entender e aprender as regras na prática, mesmo sem ter estudado o guia de práticas da empresa. Este mesmo desenvolvedor, chega no time de especialistas com um nível de maturidade maior e o custo pra isso é um serviço rodando em um servidor: o que é bem mais barato do que a hora de um analista.

O Jhulis integrado em uma esteira de CI, vira um *gate* de qualidade e impede que códigos evoluam sem ter passado por um fluxo de qualidade no que diz respeito ao contrato de API.

> Acesse o projeto do Jhulis no Github: https://github.com/oliveira-michel/Jhulis