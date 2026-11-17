# CTF 11: Roteamento estratégico

**Categoria:** Redes  
**Técnicas:** Planejamento VLSM

## Enunciado

A equipe de redes da FIAP Corp deve distribuir o bloco 192.168.10.0/24 entre quatro setores — Engenharia (60 hosts), RH (30 hosts), Financeiro (25 hosts) e TI (10 hosts) — utilizando VLSM (Variable Length Subnet Masking). O objetivo é identificar o endereço de broadcast da sub-rede alocada ao setor de RH.

## Objetivo

Verificar a distribuição VLSM do bloco 192.168.10.0/24 entre quatro setores e identificar o endereço de broadcast da sub-rede do setor de RH.

## Resolução

1. Ler o arquivo subnet_plan.txt com as necessidades de cada setor.
2. Ordenar os setores da maior para a menor quantidade de hosts.
3. Atribuir a cada setor a menor máscara que comporte seus hosts (2^n − 2 ≥ hosts), conforme o Quadro 1.
4. Identificar o último endereço da sub-rede do RH (192.168.10.64/27).

### Comandos utilizados

```bash
file subnet_plan.txt
# subnet_plan.txt: ASCII text
cat subnet_plan.txt
# Bloco principal: 192.168.10.0/24
# Setor: Engenharia  Necessidade: 60 hosts
# Setor: RH          Necessidade: 30 hosts
# Setor: Financeiro  Necessidade: 25 hosts
# Setor: TI          Necessidade: 10 hosts
```

### Explicação

No VLSM, as sub-redes são alocadas da maior para a menor demanda, escolhendo para cada setor a menor máscara que comporte seus hosts (2^n − 2 ≥ hosts). A distribuição resultante é apresentada no Quadro 1. O setor de RH recebe a sub-rede 192.168.10.64/27, cujo último endereço — o de broadcast — é 192.168.10.95.

| Setor | Hosts | Máscara | Rede / faixa válida | Broadcast |
|---|---|---|---|---|
| Engenharia | 60 | /26 | .0 / .1 – .62 | 192.168.10.63 |
| RH | 30 | /27 | .64 / .65 – .94 | 192.168.10.95 |
| Financeiro | 25 | /27 | .96 / .97 – .126 | 192.168.10.127 |
| TI | 10 | /28 | .128 / .129 – .142 | 192.168.10.143 |

### Evidência

![CTF 11 – Roteamento estratégico](../img/ctf-11.png)

---

[↑ Voltar ao índice](../README.md) · [← CTF 10](ctf-10-quebra-de-sub-rede.md) · [CTF 12 →](ctf-12-tool.md)
