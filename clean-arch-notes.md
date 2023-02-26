# Clean Arch
Main idea:
Purpose:
Main train of thoughts:

## Part X

### Chapter X

#### Topic Y

## Parte 4 - Princípios dos componentes

[*] Se os princípios SOLID orientam a organização dos tijolos em paredes e salas, os princípios dos compoentes determinam como organizar as salas em prédios. Sistemas de softwares grandes, como prédios, são constrídos a partir de componentes menores.

### Chapter 12 - Componentes

[**] Componentes são unidades de implantação. Eles são as menores entidades que podem ser implantadas como parte de um sistema. Em linguages compiladas, são agregações de arquivos binários. Em linguages interpretadas, são agregações de código-fonte. Em todas as linguagens, são o o grânulo da implantação.

[*] Componentes bem projetados sempre detém a capacidade de serem implantados de forma independente, e portanto, desenvolvidos independentemente. 

#### A história dos componentes

[*] Programas não relocáveis -> relocalização -> ligadores -> velocidade.
    [?] Existem vários termos que não me são familiares. Buscar terminar o Nand2tetris para entender melhor sobre compilação, ligação e relocalização.

[*] Os arquivos dinamicamente ligados, que podem ser reunidos na hora da execução, são os componentes do software das nossas arquiteturas. Demorou, mas chegamos à um ponto em que a arquitetura de plugin de componente pode ser aplicada como o padrão típico, ao contrário do esforço hercúlo que foi no passado.

### Chapter 13 - Coesão de componentes

[*] Quais classes pertencem a quais componentes? Decisão importante que requer a orientação de bons princípios de engenharia. Infelizmente, ao longo dos anos, essa decisão tem sido tomada caso a caso, quase inteiramente com base no contexto. 
    [!] Com certeza, jamais tinha ouvido falar nesses princípios e acredito que a quantidade de pessoas que os conhece é bem pequena.
    [->] Idéia de post sobre componentes aplicados à iOS.
[**] Três princípios de Coesão de Componentes:
    - REP: Princípio da Equivalência de Reuso/Release (Reuse/Release Equivalence Principle)
    - CCP: Princípio do Fechamento Comum (Common Closure Principle)
    - CRP: Princípio do Reuso Comum (Common Reuse Principle)

#### O princípio da Equivalência de Reuse/Release
> Granularidade de Reuse é a granularidade de Release.

As pessoas que querem reutilizar compoenntes de software não podem, e não devem, fazê-lo a não ser que esses compoenentes sejam rastreados por meio de um processo de release e recebam números de release. 

Isso não é só porque, sem números de release, seria impossível garantir que todos os componentes reutilizados sejam compatíveis uns com os outros. Mas também pois programadores precisam saber quando chegaram os novos releases e quais mudanças trouxeram. 

[*] O processo de release deve produzir as notificações e documentos de release para que os usuários tomem decisões informadas sobre o momento e a viabilidade de usar o novo release. 
    [->] How to generate automatic documentation and Changelog conventions for software development. 
[*] Do ponto de vista de design e arquitetura de software, esse princípio significa que as classes e módulos formados em um componente devem pertencer a um grupo coeso. O componente não pode simplesmente consistir de uma mistura aleatória de classes e módulos, mas deve haver algum tema ou propósito abrangente que todos esses módulos compartilhem. Outra forma de olhar esse princípio é que classes e módulos agrupados em um componente devem ser passíveis de release em conjunto. O fato de compartilahrem o mesmo número de versão e o mesmo rastreamento de release e de estarem incluídos na mesma documentação de release deve fazer sentido tanto para o autor quanto para os usuários.

#### O princípio do Fechamento Comum (Common Closure Priciple)
> Reuna nos mesmos componentes classes que mudam pelas mesmas razões e ao mesmo momento. Separe em componentes diferentes classes que mudam em momentos diferentes e por razões diferentes.

