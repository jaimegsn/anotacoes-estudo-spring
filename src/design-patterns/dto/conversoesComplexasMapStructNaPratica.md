# Conversões Complexas com MapStruct na Prática

Utilizamos a anotação **`@Mapping`** no método do Mapper que está realizando a conversão, essa annotation permite que você especifique como campos específicos devem ser mapeados, permitindo um maior controle sobre como ocorre a conversão. Aqui estão os principais atributos da anotação **`@Mapping`**:

- **`target`**: Especifica o campo/atributo na classe de destino que você deseja mapear. Este é o campo que receberá o valor após a conversão.
- **`source`**: Especifica o campo/atributo correspondente na classe de origem que fornecerá o valor a ser mapeado.
- **`dateFormat`**: Este atributo é usado principalmente para formatar campos de data e hora durante a conversão. Quando você precisa converter tipos de dados de data e hora, como **`LocalDateTime`**, para **`String`** (ou vice-versa), o atributo **`dateFormat`** especifica o formato no qual a conversão deve ocorrer.
- **`numberFormat`**: Especifica o formato numérico para campos numéricos durante a conversão.
- **`qualifiedByName`**: Permite que você especifique um método que será usado para realizar o mapeamento.
- **`ignore`**: Indica que o campo deve ser ignorado durante o mapeamento.
- **`defaultValue`**: Permite definir um valor padrão para o campo de destino caso o campo de origem seja nulo.
- **`expression`**: Permite definir uma expressão que será usado para realizar o mapeamento, é como se o **`expression`** fosse uma linha de código Java, onde você pode realizar operações, cálculos, concatenações e outras lógicas diretamente no mapeamento. E também pode chamar métodos com ele.

Cada **`@Mapping`** serve para um campo do objeto específico, então podemos utilizar a annotation **`@Mappings`** para englobar vários **`@Mapping`**, veremos aqui um exemplo aplicando tudo isso que vimos:

```java
@Mapper(componentModel = "spring")
public interface MyMapper {
    MyMapper INSTANCE = Mappers.getMapper(MyMapper.class);

    @Mappings({
        @Mapping(target = "destinationField", source = "sourceField"),
        @Mapping(target = "concatenatedField",
					expression = "java(source.getsourceField() + \" concatenated\")"),
        @Mapping(target = "formattedNumber", numberFormat = "#,##0.00", source = "sourceNumber")
    })
    Destination sourceToDestination(Source source);
}
```
