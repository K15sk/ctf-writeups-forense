# CTF 6: Filtragem básica

**Categoria:** Manipulação de texto  
**Técnicas:** awk com regex em /etc/passwd

## Enunciado

O analista deve filtrar usuários de um arquivo passwd que obedeçam aos seguintes critérios: a primeira letra do nome de usuário é uma vogal; a terceira letra é uma consoante; e o shell do usuário é /bin/bash. Flag no formato FIAP{qde}.

## Objetivo

Filtrar o arquivo passwd.txt e contar os usuários cujo nome começa com vogal, tem consoante na terceira letra e utiliza o shell /bin/bash.

## Resolução

1. Verificar o tipo do arquivo com file.
2. Utilizar o awk com separador “:” para analisar os campos de cada linha.
3. Aplicar a condição de shell ($NF == "/bin/bash") e a expressão regular sobre o nome do usuário ($1).
4. Contar os resultados com wc -l.

### Comandos utilizados

```bash
file passwd.txt
# passwd.txt: ASCII text
awk -F: '$NF == "/bin/bash" && \
  $1 ~ /^[aeiouAEIOU].[bcdfghjklmnpqrstvwxyzBCDFGHJKLMNPQRSTVWXYZ]/ \
  {print $1}' passwd.txt | wc -l
# 17
```

### Explicação

O awk foi configurado com o separador “:” (-F:). A condição $NF == "/bin/bash" verifica o último campo (shell); a expressão regular aplicada ao primeiro campo ($1) exige uma vogal na primeira posição, qualquer caractere na segunda e uma consoante na terceira. O comando wc -l contou as linhas que atenderam a todos os critérios.

### Evidência

![CTF 6 – Filtragem básica](../img/ctf-06.png)

---

[↑ Voltar ao índice](../README.md) · [← CTF 5](ctf-05-criacao-de-usuario-suspeita.md) · [CTF 7 →](ctf-07-firewall-auditor.md)
