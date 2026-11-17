# CTF 1: Barreiras invisíveis

**Categoria:** Análise de malware / Firewall  
**Técnicas:** iptables, leitura de script de persistência

## Enunciado

Durante a análise de uma imagem de firewall (fw), foi identificado que alterações manuais foram feitas para bloquear a comunicação de saída em portas específicas. Um script suspeito (install.sh) foi encontrado entre os arquivos do sistema. A missão é localizar e interpretar a configuração de bloqueio aplicada. Pergunta: qual é a porta que foi bloqueada pelo script de firewall?

## Objetivo

Analisar a imagem de firewall fornecida, localizar o script suspeito install.sh e interpretar a regra de bloqueio de saída que ele aplica, a fim de identificar a porta bloqueada.

## Resolução

1. Identificar o tipo do artefato fw com o comando file (arquivo compactado com gzip).
2. Extrair o conteúdo e acessar o diretório rk.
3. Listar os arquivos e ler o script install.sh com cat.
4. Localizar a regra iptables aplicada à cadeia OUTPUT e identificar a porta de destino bloqueada.

### Comandos utilizados

```bash
cd ~/Documents/
file fw
# fw: gzip compressed data, last modified: Thu Dec 16 00:13:31 2010,
#     from Unix, original size modulo 2^32 8704000
file fw_extraido
ls -l
cd rk
ls -la
cat install.sh
```

### Explicação

O comando file revelou que o artefato fw era um arquivo compactado com gzip. Após a extração, o diretório rk foi acessado e o script install.sh foi lido com cat. O script grava em /etc/rc.d/rc.local e em /etc/init.d/xfs3 uma regra de iptables que insere, na primeira posição da cadeia OUTPUT, o descarte (DROP) de todo o tráfego TCP com destino à porta 45295. Dessa forma, o bloqueio é reaplicado a cada inicialização do sistema.

### Evidência

![CTF 1 – Barreiras invisíveis](../img/ctf-01.png)

---

[↑ Voltar ao índice](../README.md) · [CTF 2 →](ctf-02-rastros-do-pinguim.md)
