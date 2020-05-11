# Escrevendo APIs melhores com o Jhulis: validando boas práticas

Linguagens para definição de contratos de REST APIs, como OpenAPI Specification (aka Swagger) servem para gerar um documento que pode ser usado em gateways, middlewares, geração de código, entre outros e, principalmente, gerar documentação para os usuários.

Uma das formas de se iniciar um projeto com APIs é definindo este documento (contrato) antes de se iniciar a programação da API. O ideal, inclusive, é que este contrato seja definido ainda na fase de concepção do projeto, dado que neste processo muitas dúvidas são levantadas. É o que chamamos de contract-first.

> Leia também: [Definindo contratos de REST APIs](https://oliveira-michel.github.io/artigos/2020/01/28/definindo-contratos-de-rest-apis.htm)

No entanto, sabemos que nem toda API nasce com todo o seu escopo definido e muitas implementações acontecem através de projetos,  principalmente em empresas e sistemas grandes. Ou seja, a cada projeto um pedaço do software vai sendo implementado.

Nesse processo, conhecer e aplicar boas práticas ao se definir o contrato é essencial para se criar contratos que possam evoluir com o tempo sem quebrar a compatibilidade com os usuários anteriores.

> Leia também: [Guia de Design REST](https://oliveira-michel.github.io/artigos/2019/07/11/guia-de-design-rest.htm)

Para orientar os times na adoção destas práticas, as empresas têm criado times especialistas em APIs para orientar os desenvolvedores e fazer com que todo o ecossistema integrado via API tenha uma convergência à alguns padrões, com isso, a curva de aprendizagem e automações possíveis melhora, fazendo com que cada vez mais, os consumidores de API gastem menos tempo para usar novas implementações nos sistemas.

> Leia também: [Governança de REST APIs : Por onde começar?](https://www.linkedin.com/pulse/governan%25C3%25A7a-de-rest-apis-por-onde-come%25C3%25A7ar-michel-oliveira-e-oliveira)

## Problemas disso tudo

Dois grandes problemas acontecem em cima disso tudo aí em cima:

* Existem muitos **detalhes / regrinhas** para se fazer uma API Restfull (que adota as práticas básicas do REST) e aderente ao que a empresa considera como boas práticas. Muitos deles **passam desapercebido** pelo desenvolvedor inexperiente e até mesmo pelo especialista que orienta esses desenvolvedores. Minha experiência é de ver usuários reclamando de incoerência no tipo de detalhe que um especialista observava e que outro não. 
* O **acesso aos especialistas pode virar um gargalo** dependendo do tamanho da empresa e do time de especialistas. Aqui novamente surgem reclamações, principalmente quando a modelagem da API do projeto já chega nos especialistas com o projeto atrasado.

## Como o Jhulis ajuda a solucionar esses problemas

A avaliação funcional das APIs, ou seja, análise da granularidade com que as informações são disponibilizadas, a aderência dos recursos disponibilizados na API ao modelo de domínio do negócio entre outros, ainda precisa ficar nas mãos de especialistas em negócio e REST APIs. Conhecer um pouco de Domain Driven Design ajuda nesta hora. No entanto, a parte apenas técnica pode ser automatizada. Por exemplo:

* uma propriedade do tipo string cujo valor de exemplo só tem números é uma provável candidata a se tornar uma propriedade do tipo number;
* uma rota de API que não retorna nenhum caso de 2XX (sucesso) provavelmente foi por conta de esquecimento por parte o analista;
* uma rota de API que não retorna nenhum caso de 4XX ou 5XX (erros) provavelmente foi por conta de esquecimento por parte o analista;
* se a empresa define que o versionamento se dá no padrão '/v1/', por exemplo e o analista define no contrato a versão como 1.0.0, provavelmente, ele não conhece o padrão;
* se não há descrições e exemplos, isso pode ser melhorado;
* se existem rotas com recursos do tipo "/gravar-isso", "apagar-aquilo" etc., provavelmente o analista não está utilizando corretamente os verbos HTTP e nomeando corretamente os recursos.

O Jhulis é capaz de fazer mais de 30 sugestões de ajustes como essas, fazendo com que o contrato da API fique mais aderente às boas práticas sem depender de um especialista em APIs orientando neste tipo de detalhes.

## Proposta de uso do Jhulis com DEVOPS

O Jhulis pode atuar em dois momentos: na etapa de criação do contrato de API e na etapa de se garantir a qualidade dele através da esteira de CI.

![fluxo de uso do jhulis](https://raw.githubusercontent.com/oliveira-michel/artigos/master/jhulis/fluxo-integracao.png)



