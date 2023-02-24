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

