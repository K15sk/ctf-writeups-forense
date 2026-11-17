# CTF 9: Na madruga

**Categoria:** Forense Linux  
**Técnicas:** Análise de auth.log (SSH)

## Enunciado

Suspeita-se que um atacante tenha tentado acessar um servidor Linux entre 03:00 e 04:00 de 22 de abril de 2025. A partir do arquivo auth.log, a missão é identificar o primeiro endereço IP que tentou, sem sucesso, autenticar-se no servidor entre 03:00:00 e 03:59:59. Flag no formato FIAP{ip}.

## Objetivo

Analisar o arquivo auth.log e identificar o primeiro IP com tentativa de autenticação falha entre 03:00:00 e 03:59:59 de 22/04/2025.

## Resolução

1. Verificar o tipo do arquivo com file e ler o log com cat.
2. Filtrar as linhas do intervalo das 03h do dia 22 de abril.
3. Desconsiderar os eventos “Accepted password” e manter apenas os “Failed password”.
4. Ordenar pelo horário e selecionar o primeiro registro (03:40:07, IP 10.0.0.190).

### Comandos utilizados

```bash
file auth.log
# auth.log: ASCII text
cat auth.log

# filtragem equivalente:
grep "^Apr 22 03:" auth.log | grep "Failed password" | sort -k3 | head -n 1
# Apr 22 03:40:07 server sshd[2679]: Failed password for user1
#   from 10.0.0.190 port 49265 ssh2
```

### Explicação

O log não está em ordem cronológica, por isso é necessário filtrar o intervalo de horário e o tipo de evento. Entre as linhas do período das 03h, o registro das 03:43:00 corresponde a uma autenticação aceita (Accepted password) e, portanto, não atende ao critério. A primeira falha (Failed password) no intervalo ocorreu às 03:40:07, para o usuário user1, a partir do IP 10.0.0.190.

### Evidência

![CTF 9 – Na madruga](../img/ctf-09.png)

---

[↑ Voltar ao índice](../README.md) · [← CTF 8](ctf-08-vigilancia-administrativa.md) · [CTF 10 →](ctf-10-quebra-de-sub-rede.md)
