---
description: Open-Closed Principle ​
---

# OCP

<mark style="color:red;">Objetos ou entidades devem estar abertos para extensão, mas fechados para modificação</mark>, ou seja, outras classes podem ter acesso ao que aquela classe possui, porém, não podem alterá-las. ​ ​



**“Aberto para extensão” diz que você deve projetar suas classes para que novas funcionalidades possam ser adicionadas à medida que novos requisitos são gerados. “**



**“Fechado para modificação” significa que uma vez que uma classe tenha sido desenvolvida ela nunca deve ser modificada, exceto para corrigir bugs e demais problemas no código.**



A ideia aqui não é não mexer na classe em hipótese alguma, e sim, caso necessário, adicionar uma nova função àquela classe e não alterar o que já existe nela.

<figure><img src=".gitbook/assets/pasted image 0 (1).png" alt="" width="250"><figcaption><p>Exemplo Cozinha</p></figcaption></figure>

```
Exemplos em Código
```

* Exemplo Boa Prática:

```java
// Interface para métodos de pagamento
interface MetodoPagamento {
    void realizarPagamento(double valor);
}

// Implementação do pagamento com cartão de crédito
class CartaoCreditoPagamento implements MetodoPagamento {
    @Override
    public void realizarPagamento(double valor) {
        System.out.println("Pagamento com cartão de crédito no valor de $" + valor);
        // Lógica para processar o pagamento com cartão de crédito
    }
}

// Implementação do pagamento com PayPal
class PayPalPagamento implements MetodoPagamento {
    @Override
    public void realizarPagamento(double valor) {
        System.out.println("Pagamento com PayPal no valor de $" + valor);
        // Lógica para processar o pagamento com PayPal
    }
}

// Classe Pagamento, aberta para extensão
class Pagamento {
    private MetodoPagamento metodoPagamento;

    public void setMetodoPagamento(MetodoPagamento metodoPagamento) {
        this.metodoPagamento = metodoPagamento;
    }

    public void processarPagamento(double valor) {
        metodoPagamento.realizarPagamento(valor);
    }
}

public class Main {
    public static void main(String[] args) {
        Pagamento pagamento = new Pagamento();

        // Realizar pagamento com cartão de crédito
        MetodoPagamento cartaoCredito = new CartaoCreditoPagamento();
        pagamento.setMetodoPagamento(cartaoCredito);
        pagamento.processarPagamento(100.00);

        // Realizar pagamento com PayPal
        MetodoPagamento paypal = new PayPalPagamento();
        pagamento.setMetodoPagamento(paypal);
        pagamento.processarPagamento(50.00);
    }
}

```

* A classe Pagamento é aberta para extensão, pois você pode criar novas implementações de MetodoPagamento sem modificar o código-fonte da classe Pagamento existente. Utilizando o princípio OCP, onde a classe Pagamento é fechada para modificação e aberta para extensão.



* Exemplo Má Prática:

```java
// Classe Pagamento que não segue o OCP
class Pagamento {
    public void realizarPagamentoCartaoCredito(double valor) {
        System.out.println("Pagamento com cartão de crédito no valor de $" + valor);
        // Lógica para processar o pagamento com cartão de crédito
    }

    public void realizarPagamentoPayPal(double valor) {
        System.out.println("Pagamento com PayPal no valor de $" + valor);
        // Lógica para processar o pagamento com PayPal
    }
}

public class Main {
    public static void main(String[] args) {
        Pagamento pagamento = new Pagamento();

        // Realizar pagamento com cartão de crédito
        pagamento.realizarPagamentoCartaoCredito(100.00);

        // Realizar pagamento com PayPal
        pagamento.realizarPagamentoPayPal(50.00);
    }
}

```

* A classe Pagamento possui métodos específicos para cada forma de pagamento, como realizarPagamentoCartaoCredito e realizarPagamentoPayPal. Se precisar adicionar um novo método de pagamento, seria necessário modificar a classe Pagamento, o que não segue o OCP, já que ela não está fechada para modificação.
