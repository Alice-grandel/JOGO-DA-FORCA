# 🎯 Jogo da Forca em Rust

Um jogo da forca simples feito em Rust rodando no terminal. O objetivo é adivinhar a palavra secreta, letra por letra, com no máximo 3 erros.

---

## 🦀 Tecnologias usadas

- Linguagem: **Rust**
- Conceitos utilizados:
  - `Vec` (vetores)
  - `loop`
  - `funções`
  - `match`
  - `chars()`
  - Entrada e saída com `stdin`
  - Controle de fluxo (`if`, `for`, `break`)
 
# CODIGO:

```
use std::io;

fn main() {
    let palavra_secreta = "banana";
    let mut letras_descobetas = vec!['-'; palavra_secreta.len()];
    let mut tentativas_erradas = 0;
    let mut letras_erradas: Vec<char> = Vec::new();

    loop {
        println!("=== JOGO DA FORCA! ===");

        mostrar_progresso(&letras_descobetas, &letras_erradas, tentativas_erradas);

        let letra = let_letras("Digite uma letra:");

        if palavra_secreta.contains(letra) {
            for (i, c) in palavra_secreta.chars().enumerate() {
                if c == letra {
                    letras_descobetas[i] = letra;
                }
            }
        } else {
            if !letras_erradas.contains(&letra) {
                letras_erradas.push(letra);
                tentativas_erradas += 1;
            }
        }

        if !letras_descobetas.contains(&'-') {
            println!("Parabéns! Você acertou a palavra '{}'.", palavra_secreta);
            break;
        }

        if tentativas_erradas >= 3 {
            println!("Você perdeu! A palavra era '{}'.", palavra_secreta);
            break;
        }

        println!("------------------------------------------------");
    }

    println!("\n=== JOGO ENCERRADO ===");
}

fn let_letras(mensagem: &str) -> char {
    loop {
        println!("{}", mensagem);
        let mut entrada = String::new();
        io::stdin().read_line(&mut entrada).expect("Erro");

        if let Some(c) = entrada.trim().chars().next() {
            return c.to_ascii_lowercase();
        }

        println!("Digite uma letra válida!");
    }
}

fn mostrar_progresso(letras: &Vec<char>, erradas: &Vec<char>, erros: usize) {
    println!("Palavra: {}", letras.iter().collect::<String>());
    println!("Letras erradas: {:?}", erradas);
    println!("Erros: {}", erros);
}

```
