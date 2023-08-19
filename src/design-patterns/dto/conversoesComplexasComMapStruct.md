# Conversões Complexas com MapStruct

Existem certos tipos de dados que são complexos de se converter, então o MapStruct oferece uma flexibilidade para personalizar a conversão, alguns exemplos complexos de conversão:

- **Conversão de Enumeradores (Enums) Personalizados em códigos numéricos**: Enums personalizados podem ter valores ou lógicas associadas que requerem mapeamento especial para determinados valores. Por exemplo, converter um enum para um código numérico específico associado a ele.
- **Conversões com Cálculos no Campo**: Quando você precisa realizar cálculos complexos durante a conversão, como converter unidades de medida ou calcular um campo derivado com base em outros campos.
- **Personalizações de Formatação**: Além das datas, outros campos podem precisar de formatação específica, como números decimais com um número específico de casas decimais. Ou seja em dados cujo existem diversas formas de representa-lo é necessário definir um padrão de formatação a ser seguido pelo conversor.

E outros diversos casos…

### Importância de Testes Automatizados no Mapper

Caso não haja nenhuma personalização na conversão desses casos, os dados podem ficar errados ou nulos.  É ai que está a importância de realizar testes automatizados no Mapper, para saber se a conversão está se saindo corretamente como esperado.

Ainda mais porque como o MapStruct se utiliza de métodos abstratos não têm como prever seu comportamento.