[!] SRP aplicado no nível de componente. Assim como uma classe não deve ter várias razões para mudar, um componente também não.

[**] Na maioria das aplicações a manutenção é mais importante do que reutilização. Quando o código de uma aplicação tem que mudar, é preferível que todas as mudanács ocorram em um componente em vez de serem distribuídas por vários componentes. 

#### O princípio do Reuso Comum (Common Reuse Principle)
> Não forçe os usuários de um componente a dependerem de coisas que eles não precisam.

[*] quando dependemos de um componente, devemos ter certeza de que dependemos de todas as classes desse componente. Em outras palavras, devemos ter certeza de que as classes que colocamos em um componente são inseparáveis — que é impossível depender de umas e não de outras. Caso contrário, teremos que reimplantar mais componentes do que o necessário e desperdiçar horas importantes de trabalho.

o CRP nos diz mais sobre as classes que não devem ficar juntas do que sobre as classes que devem ficar juntas. Segundo o CRP, as classes que não têm uma forte ligação entre si não devem ficar no mesmo componente.

O CRP é uma versão genérica do ISP. O ISP aconselha a não depender de classes que contenham métodos que não usamos. Já o CRP orienta a não depender de componentes que tenham classes que não usamos.

> Não dependa do que você não precisa

#### O diagrama de tensão para Coesão de Componentes

[!] Quando um arquiteto se concentra apenas no REP e no CRP, descobre que muitos componentes são impactados quando mudanças simples são feitas. Por outro lado, um arquiteto que foca demais em CCP e REP fará com que muitos releases desnecessárias sejam geradas.

[*] Geralmente, os projetos tendem a começar do lado direito do triângulo, onde o único sacrifício é o reúso. À medida que amadurece e que outros projetos começam a ser desenvolvidos a partir dele, o projeto passará para o lado esquerdo. Isso significa que a estrutura de componentes de um projeto pode variar com o tempo e a maturidade. Ela está mais relacionada ao modo de desenvolvimento e uso do projeto do que com a sua função real.

### Capítulo 14 - Acoplamento de componentes

#### Princípio das dependências acíclicas (ADP)
> Não permita ciclos no grafo de dependência dos componentes

##### O build semanal
[!] O build semanal costumava ser comum em projetos de médio porte. Ele funciona assim: todos os desenvolvedores ignoram uns aos outros nos primeiros quatro dias da semana. Todos trabalham em cópias privadas do código e não se preocupam em integrar seus trabalhos de maneira coletiva. Então, na sexta-feira, eles integram todas as mudanças e fazem o build do sistema.
			
Essa abordagem tem a vantagem maravilhosa de permitir que os desenvolvedores vivam em um mundo isolado durante quatro dos cinco dias de trabalho. Evidentemente, a desvantagem consiste no grande ônus de integração a ser pago na sexta-feira.

À medida que o ciclo de desenvolvimento versus integração diminui, a eficiência da equipe também diminui. No fim, essa situação se torna tão frustrante que os desenvolvedores, ou os gestores de projetos, declaram que o cronograma deve ser alterado para uma implementação quinzenal. Isso é suficiente por um tempo, mas o tempo de integração cresce com o tamanho do projeto.

Fica cada vez mais difícil realizar a integração e os testes, e a equipe perde a vantagem do feedback rápido.

##### Eliminando os ciclos
[**] A solução para este problema é particionar o ambiente de desenvolvimento em componentes passíveis de release. Os componentes se tornam unidades de trabalho que podem ser da responsabilidade de um único desenvolvedor ou de uma equipe de desenvolvedores. Quando fazem um componente funcionar, os desenvolvedores fazem o release dele para uso pelos demais desenvolvedores. Eles atribuem um número de release e movem o componente para um diretório a fim de que outras equipes o utilizem.

