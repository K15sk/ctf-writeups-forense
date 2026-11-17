# CTF 15: Neon scavenger

**Categoria:** Forense Linux  
**Técnicas:** Extração de dados de kernel.log com tr/awk

## Enunciado

O kernel despejou detritos em kernel.log após uma brecha no setor 7. A chave de acesso foi fragmentada e ocultada sob ruído de hardware. É preciso filtrar o lixo, ignorar as frequências numéricas e reconstruir a sequência — o sinal está nos erros.

## Objetivo

Filtrar o ruído do arquivo kernel.log e reconstruir a chave de acesso fragmentada nas linhas de erro do kernel.

## Resolução

1. Ler o arquivo kernel.log e identificar as linhas KERNEL_ERR.
2. Remover os dígitos (“frequências numéricas”) com tr -d '0-9' e os espaços.
3. Extrair o conteúdo após os dois-pontos com awk.
4. Unir os fragmentos em uma única linha com tr -d '\n' e descartar o ruído final.

### Comandos utilizados

```bash
ls -l kernel.log
cat kernel.log | head -n 20
# [ 4.992103] KERNEL_ERR: 492F842I731A853P294{632
# [ 6.442190] KERNEL_ERR: 742C742y385b395e482r385D482e385f...
# [ 7.882144] KERNEL_ERR: 492_385A842n632a842l632y732s532i...

grep "KERNEL_ERR:" kernel.log | tr -d '0-9' | tr -d ' ' \
  | awk -F':' '{print $2}' | tr -d '\n'
# FIAP{CyberDefense_Analysis}x
```

### Explicação

Seguindo a pista “o sinal está nos erros”, foram selecionadas apenas as linhas KERNEL_ERR. O comando tr -d '0-9' removeu os dígitos (as “frequências numéricas”), o segundo tr eliminou os espaços, o awk extraiu o conteúdo após os dois-pontos e o último tr juntou os fragmentos em uma única linha. O caractere “x” final é ruído posterior ao fechamento da chave.

### Evidência

![CTF 15 – Neon scavenger](../img/ctf-15.png)

---

[↑ Voltar ao índice](../README.md) · [← CTF 14](ctf-14-filtragem-obscura.md)
