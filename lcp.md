---
description: Liskov Substitution Principle
---

# LCP

<mark style="color:red;">Princípio da substituição de Liskov — Uma classe derivada deve ser substituível por sua classe base.</mark>



&#x20;"Se S é um subtipo de T, então os objetos do tipo T, em um programa, podem ser substituídos pelos objetos de tipo S sem que seja necessário alterar as propriedades deste programa." ​



Na prática, todas as classes filhas (que foram implementadas através de uma herança) devem manter os mesmos comportamentos da classe pai. Isto é, classes derivadas podem ser substitutas de suas classes base, ou ainda: toda e qualquer classe derivada pode ser usada como se fosse a classe base.



<figure><img src=".gitbook/assets/pasted image 0 (2).png" alt="" width="250"><figcaption><p>Exemplo Pessoa</p></figcaption></figure>

```
Exemplos Código
```

* &#x20;Exemplo Boa Prática:

```java
class Retangulo {
    protected int largura;
    protected int altura;

    public Retangulo(int largura, int altura) {
        this.largura = largura;
        this.altura = altura;
    }

    public int getLargura() {
        return largura;
    }

    public void setLargura(int largura) {
        this.largura = largura;
    }

    public int getAltura() {
        return altura;
    }

    public void setAltura(int altura) {
        this.altura = altura;
    }

    public int area() {
        return largura * altura;
    }
}

class Quadrado extends Retangulo {
    public Quadrado(int lado) {
        super(lado, lado);
    }

    @Override
    public void setLargura(int largura) {
        super.setLargura(largura);
        super.setAltura(largura);
    }

    @Override
    public void setAltura(int altura) {
        super.setAltura(altura);
        super.setLargura(altura);
    }
}

public class Main {
    static void verificarArea(Retangulo retangulo) {
        retangulo.setLargura(3);
        retangulo.setAltura(4);

        if (retangulo.area() == 12) {
            System.out.println("Área verificada com sucesso.");
        } else {
            System.out.println("Houve um problema na verificação da área.");
        }
    }

    public static void main(String[] args) {
        Retangulo retangulo = new Retangulo(2, 5);
        Quadrado quadrado = new Quadrado(3);

        verificarArea(retangulo);
        verificarArea(quadrado); // Funciona para Quadrado devido ao LSP
    }
}

```

* Temos uma classe base Retangulo e uma classe derivada Quadrado. A classe Quadrado é uma especialização de Retangulo, onde a largura e a altura são sempre iguais para garantir que seja um quadrado. O método verificarArea funciona para ambas as classes. Isso significa que podemos substituir um objeto Retangulo por um objeto Quadrado sem afetar a corretude do programa.



* Exemplo Má Prática:

```java
class Retangulo {
    protected int largura;
    protected int altura;

    public Retangulo(int largura, int altura) {
        this.largura = largura;
        this.altura = altura;
    }

    public int getLargura() {
        return largura;
    }

    public void setLargura(int largura) {
        this.largura = largura;
    }

    public int getAltura() {
        return altura;
    }

    public void setAltura(int altura) {
        this.altura = altura;
    }

    public int area() {
        return largura * altura;
    }
}

class Quadrado extends Retangulo {
    public Quadrado(int lado) {
        super(lado, lado);
    }

    @Override
    public void setLargura(int largura) {
        super.setLargura(largura);
        super.setAltura(largura);
    }

    @Override
    public void setAltura(int altura) {
        super.setAltura(altura);
        super.setLargura(altura);
    }
}

public class Main {
    static void verificarArea(Retangulo retangulo) {
        retangulo.setLargura(3);
        retangulo.setAltura(4);

        if (retangulo.area() == 12) {
            System.out.println("Área verificada com sucesso.");
        } else {
            System.out.println("Houve um problema na verificação da área.");
        }
    }

    public static void main(String[] args) {
        Retangulo retangulo = new Quadrado(3); // Substituição de Liskov que não funciona
        verificarArea(retangulo);
    }
}

```

* A classe Quadrado herda da classe Retangulo, mas a implementação dos métodos setLargura e setAltura em Quadrado não está de acordo com o princípio. Já que não podemos substituir um objeto Retangulo por um objeto Quadrado sem afetar a corretude do programa.
