# IoC, Injeção de Dependências, Componentes e Bean

### Componentes e Sistema:

Todos os sistemas são compostos por vários componentes, incluindo um sistema de um carro, navio, avião, software… É importante que os componentes de um sistema sejam projetados de forma independente, permitindo que cada um seja corrigido ou atualizado sem afetar os outros. Um sistema com componentes altamente acoplados pode tornar a manutenção mais complexa e custosa, pois a alteração em um componente pode exigir modificações em vários outros.

### Inversão de Controle:

Inversão de controle é um conceito onde, ao invés de declarativamente você executar uma ação ou algum trecho de código, um framework ou algum outro método, ou algum container, ou alguma outra classe executa essa ação por você.

É como ter um cozinheiro mestre que fornece os ingredientes já preparados para que o programador possa se concentrar na tarefa principal, sem se preocupar com os detalhes de como obter e combinar os ingredientes corretos. Isso ajuda a simplificar o desenvolvimento e a manutenção do software.

Agora veremos uma técnica que usa inversão de controle, chamada injeção de dependências:

- [Injeção de dependências no Java Puro](./ioc/java-puro.md)
- [@Autowired](./ioc/autowired.md)
- [Injeção de dependências com Construtor](./ioc/construtor.md)
- [@Autowired em cada atributo vs @Autowired com Construtor](./ioc/autowired-vs-construtor.md)
