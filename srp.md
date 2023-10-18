---
description: Single Responsibility Principle ​
---

# SRP

<mark style="color:red;">**Princípio da Responsabilidade Única ​**</mark>



Uma classe deve ter um, e somente um, motivo para mudar. ​ Deve ter apenas um objetivo, ou seja, ela deve possuir apenas uma função ou funções similares. Esse princípio não se aplica apenas a classes, mas também a métodos e funções. ​



<figure><img src=".gitbook/assets/pasted image 0.png" alt="" width="250"><figcaption><p>Exemplo Show</p></figcaption></figure>



Em um show, as responsabilidades são compartilhadas com um objetivo, nesse caso, produzir música de qualidade. ​ O princípio da responsabilidade única é justamente esse, fazer com que uma única classe execute funções que tem haver com aquela classe.



```
Exemplos de código
```

* Exemplo de boa prática:

```java
// Classe para representar um usuário
public class Usuario {
    private String nome;
    private String email;
    private String senha;

    public Usuario(String nome, String email, String senha) {
        this.nome = nome;
        this.email = email;
        this.senha = senha;
    }

    public String getNome() {
        return nome;
    }

    public String getEmail() {
        return email;
    }

    public String getSenha() {
        return senha;
    }
}

// Classe para mostrar detalhes do usuário
public class UsuarioDetalhes {
    public void mostrarDetalhes(Usuario usuario) {
        System.out.println("Nome: " + usuario.getNome());
        System.out.println("Email: " + usuario.getEmail());
    }
}

// Classe para validar o usuário
public class UsuarioValidador {
    public boolean validarUsuario(Usuario usuario) {
        // Lógica de validação, por exemplo, verificar se o email é válido
        return usuario.getEmail().contains("@");
    }
}

public class Main {
    public static void main(String[] args) {
        // Cria um novo usuário
        Usuario novoUsuario = new Usuario("Alice", "alice@example.com", "senha123");

        // Exibe os detalhes do usuário usando UsuarioDetalhes
        UsuarioDetalhes usuarioDetalhes = new UsuarioDetalhes();
        usuarioDetalhes.mostrarDetalhes(novoUsuario);

        // Valida o usuário usando UsuarioValidador
        UsuarioValidador usuarioValidador = new UsuarioValidador();
        boolean valido = usuarioValidador.validarUsuario(novoUsuario);

        if (valido) {
            System.out.println("Usuário válido.");
        } else {
            System.out.println("Usuário inválido.");
        }
    }
}

```

* Cada classe tem uma única responsabilidade claramente definida.



* Exemplo de má prática:

```java
public class Usuario {
    private String nome;
    private String email;
    private String senha;

    public Usuario(String nome, String email, String senha) {
        this.nome = nome;
        this.email = email;
        this.senha = senha;
    }

    public String getNome() {
        return nome;
    }

    public String getEmail() {
        return email;
    }

    public String getSenha() {
        return senha;
    }

    public void mostrarDetalhes() {
        System.out.println("Nome: " + nome);
        System.out.println("Email: " + email);
    }

    public boolean validarUsuario() {
        // Lógica de validação, por exemplo, verificar se o email é válido
        return email.contains("@");
    }

    public static void main(String[] args) {
        // Cria um novo usuário
        Usuario novoUsuario = new Usuario("Alice", "alice@example.com", "senha123");

        // Exibe os detalhes do usuário
        novoUsuario.mostrarDetalhes();

        // Valida o usuário
        boolean valido = novoUsuario.validarUsuario();

        if (valido) {
            System.out.println("Usuário válido.");
        } else {
            System.out.println("Usuário inválido.");
        }
    }
}

```

* `A classe Usuario tem mais de uma responsabilidade, caso ocorra um problema com algum método, pode dificultar na manutenção e funcionalidade do código, além de que segundo o SRP, uma classe deve ter apenas uma única razão para mudar.`
