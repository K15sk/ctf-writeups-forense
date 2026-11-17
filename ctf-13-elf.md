# CTF 13: ELF

**Categoria:** Decodificação  
**Técnicas:** Script oculto em hex + Base64

## Enunciado

Durante uma investigação em um servidor Linux comprometido, foi encontrado um arquivo oculto aparentemente inofensivo que, após execução, revela uma mensagem que pode indicar o próximo passo da investigação. Pergunta: qual mensagem aparece ao executar o script?

## Objetivo

Interpretar e decodificar o script oculto no arquivo file para descobrir a mensagem exibida ao executá-lo.

## Resolução

1. Verificar o tipo do arquivo com file.
2. Converter o conteúdo hexadecimal em texto com xxd -r -p, revelando um script Bash.
3. Identificar a string Base64 que o script decodifica e imprime.
4. Decodificar a string exata do script com base64 -d.

### Comandos utilizados

```bash
file file
# file: ASCII text
cat file | xxd -r -p

#!/bin/bash
x=$(echo "YWNjZXNzbyNjb25jZWRpZG8=" | base64 -d)
echo "$x"

echo "YWNjZXNzbyNjb25jZWRpZG8=" | base64 -d
# accesso#concedido
```

### Explicação

Assim como no desafio 2, o arquivo continha um script Bash em hexadecimal, recuperado com xxd -r -p. O script apenas decodifica uma string Base64 e imprime o resultado. A decodificação da string YWNjZXNzbyNjb25jZWRpZG8= com base64 -d revelou a mensagem “accesso#concedido”.

### Evidência

![CTF 13 – ELF](../img/ctf-13.png)

---

[↑ Voltar ao índice](../README.md) · [← CTF 12](ctf-12-tool.md) · [CTF 14 →](ctf-14-filtragem-obscura.md)
