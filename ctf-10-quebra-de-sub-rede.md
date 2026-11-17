# CTF 10: Quebra de sub-rede

**Categoria:** Redes  
**Técnicas:** Cálculo de sub-rede /26

## Enunciado

Durante a configuração de um ambiente isolado, o administrador da rede especificou o bloco de endereçamento da sub-rede interna no arquivo net.txt. A missão é calcular o primeiro endereço válido para hosts nessa sub-rede.

## Objetivo

Ler a configuração de rede do arquivo net.txt e calcular o primeiro endereço válido para hosts na sub-rede.

## Resolução

1. Ler o arquivo net.txt com cat e obter o IP 192.168.15.100 e a máscara 255.255.255.192.
2. Converter a máscara para a notação /26 (blocos de 64 endereços).
3. Determinar a sub-rede do IP: rede 192.168.15.64 e broadcast 192.168.15.127.
4. Somar 1 ao endereço de rede para obter o primeiro host válido.

### Comandos utilizados

```bash
file net.txt
# net.txt: Unicode text, UTF-8 text
cat net.txt
# interface: Ethernet0
# ip_address: 192.168.15.100
# subnet_mask: 255.255.255.192
# gateway: 192.168.15.126
# dns: 8.8.8.8
```

### Explicação

A máscara 255.255.255.192 equivale a /26, ou seja, sobram 6 bits para hosts e cada sub-rede possui 64 endereços (blocos de 0, 64, 128 e 192 no último octeto). O endereço 192.168.15.100 está no bloco que vai de 192.168.15.64 (endereço de rede) até 192.168.15.127 (broadcast). Assim, o primeiro endereço válido para hosts é o seguinte ao endereço de rede, e o gateway (192.168.15.126) ocupa o último endereço utilizável.

### Evidência

![CTF 10 – Quebra de sub-rede](../img/ctf-10.png)

---

[↑ Voltar ao índice](../README.md) · [← CTF 9](ctf-09-na-madruga.md) · [CTF 11 →](ctf-11-roteamento-estrategico.md)
