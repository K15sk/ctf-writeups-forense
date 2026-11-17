# CTF 12: Tool

**Categoria:** Forense Linux  
**Técnicas:** Análise de dpkg.log

## Enunciado

Após a detecção de atividades anômalas em um servidor Linux, foi realizada a coleta de evidências (linux.zip). Entre os registros do sistema há indícios da instalação de uma ferramenta típica de análise de vulnerabilidades. A missão é descobrir o nome dessa ferramenta.

## Objetivo

Analisar as evidências coletadas do servidor Linux (linux.zip) para identificar a ferramenta de análise de vulnerabilidades instalada.

## Resolução

1. Acessar o diretório Linux e listar os registros do sistema.
2. Identificar o dpkg.log, que registra as operações do gerenciador de pacotes.
3. Filtrar as linhas “status installed” com grep.
4. Localizar o pacote nessus 4.53-3, instalado em 24/04/2010.

### Comandos utilizados

```bash
cd Linux
ls -la
# apache2/  apt/  auth.log  daemon.log  debug  dpkg.log ...
grep -i "status installed" dpkg.log
# 2010-04-24 19:38:16 status installed nessus 4.53-3
```

### Explicação

O arquivo dpkg.log registra todas as operações do gerenciador de pacotes do Debian/Ubuntu. Filtrando as linhas com “status installed”, obteve-se a lista de pacotes instalados, entre os quais aparece o nessus (versão 4.53-3), instalado em 24/04/2010 às 19:38:16. O Nessus é um scanner de vulnerabilidades amplamente conhecido.

### Evidência

![CTF 12 – Tool](../img/ctf-12.png)

---

[↑ Voltar ao índice](../README.md) · [← CTF 11](ctf-11-roteamento-estrategico.md) · [CTF 13 →](ctf-13-elf.md)