À medida que novos releases de um componente ficam disponíveis, outras equipes podem decidir se adotarão imediatamente o novo release. Se decidirem não fazê-lo, continuarão a usar o antigo. Caso decidam que estão prontos, começarão a usar o novo. Assim, nenhuma equipe fica à mercê da outra.

Para que funcione com sucesso, no entanto, você deve gerenciar a estrutura de dependência dos componentes. Não pode haver ciclos. Se houver ciclos na estrutura de dependência, a "síndrome da manhã seguinte" não poderá ser evitada.

##### O efeito do ciclo sobre o grafo de dependência.

Esse ciclo cria alguns problemas imediatos. Por exemplo, os desenvolvedores que trabalham no componente Database sabem que, para liberá-lo, o componente deve ser compatível com Entities. Contudo, com o ciclo estabelecido, o componente Database agora também deve ser compatível com Authorizer. Mas Authorizer depende de Interactors. Isso dificulta muito mais a liberação de Database. Entities, Authorizer e Interactors se tornaram, na verdade, um grande componente

Considere o que acontece quando queremos testar o componente Entities. Para nossa decepção, descobrimos que devemos fazer o build do componente e integrá-lo com Authorizer e Interactors. Esse nível de acoplamento entre componentes é preocupante, até mesmo intolerável.

##### Quebrando o ciclo

Sempre é possível quebrar o ciclo de componentes e restabelecer o grafo de dependências como um DAG. Há dois mecanismos primários para isso:
			
1. Aplique o Princípio da Inversão de Dependência (DIP). No caso da Figura 14.3, podemos criar uma interface com os métodos de que a classe User precisa. Em seguida, podemos colocar essa interface em Entities e herdá-la em Authorizer. Isso inverte a dependência entre Entities e Authorizer e, portanto, quebra o ciclo.

2. Crie um novo componente do qual tanto Entities quanto Authorizer dependam. Mova a(s) classe(s) das quais ambos dependem para esse novo componente
    - Composability?

#### Top-Down Design
Os problemas que discutimos até agora levam a uma conclusão inescapável: a estrutura de componentes não pode ser projetada de cima para baixo. Ela não é uma da primeiras coisas a serem projetadas no sistema, mas evolui à medida que o sistema cresce e muda.

Quando vemos um agrupamento de alta granularidade como uma estrutura de dependências de componentes, acreditamos que os componentes devem, de alguma forma, representar as funções do sistema. Ainda assim, isso não parece ser um atributo de diagramas de dependência de componentes.
			
[**] Na verdade, os diagramas de dependência de componentes têm pouco a ver com descrever a função da aplicação. Na verdade, eles são um mapa para a facilidade de se fazer o build e a manutenção da aplicação. É por isso que não são projetados no início do projeto.

[**] Nessa estrutura de dependências, uma das principais preocupações é com o isolamento da volatilidade. Não queremos que os componentes que mudam frequentemente e por motivos fúteis afetem componentes que, em regra, devem ser estáveis.

Consequentemente, o grafo de dependências de componentes é criado e moldado pelos arquitetos de modo a proteger os componentes estáveis e de alto valor dos componentes voláteis.

[*] Se tentássemos projetar a estrutura de dependência de componentes antes de projetar qualquer classe, provavelmente fracassaríamos feio. Não saberíamos muito sobre o fechamento comum, estaríamos alheios a qualquer elemento reutilizável e quase certamente criaríamos componentes que produziriam ciclos de dependência. Portanto, a estrutura de dependências de componentes deve crescer e evoluir de acordo com o design lógico do sistema.

#### O Princípio das Dependências Estáveis.(SDP)
 > Dependa na direção da estabilidade.

[**] Um componente que seja difícil de mudar não deve ser dependente de qualquer componente que esperamos que seja volátil. Caso contrário, o componente volátil também será difícil de mudar.

É uma perversidade do software que um módulo que você projetou para ser fácil de mudar seja transformado em algo difícil de mudar devido à simples inclusão de uma dependência por outra pessoa. Ao aplicarmos o Princípio das Dependências Estáveis (SDP), garantimos que os módulos difíceis de mudar não sejam dependentes de módulos projetados para serem fáceis de mudar.

