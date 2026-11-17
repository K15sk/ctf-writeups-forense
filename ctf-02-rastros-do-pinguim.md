# CTF 2: Rastros do pinguim

**Categoria:** Decodificação  
**Técnicas:** Hexadecimal (xxd), substring em Bash, Base64

## Enunciado

Durante a análise de uma estação Linux comprometida, foi encontrado um arquivo nomeado code. Informações iniciais indicam que, ao ser interpretado corretamente, ele pode fornecer a flag necessária para a investigação. A missão é interpretar o conteúdo e reconstruir o que for necessário para obtenção da flag. Pergunta: qual é a flag?

## Objetivo

Interpretar o arquivo code, recuperar o script que ele contém e reconstruir a string codificada para obter a flag.

## Resolução

1. Verificar o tipo do arquivo com file (texto ASCII em hexadecimal).
2. Converter o hexadecimal em texto com xxd -r -p, revelando um script Bash.
3. Interpretar as expansões de substring do script, que removem o ruído “XX” e “YY” e montam a string Base64.
4. Decodificar a string RklBUFtiYXNofQ== com base64 -d para obter a flag.

### Comandos utilizados

```bash
cd ~/Documents/
file code
# code: ASCII text
cat code | xxd -r -p

#!/bin/bash
a="XXRklBUFtiYXNofQ==YY"
b=${a:2:4}     # RklB
c=${a:6:5}     # UFtiY
d=${a:11:5}    # XNofQ
e=${a:16:2}    # ==
full="$b$c$d$e"
echo "$full" | base64 -d

echo "RklBUFtiYXNofQ==" | base64 -d
```

### Explicação

O conteúdo de code estava em hexadecimal. O comando xxd -r -p converteu o texto de volta para bytes, revelando um script Bash. O script recorta trechos da variável a por meio de expansão de substring (${variável:início:tamanho}), descartando os caracteres de ruído “XX” e “YY”, e concatena as partes na string Base64 RklBUFtiYXNofQ==. A decodificação dessa string com base64 -d revelou a flag.

### Evidência

![CTF 2 – Rastros do pinguim](../img/ctf-02.png)

---

[↑ Voltar ao índice](../README.md) · [← CTF 1](ctf-01-barreiras-invisiveis.md) · [CTF 3 →](ctf-03-palavra-escondida.md)
