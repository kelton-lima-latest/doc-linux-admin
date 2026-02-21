# Dia 04 — Curingas (globbing) e comandos diversos no Linux

> **Observação:** os exemplos de globbing abaixo foram testados no diretório `/usr/bin/`.  
> Em shells como **bash** e **zsh**, os “curingas” são expandidos pelo **próprio shell** antes do comando (`ls`, `cp`, etc.) ser executado.

---

## 1) Curingas (globbing) no Shell

### Visão geral dos padrões

| Padrão | O que significa | Exemplo |
|---|---|---|
| `*` | **Zero ou mais** caracteres na posição | `ls a*` |
| `?` | **Exatamente 1** caractere na posição | `ls m??` |
| `[a-z]` | **Faixa** / conjunto de caracteres (1 posição) | `ls m[a-v]*` |
| `[^...]` | **Negação** dentro de colchetes (1 posição) | `ls m[^v]*` |
| `{a,b}` | **Expansão de chaves** (gera combinações de strings) | `ls x{zd,ze}*` |

> Nota: `[]` e `[^...]` sempre correspondem a **um único caractere** naquela posição.  
> Para “continuar” o padrão, combine com `*` (ex.: `m[a-v]*`).

---

### `*` — zero ou mais caracteres

- Identifica **nenhum, um ou mais** caracteres naquela posição.

```bash
# Retorna todos os arquivos que iniciam com a letra a
ls a*

# Retorna todos os arquivos que iniciam com a letra b
ls b*

# Retorna todos os arquivos que terminam com "path"
ls *path

# Retorna todos os arquivos que iniciam com "a" e terminam com "r"
ls a*r
```

---

### `?` — exatamente um caractere

- Identifica **apenas 1** caractere naquela posição.

```bash
# Arquivos que iniciam com "m" e têm 1 caractere após o inicial
ls m?

# Arquivos que iniciam com "m" e têm 2 caracteres após o inicial
ls m??
```

---

### `[a-z]` — faixa / conjunto entre colchetes

- Define um padrão entre colchetes, limitando uma faixa de caracteres para **um único caractere** naquela posição.

```bash
# Inicia com "m" e tem na segunda posição um caractere entre "a" e "t"
ls m[a-t]*

# Inicia com "m" e tem na segunda posição um caractere entre "a" e "v"
ls m[a-v]*

# Inicia com "m" e NÃO tem "v" como segundo caractere
ls m[^v]*

# Inicia com "m" e NÃO tem (t..v) como segundo caractere
ls m[^t-v]*
```

---

### `{}` — expansão de chaves (brace expansion)

- Expansão de chaves **gera combinações de strings**.  
  Não é um “curinga” de caracteres, mas é muito usada junto com globbing.

```bash
# Inicia com "x", depois "zd" OU "ze", e segue com qualquer coisa
ls x{zd,ze}*
```

---

### Combinando padrões

```bash
# Inicia com "a", depois 1 caractere, depois "t", e segue com qualquer coisa
ls a?t*

# 1º caractere qualquer, 2º caractere "z", e segue com qualquer coisa
ls ?z*
```

---

### Boas práticas rápidas (globbing)

- Use aspas **somente** quando quiser **impedir** a expansão do shell:
  - `echo "*.log"` (imprime literalmente `*.log`)
  - `ls *.log` (lista arquivos `.log`)
- Se um padrão não encontrar nada, alguns shells podem:
  - manter o texto como está, ou
  - gerar erro (dependendo da configuração).  
  No `zsh`, isso pode ser ajustado via opções como `nomatch`.

---

## 2) Atalhos e comentários no terminal

- `Ctrl + L` ou `clear`: limpa a tela.  
  Observação: se você estiver digitando um comando e executar `clear`, o texto digitado pode permanecer no prompt (depende do terminal/shell).
- `#`: comentário. Muito utilizado para documentar comandos longos ou “pausar” explicações em scripts.

---

## 3) Data e hora

### `date` — exibe/ajusta/formata data e hora

> `date` sem parâmetros exibe **data/hora no timezone local** do sistema.  
> `date -u` exibe em **UTC**.

```bash
# Exibe data/hora local
date

# Exibe em UTC
date -u

# Ajusta apenas a hora (requer privilégios)
sudo date -s 10:25

# Ajusta data e hora (formato: MMDDhhmmYYYY)
# exemplo: 10(Out) 10(dia) 07(hora) 45(min) 2026(ano)
sudo date 101007452026
```

#### Formatação com `+...`

```bash
# Retorna somente o dia do mês (01..31)
date +%d

# Retorna dia do mês + ano (ex.: 212026)
date +%d%Y

# Retorna dia + ano com separador (ex.: 21-2026)
date +%d-%Y

# Retorna dia-ano e hora completa (HH:MM:SS)
date +"%d-%Y %T"

# Retorna dia do mês, ano, e dia do ano (001..366)
date +"%d %Y %j"

# Retorna dia e hora no formato 12h (AM/PM)
date +"%d %r"

# Converte timestamp Unix (segundos desde 1970-01-01 UTC)
date --date='@1234567890'

# Primeiro segundo do Unix epoch em UTC
date -u --date='@1'
```