##### Estabilidade
[!] a estabilidade não está diretamente relacionada com a frequência da mudança.

O Dicionário Webster define estável como a propriedade de algo que "não é facilmente movido". A estabilidade está relacionada com a quantidade de trabalho necessária para fazer uma mudança.

[*] Uma maneira segura de tornar um componente de software difícil de mudar é fazer com que vários componentes de software dependam dele. Um componente do qual muitos dependam é muito estável porque requer muito trabalho para reconciliar eventuais mudanças com todos os componentes dependentes.

[to-do] translate into definitions:
Nesse caso, dizemos que X é responsável por esses três componentes. Por outro lado, como X não depende de nada, não têm influências externas para fazê-lo mudar. Logo, dizemos que ele é independente.

Como nenhum outro componente depende de Y, dizemos que ele é irresponsável. Além disso, Y depende de três componentes, logo, as mudanças podem vir de três fontes externas. Nesse caso, dizemos que Y é dependente.

##### Métricas de Estabilidade
[***] Como podemos medir a estabilidade de um componente? Uma maneira é contar o número de dependências que entram e saem desse componente. Essas contagens nos permitirão calcular a estabilidade posicional do componente.
			
    Fan-in: Dependências que chegam. Essa métrica identifica o número de classes fora desse componente que dependem das classes contidas dele.
    Fan-out: Dependências que saem. Essa métrica identifica o número de classes contidas nesse componente que dependem de classes fora dele.
    I: Instabilidade: I = Fan-out , (Fan-in + Fan-out). Essa métrica tem a variação [0, 1]. I = 0 indica um componente com estabilidade máxima. I = 1 indica um componente com instabilidade máxima.

[!] De fato, a métrica I é mais fácil de calcular quando você organizou seu código-fonte de modo que haja uma classe em cada arquivo-fonte.

[**] Quando a métrica I é igual a 1, nenhum outro componente depende desse componente (Fan-in = 0) e esse componente depende de outros componentes (Fan-out 7 0). Para um componente, essa situação é a mais instável que se pode imaginar, pois aqui ele é irresponsável e dependente. A ausência de dependentes não dá ao componente nenhuma razão para não mudar, e o componente do qual depende pode oferecer a ele várias razões para mudar.
			
Em contrapartida, quando a métrica I é igual a 0, há outros componentes que dependem deste componente (Fan-in 7 0), mas ele não depende de outros componentes (Fan-out = 0). Esse componente é responsável e independente, ou seja, o mais estável possível. Seus dependentes dificultam a mudança do componente, que não tem dependências para forçá-lo a mudar.

[***] O SDP diz que a métrica I de um componente deve ser maior do que a métrica I dos componentes dos quais ele depende. Ou seja, as métricas I devem diminuir na direção da dependência.
    [to-do] Research if any proof can be drawn about retain cycles.

##### Nem todos os componentes devem ser estáveis

Se todos os componentes de um sistema tivessem estabilidade máxima, o sistema seria imutável. Essa não é uma situação desejável.

[**] Os componentes mutáveis estão no topo e dependem do componente estável abaixo. Colocar os componentes instáveis no topo do diagrama é uma convenção útil porque qualquer flecha que aponte para cima estará violando o SDP (e, como veremos mais adiante, o ADP).

#### O Princípio das Abstrações Estáveis.(SAP)

## References


## Symbols
[***] - Very, very special thought. Should exist very few of these.
[**] - Very special thoughts.
[*] - good train of thoughts
[!] - Attention point on something important, but not such much as above asteriscs
[?] - Questions about what's written.
[to-do] - Action item based on authors proposition
[->] - Could result in project idea (code, post, research)
[r] - Reference made by me to another content
[sz] - Sumarization of previous topics, on my words. 


