# Injeção de dependências no Java Puro

Utilizando Java puro temos esse exemplo aqui bastante acoplado e sem injeção de dependências aonde os objetos são iniciados nos atributos de uma classe:

```java
public class Zoologico {
	private Animal animal1 = new Zebra();
	private Animal animal2 = new Cavalo();
}
```

Esse é uma má prática pois qualquer alteração na classe Zebra ou Cavalo terá um impacto direto na classe Zoológico.

Agora aplicando injeção de dependências no construtor delegamos para outra classe a responsabilidade de instanciar esses objetos das quais a classe Zoológico depende:

```java
public class Zoologico {
	private Animal animal1;
	private Animal animal2;
	
	public Zoologico(Animal animal1, Animal animal2){
		this.animal1 = animal1;
		this.animal2 = animal2;
	}
}
```

Essa pequena mudança permite que façamos manutenções de forma mais simples na classe Zoológico, já com o forte acoplamento do primeiro exemplo poderíamos ter que fazer alterações também na classe Zebra e na classe Cavalo dependendo da situação e da manutenção.

O ponto é que com forte acoplamento as três classes teriam impacto direto umas nas outras, onde dependendo da situação teríamos que realizar manutenção nas três classes, por mais que a intenção fosse realizar em apenas uma.