#  CTF Writeups — Análise Forense e Segurança Cibernética

Resolução comentada de **15 desafios no formato Capture The Flag (CTF)** realizados na Global Solution do 1º semestre do curso de **Segurança Cibernética da FIAP**, em ambiente **Kali Linux**.

Cada writeup traz o enunciado, o objetivo, o passo a passo da investigação, os comandos utilizados, a explicação do raciocínio, a evidência (captura de tela) e a resposta.

##  Sobre

**Karen Simões Kröger** — estudante de Segurança Cibernética na FIAP.

<!-- Adicione aqui seus links, por exemplo:
[LinkedIn](https://www.linkedin.com/in/seu-usuario) · [E-mail](mailto:seu@email.com)
-->

##  Habilidades demonstradas

- **Forense em Linux:** análise de `auth.log`, `dpkg.log` e `kernel.log`
- **Forense em Windows:** investigação de logs do Sysmon (`.evtx`) para identificar criação de contas e escalonamento de privilégios
- **Análise de rede:** identificação de conexões suspeitas de comando e controle (C2) cruzando `netstat` e lista de processos
- **Firewall:** leitura e auditoria de regras `iptables` e de scripts de persistência
- **Decodificação de dados:** hexadecimal, Base64 e reconstrução de strings ofuscadas em scripts Bash
- **Processamento de texto na linha de comando:** `grep`, `awk`, `sed`, `sort`, `uniq`, `tr` e pipes
- **Redes IPv4:** cálculo de sub-redes e planejamento com VLSM

## Ferramentas

`Kali Linux` · `Bash` · `grep` · `awk` · `sed` · `sort` · `uniq` · `tr` · `strings` · `xxd` · `base64` · `file`

## Índice dos desafios

| # | Desafio | Categoria | Técnicas |
|---|---|---|---|
| 1 | [Barreiras invisíveis](ctf-01-barreiras-invisiveis.md) | Análise de malware / Firewall | iptables, leitura de script de persistência |
| 2 | [Rastros do pinguim](ctf-02-rastros-do-pinguim.md) | Decodificação | Hexadecimal (xxd), substring em Bash, Base64 |
| 3 | [Palavra escondida](ctf-03-palavra-escondida.md) | Manipulação de texto | sort, uniq, sed |
| 4 | [Palavras ocultas](ctf-04-palavras-ocultas.md) | Decodificação | Base64 + filtragem |
| 5 | [Criação de usuário suspeita](ctf-05-criacao-de-usuario-suspeita.md) | Forense Windows | Logs Sysmon (.evtx), strings UTF-16 |
| 6 | [Filtragem básica](ctf-06-filtragem-basica.md) | Manipulação de texto | awk com regex em /etc/passwd |
| 7 | [Firewall auditor](ctf-07-firewall-auditor.md) | Firewall | Auditoria de regras iptables |
| 8 | [Vigilância administrativa](ctf-08-vigilancia-administrativa.md) | Forense de rede | Correlação netstat × processos (C2) |
| 9 | [Na madruga](ctf-09-na-madruga.md) | Forense Linux | Análise de auth.log (SSH) |
| 10 | [Quebra de sub-rede](ctf-10-quebra-de-sub-rede.md) | Redes | Cálculo de sub-rede /26 |
| 11 | [Roteamento estratégico](ctf-11-roteamento-estrategico.md) | Redes | Planejamento VLSM |
| 12 | [Tool](ctf-12-tool.md) | Forense Linux | Análise de dpkg.log |
| 13 | [ELF](ctf-13-elf.md) | Decodificação | Script oculto em hex + Base64 |
| 14 | [Filtragem obscura](ctf-14-filtragem-obscura.md) | Manipulação de texto | Laço while, base64, uniq -c |
| 15 | [Neon scavenger](ctf-15-neon-scavenger.md) | Forense Linux | Extração de dados de kernel.log com tr/awk |

##  Estrutura do repositório

- `ctf-NN-nome.md`: writeup de cada desafio
- `ctf-NN.png`: captura de tela da resolução
- `Relatorio_Global_Solution_1Semestre.pdf`: relatório completo em formato ABNT

##  Relatório completo

O relatório acadêmico original, em formato ABNT, está em [`Relatorio_Global_Solution_1Semestre.pdf`](Relatorio_Global_Solution_1Semestre.pdf).

##  Principais aprendizados

Na maioria dos casos, o primeiro passo foi identificar a natureza do artefato com `file`, o que orientou a técnica de leitura e decodificação. Os desafios mostraram padrões comuns em incidentes reais: ofuscação simples com hexadecimal e Base64, persistência por scripts de inicialização, criação de contas administrativas, conexões de saída para portas não padronizadas e instalação de scanners de vulnerabilidade. Também reforçaram que um único caractere copiado errado muda completamente o resultado de uma decodificação — por isso cada etapa precisa ser validada.

---

*Projeto acadêmico desenvolvido para a FIAP — Segurança Cibernética, 2026.*
