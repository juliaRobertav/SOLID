---
description: Dependency Inversion Principle
---

# DIP

<mark style="color:red;">Dependa de abstrações e não de implementações.</mark>&#x20;



“Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender da abstração.” ​ “Abstrações não devem depender de detalhes. Os detalhes devem depender das abstrações.”



A ideia é que isolemos nossa classe atrás de um limite formado pelas abstrações que dela dependem. Se os detalhes por trás dessas abstrações mudarem, nossa classe ainda continuará segura. Isso ajuda a manter o acoplamento baixo, além de tornar nosso projeto mais fácil de ser alterado, permitindo testar coisas isoladamente.

<figure><img src=".gitbook/assets/pasted image 0 (4).png" alt="" width="250"><figcaption><p>Exemplo Casa</p></figcaption></figure>

```
Exemplos de código
```

* Exemplo Boa Prática:

```java
// Abstração para lâmpada
interface Lampada {
    void ligar();
    void desligar();
}

// Implementação de uma lâmpada
class Luminaria implements Lampada {
    @Override
    public void ligar() {
        System.out.println("Luminária ligada.");
    }

    @Override
    public void desligar() {
        System.out.println("Luminária desligada.");
    }
}

// Classe Interruptor
class Interruptor {
    private Lampada lampada;

    public Interruptor(Lampada lampada) {
        this.lampada = lampada;
    }

    public void ligarLuz() {
        lampada.ligar();
    }

    public void desligarLuz() {
        lampada.desligar();
    }
}

public class Main {
    public static void main(String[] args) {
        Lampada luminaria = new Luminaria();
        Interruptor interruptor = new Interruptor(luminaria);

        interruptor.ligarLuz();
        interruptor.desligarLuz();
    }
}

```

* A classe Interruptor depende da abstração Lampada para controlar a lâmpada. O Princípio da Inversão de Dependência (DIP) é seguido, pois a classe de alto nível (Interruptor) não depende diretamente da classe de baixo nível (Luminaria). Isso torna o código flexível e permite a troca de diferentes implementações de lâmpada sem modificar o Interruptor.



* Exemplo Má Prática:

```java
// Classe para uma lâmpada
class Luminaria {
    public void ligar() {
        System.out.println("Luminária ligada.");
    }

    public void desligar() {
        System.out.println("Luminária desligada.");
    }
}

// Classe Interruptor dependendo diretamente da implementação concreta da lâmpada
class Interruptor {
    private Luminaria luminaria;

    public Interruptor(Luminaria luminaria) {
        this.luminaria = luminaria;
    }

    public void ligarLuz() {
        luminaria.ligar();
    }

    public void desligarLuz() {
        luminaria.desligar();
    }
}

public class Main {
    public static void main(String[] args) {
        Luminaria luminaria = new Luminaria();
        Interruptor interruptor = new Interruptor(luminaria);

        interruptor.ligarLuz();
        interruptor.desligarLuz();
    }
}

```

* Neste exemplo, a classe Interruptor depende diretamente da implementação concreta da lâmpada Luminaria, o que não segue o Princípio da Inversão de Dependência (DIP). Qualquer mudança na implementação da lâmpada pode exigir a modificação da classe Interruptor, tornando o código menos flexível e mais difícil de manter.
