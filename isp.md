---
description: Interface Segregation Principle
---

# ISP

<mark style="color:red;">Princípio da Segregação da Interface — Uma classe não deve ser forçada a implementar interfaces e métodos que não irão utilizar. ​</mark>



Esse princípio basicamente diz que é melhor criar interfaces mais específicas ao invés de termos uma única interface genérica.



Quando você aplica o princípio de herança, fazendo uma classe herdar da outra, sua classe filha é obrigada a implementar os métodos da classe pai e como você já deve estar imaginando, isso vai contra os princípios do SOLID, pois não é nada interessante que uma classe implementa métodos que não é útil para ela. Com o princípio de segregação de interface, é possível implementar somente o que importa para as nossas classes. ​

<figure><img src=".gitbook/assets/pasted image 0 (3).png" alt="" width="250"><figcaption><p>Exemplo Farmácia</p></figcaption></figure>

```
Exemplos de Código
```

* Exemplo Boa Prática:

```java
// Interfaces segregadas para dispositivos eletrônicos
interface LigarDesligar {
    void ligar();
    void desligar();
}

interface Recarregavel {
    void carregar();
    void descarregar();
}

// Implementação para um smartphone
class Smartphone implements LigarDesligar, Recarregavel {
    @Override
    public void ligar() {
        // Lógica para ligar o smartphone
    }

    @Override
    public void desligar() {
        // Lógica para desligar o smartphone
    }

    @Override
    public void carregar() {
        // Lógica para carregar o smartphone
    }

    @Override
    public void descarregar() {
        // Lógica para descarregar o smartphone
    }
}

public class Main {
    public static void main(String[] args) {
        Smartphone smartphone = new Smartphone();
        smartphone.ligar();
        smartphone.carregar();
    }
}
vav
```

* As interfaces foram segregadas em LigarDesligar e Recarregavel, tornando a implementação mais flexível e seguindo o ISP. Cada classe pode implementar apenas as interfaces relevantes para suas necessidades, evitando a implementação de métodos não utilizados. Isso torna o código mais claro e mais adaptável a mudanças futuras.



* Exemplo Má Prática:

```java
// Interface geral para dispositivos eletrônicos
interface DispositivoEletronico {
    void ligar();
    void desligar();
    void carregar();
    void descarregar();
}

// Implementação para um smartphone
class Smartphone implements DispositivoEletronico {
    @Override
    public void ligar() {
        // Lógica para ligar o smartphone
    }

    @Override
    public void desligar() {
        // Lógica para desligar o smartphone
    }

    @Override
    public void carregar() {
        // Lógica para carregar o smartphone
    }

    @Override
    public void descarregar() {
        // Lógica para descarregar o smartphone
    }
}

public class Main {
    public static void main(String[] args) {
        Smartphone smartphone = new Smartphone();
        smartphone.ligar();
        smartphone.carregar();
    }
}

```

* Neste exemplo, a interface DispositivoEletronico contém métodos que são irrelevantes para um Smartphone, como carregar e descarregar. Isso força a classe Smartphone a implementar métodos que não fazem sentido para ele, violando o ISP.