### `hwclock --systohc`

- Salva o horário atual do **sistema** no relógio de **hardware** (RTC).  
  Útil para manter a hora consistente após desligar/reiniciar.

```bash
hwclock --systohc
```

---

## 4) Disco: espaço e consumo

### `df` — espaço livre em partições montadas

```bash
# Visão padrão
df

# Formato humanizado (blocos 1024)
df -h

# Formato “humanizado” (blocos 1000)
df -H

# Apenas sistemas de arquivos locais
df -l

# Em MB
df -m

# Inclui pseudo-filesystems (ex.: cgroups)
df -a

# Informações de inodes (limite de arquivos)
df -i

# Exibe o tipo do filesystem
df -T

# Tipo + humanizado
df -hT

# Filtra por tipo de filesystem
df -hT -t ext4

# Mostra somente cgroup2 (exemplo)
df -ahT -t cgroup2

# Saída em formato POSIX
df -P
```

### `du` — quanto um arquivo/diretório ocupa em disco

```bash
# Formato humanizado
du -h

# Soma total (útil para diretórios)
du -hs

# Soma total em KB
du -ks

# Soma total em MB
du -ms

# Humanizado + total ao final
du -hc
```

### `ln` — links (hard e simbólico)

- **Hard link**: aponta para o mesmo inode (normalmente no **mesmo filesystem**).
- **Link simbólico** (`-s`): atalho que aponta para um caminho.

```bash
# Link simbólico
ln -s nome-arquivo nome-link
```

---

## 5) Localização de arquivos e diretórios

### `find` — localizar arquivos/diretórios com filtros

```bash
# Lista arquivos e diretórios a partir do diretório atual
find .

# Procura "docker" em /usr/
find /usr/ -name docker

# Apenas diretórios chamados docker
find /usr/ -type d -name docker

# Apenas arquivos chamados docker
find /usr/ -type f -name docker

# Limita profundidade (até 2 níveis)
find /usr/ -maxdepth 2 -type f -name docker

# Entre 2 e 4 níveis (mínimo e máximo)
find /usr/ -mindepth 2 -maxdepth 4 -type f -name docker
```

#### Tempo (mtime/atime/ctime) — observações importantes

- `-mtime`: **modificação** do conteúdo (em dias)
- `-amin`: **acesso** (em minutos)
- `-cmin`: **mudança de metadados** (em minutos)”
- `-ctime`: **mudança de metadados** (em dias)”

```bash
# Modificados nas últimas 24h
find /etc -mtime -1

# Acessados nos últimos 10 minutos
find /etc -amin -10

# Alterados nos últimos 10 minutos (metadados)
find /tmp -cmin -10

# Metadados alterados nas últimas 24h
find /etc -ctime -1

# Metadados alterados há mais de 2 dias
find /etc -ctime +2
```

#### Dono / grupo / links / tamanho / tipos de arquivo

```bash
# Grupo / usuário por ID
find . -gid 1000
find . -uid 1000

# Usuário / grupo por nome
find . -user root
find . -group root

# Quantidade de hard links
find . -links 1

# Tamanho (blocos, KB, bytes)
find / -size +1000
find / -size +1000k
find / -size +1000c

# Tipos em /dev (bloco, caractere, link simbólico)
find /dev -type b
find /dev -type c
find /dev -type l
```

---

## 6) Memória

### `free` — memória RAM e swap

```bash
# Visão padrão
free

# Humanizado
free -h

# Em GiB
free -gibi

# Em MiB
free -mebi

# Em KiB
free -kibi

# Atualiza a cada 1 segundo
free -gibi -s 1
```

---

## 7) Pesquisa de texto

### `grep` — buscar padrões em arquivos/entrada

```bash
# Linhas que contêm "root"
grep 'root' /etc/passwd

# Linhas que NÃO contêm "root"
grep -v 'root' /etc/passwd

# Ignora maiúsculas/minúsculas
grep -i 'AQUI' ./nome-arquivo

# Regex estendida (-E) + ignora case (-i)
grep -iE '^a' ./nome-arquivo

# String literal (não interpreta regex)
grep -iF '.*' ./nome-arquivo
```

#### Flags úteis (explicadas)

- `-f <arquivo>`: lê **vários padrões** de um arquivo (um por linha).  
  Ex.: `grep -f patterns.txt arquivo.log`
- `-F`: trata o padrão como **texto fixo** (sem regex).  
- `-E`: usa **regex estendida** (equivalente a `egrep`).

```bash
# Procura recursiva em /etc por $HOST
grep -ir "$HOST" /etc

# Retorna apenas nomes de arquivos que contêm $HOST
grep -irl "$HOST" /etc

# Retorna linhas + número da linha
grep -irn "$HOST" /etc
```

---

## 8) Visualização rápida de arquivos

### `head` — primeiras linhas/bytes

```bash
# 10 primeiras linhas
head /etc/passwd

# 3 primeiras linhas
head -n 3 /etc/passwd

# Primeiros 512 bytes
head -c 512 /etc/passwd
```

### `nl` — numeração de linhas

```bash
# Numera linhas
nl arquivo.txt
```
