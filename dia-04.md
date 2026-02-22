# Dia 04 — Curingas (globbing) e comandos diversos no Linux

> **Observação:** os exemplos de globbing abaixo foram testados no diretório `/usr/bin/`.  
> Em shells como **bash** e **zsh**, os “curingas” são expandidos pelo **próprio shell** antes do comando (`ls`, `cp`, etc.) ser executado.

---

## Sumário

1. [Curingas (globbing) no Shell](#1-curingas-globbing-no-shell)  
2. [Atalhos e comentários no terminal](#2-atalhos-e-comentários-no-terminal)  
3. [Data e hora](#3-data-e-hora)  
4. [Disco: espaço, consumo e links](#4-disco-espaço-consumo-e-links)  
5. [Localização de arquivos e diretórios](#5-localização-de-arquivos-e-diretórios)  
6. [Memória](#6-memória)  
7. [Pesquisa de texto](#7-pesquisa-de-texto)  
8. [Visualização e paginação de arquivos](#8-visualização-e-paginação-de-arquivos)  
9. [Ordenação de conteúdo](#9-ordenação-de-conteúdo)  
10. [Tempo de execução e utilitários](#10-tempo-de-execução-e-utilitários)  
11. [Logs e mensagens do Kernel](#11-logs-e-mensagens-do-kernel)  
12. [Mensagens entre usuários](#12-mensagens-entre-usuários)  
13. [Saída de texto](#13-saída-de-texto)

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

### `*` — zero ou mais caracteres

```bash
ls a*      # retorna todos os arquivos que iniciam com "a"
ls b*      # retorna todos os arquivos que iniciam com "b"
ls *path   # retorna todos os arquivos que terminam com "path"
ls a*r     # retorna todos os arquivos que iniciam com "a" e terminam com "r"
```

### `?` — exatamente um caractere

```bash
ls m?      # arquivos que iniciam com "m" e têm 1 caractere após o inicial
ls m??     # arquivos que iniciam com "m" e têm 2 caracteres após o inicial
```

### `[a-z]` / `[^...]` — faixa / conjunto (1 posição)

```bash
ls m[a-t]*   # inicia com "m" e tem 2º caractere entre "a" e "t"
ls m[a-v]*   # inicia com "m" e tem 2º caractere entre "a" e "v"
ls m[^v]*    # inicia com "m" e NÃO tem "v" como 2º caractere
ls m[^t-v]*  # inicia com "m" e NÃO tem 2º caractere entre "t" e "v"
```

### `{}` — expansão de chaves (brace expansion)

```bash
ls x{zd,ze}* # inicia com "x", depois "zd" OU "ze", e segue com qualquer coisa
```

### Combinando padrões

```bash
ls a?t*   # inicia com "a", depois 1 caractere, depois "t", e segue com qualquer coisa
ls ?z*    # 1º caractere qualquer, 2º caractere "z", e segue com qualquer coisa
```

### Boas práticas rápidas (globbing)

- Aspas impedem a expansão do shell:
  - `echo "*.log"` → imprime literalmente `*.log`
  - `ls *.log` → expande e lista arquivos `.log`
- Se o padrão não encontrar nada, o comportamento pode variar por shell/configuração (no `zsh`, a opção `nomatch` influencia isso).

---

## 2) Atalhos e comentários no terminal

- `Ctrl + L` ou `clear` → limpa a tela  
  **Obs.:** se você estiver digitando um comando, ao rodar `clear` o texto digitado pode permanecer no prompt (depende do terminal/shell).
- `#` → comentário (muito usado para documentar comandos grandes, scripts e “pausas” em exemplos)

---

## 3) Data e hora

### `date` — configura, exibe ou converte data/hora

> `date` sem parâmetros exibe data/hora no **timezone local** do sistema.  
> `date -u` exibe em **UTC**.

```bash
date                     # exibe data/hora local
date -u                  # exibe data/hora em UTC

sudo date -s 10:25       # ajusta apenas a hora (requer privilégios)

sudo date 101007452026   # ajusta data e hora (formato: MMDDhhmmYYYY)
                         # exemplo: 10(Out) 10(dia) 07(hora) 45(min) 2026(ano)
```

#### Formatação com `+...`

```bash
date +%d                 # retorna somente o dia do mês (01..31)
date +%d%Y               # retorna dia do mês + ano (ex.: 212026)
date +%d-%Y              # retorna dia e ano com separador (ex.: 21-2026)
date +"%d-%Y %T"         # retorna dia-ano e hora completa (HH:MM:SS)
date +"%d %Y %j"         # retorna dia do mês, ano e dia do ano (001..366)
date +"%d %r"            # retorna dia e hora no formato 12h (AM/PM)

date --date='@1234567890' # converte timestamp Unix (segundos desde 1970-01-01 UTC)
date -u --date='@1'       # primeiro segundo do Unix epoch em UTC
```

### `hwclock --systohc`

```bash
hwclock --systohc        # salva o horário do sistema no relógio de hardware (RTC)
```

---

## 4) Disco: espaço, consumo e links

### `df` — espaço livre em partições montadas

```bash
df                       # mostra espaço livre em cada partição montada
df -h                    # humanizado (blocos 1024); também lista mounts de rede
df -H                    # humanizado (blocos 1000)
df -l                    # somente sistemas de arquivos locais
df -m                    # exibe em MB
df -a                    # inclui pseudo-filesystems (ex.: cgroups)
df -i                    # detalhamento de inodes (limite de arquivos)
df -T                    # mostra o tipo do filesystem em cada partição
df -hT                   # tipo + humanizado
df -hT -t ext4           # filtra por tipo de filesystem (ex.: ext4)
df -ahT -t cgroup2       # exemplo: mostra sistemas usando cgroup2
df -P                    # formato POSIX (útil para scripts)
```

### `du` — quanto arquivo/diretório ocupa em disco

```bash
du                       # exibe uso de disco por diretório/arquivo (por padrão em blocos)
du -h                    # formato humanizado
du -H                    # (varia por distro) humanizado/decimal (nem sempre disponível)
du -hs                   # soma total do alvo (resumo)
du -ks                   # soma total em KB
du -ms                   # soma total em MB
du -hc                   # humanizado + total ao final
```

### `ln` — links (hard e simbólico)

```bash
ln arquivo destino       # cria hard link (mesmo inode; normalmente no mesmo filesystem)
ln -s nome-arquivo nome-link  # cria link simbólico (atalho por caminho)
```

---

## 5) Localização de arquivos e diretórios

### `find` — localizar arquivos/diretórios

```bash
find .                   # lista arquivos e diretórios a partir do diretório atual
find /usr/ -name docker  # busca por nome "docker" em /usr/

find /usr/ -type d -name docker     # apenas diretórios chamados docker
find /usr/ -type f -name docker     # apenas arquivos chamados docker

find /usr/ -maxdepth 2 -type f -name docker                 # até 2 níveis de profundidade
find /usr/ -mindepth 2 -maxdepth 4 -type f -name docker      # entre 2 e 4 níveis
```

#### Tempo (mtime/atime/ctime) — observações importantes

- `-mtime` → **modificação do conteúdo** (dias)  
- `-amin` → **acesso** (minutos)  
- `-cmin` → **mudança de metadados** (minutos)  
- `-ctime` → **mudança de metadados** (dias)

```bash
find /etc -mtime -1      # arquivos modificados nas últimas 24h
find /etc -amin -10      # arquivos acessados nos últimos 10 minutos
find /tmp -cmin -10      # arquivos com metadados alterados nos últimos 10 minutos
find /etc -ctime -1      # metadados alterados nas últimas 24h
find /etc -ctime +2      # metadados alterados há mais de 2 dias
```

#### Dono / grupo / links / tamanho / tipos

```bash
find . -gid 1000         # arquivos/diretórios do grupo ID 1000
find . -uid 1000         # arquivos/diretórios do usuário ID 1000
find . -user root        # arquivos/diretórios do usuário root
find . -group root       # arquivos/diretórios do grupo root

find . -links 1          # itens que possuam exatamente 1 hard link

find / -size +1000       # mais de 1000 blocos
find / -size +1000k      # mais de 1000 KB
find / -size +1000c      # mais de 1000 bytes

find /dev -type b        # dispositivos de bloco
find /dev -type c        # dispositivos de caractere
find /dev -type l        # links simbólicos
```

---

## 6) Memória

### `free` — memória física e swap

```bash
free                     # exibe informações de memória e swap
free -h                  # humanizado
free -gibi               # em GiB
free -mebi               # em MiB
free -kibi               # em KiB
free -gibi -s 1          # atualiza a cada 1 segundo
```

---

## 7) Pesquisa de texto

### `grep` — pesquisar padrões em arquivos/entrada padrão

```bash
grep 'root' /etc/passwd          # linhas que contêm "root"
grep -v 'root' /etc/passwd       # linhas que NÃO contêm "root"

grep -i 'AQUI' ./nome-arquivo    # ignora maiúsculas/minúsculas
grep -iE '^a' ./nome-arquivo     # regex estendida + ignora case
grep -iF '.*' ./nome-arquivo     # busca literal (não interpreta regex)
```

#### Flags citadas (explicadas)

```bash
grep -f patterns.txt arquivo.log # lê padrões de um arquivo (um por linha)
```

```bash
grep -ir "$HOST" /etc            # recursivo: linhas que contêm $HOST
grep -irl "$HOST" /etc           # recursivo: apenas nomes dos arquivos com $HOST
grep -irn "$HOST" /etc           # recursivo: mostra número da linha
```

---

## 8) Visualização e paginação de arquivos

### `head` — primeiras linhas/bytes

```bash
head /etc/passwd          # 10 primeiras linhas
head -n 3 /etc/passwd     # 3 primeiras linhas
head -c 512 /etc/passwd   # primeiros 512 bytes
```

### `tail` — últimas linhas / tempo real

```bash
tail nome-arquivo         # 10 últimas linhas
tail -f nome-arquivo      # acompanha alterações em tempo real
```

### `nl` — numeração de linhas

```bash
nl arquivo.txt            # numera as linhas do arquivo
```

### `more` e `less` — paginação

```bash
more nome-arquivo         # visualiza página por página (simples)
less nome-arquivo         # página por página com navegação e busca
```

Atalhos úteis no `less`:

```text
/texto   pesquisa dentro do less
n        vai para a próxima ocorrência
q        sai do less
```

---

## 9) Ordenação de conteúdo

### `sort` — ordena conteúdo (números e texto)

```bash
sort nome-arquivo         # ordena (texto/lexicográfico)
sort -r nome-arquivo      # inverte a ordem
sort -n nome-arquivo      # ordena numericamente
sort -c nome-arquivo      # verifica se já está ordenado

# Ordena pela 2ª coluna, usando ":" como delimitador
sort -t ":" -k 2,2 nome-arquivo
```

> Nota: exemplos antigos usam `sort +1`; prefira `-k` (mais atual e portátil).

---

## 10) Tempo de execução e utilitários

### `time` — relatório de tempo de execução

```bash
time ls                   # mede o tempo de execução do comando
```

Exemplo de saída (varia):

```text
user 0,00s system 82% cpu 0,002 total
```

### `touch` — cria arquivo vazio / altera timestamp

```bash
touch nome-arquivo        # cria arquivo vazio (se não existir)

# Ajusta timestamp (formato: [[CC]YY]MMDDhhmm[.ss])
touch -t 202610100745 nome-arquivo
```

### `uptime` — tempo de atividade desde o último boot

```bash
uptime
```

---

## 11) Logs e mensagens do Kernel

### `dmesg` — mensagens do ring buffer do kernel

```bash
dmesg                     # exibe mensagens do kernel (buffer)
dmesg -t                  # sem coluna de timestamp (bruto)
dmesg -w                  # em tempo real
dmesg -x                  # decodifica em texto mais legível (varia por distro)
dmesg -T                  # timestamp legível (humano)
dmesg -c                  # apaga o buffer (cuidado)

dmesg | grep -i eth0       # filtra mensagens relacionadas (ex.: placa de rede)
```

---

## 12) Mensagens entre usuários

```bash
mesg                      # habilita/desabilita receber mensagens (para talk/write)
talk usuario              # conversa em tempo real (estilo clássico)
```

---

## 13) Saída de texto

### `echo` — exibe mensagem na tela

```bash
echo "$HOST"              # exibe valor da variável de ambiente $HOST
echo -n 'teste'           # não faz quebra de linha
echo -e "Teste do ç"      # interpreta escapes (ex.: \n, \t)
