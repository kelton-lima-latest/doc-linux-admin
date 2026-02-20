# Dia 04 — Curingas (globbing) no Shell

> **Observação:** os exemplos abaixo foram testados no diretório `/usr/bin/`.  
> Em shells como **bash** e **zsh**, esses “curingas” são expandidos pelo **próprio shell** antes do comando (`ls`, `cp`, etc.) ser executado.

---

## Visão geral dos padrões

| Padrão | O que significa | Exemplo |
|---|---|---|
| `*` | **Zero ou mais** caracteres na posição | `ls a*` |
| `?` | **Exatamente 1** caractere na posição | `ls m??` |
| `[a-z]` | **Faixa** / conjunto de caracteres | `ls m[a-v]` |
| `[^...]` | **Negação** dentro de colchetes (um caractere que **não** seja o informado) | `ls m[^v]` |
| `{a,b}` | **Expansão de chaves** (gera combinações de strings) | `ls x{zd,ze}*` |

---

## `*` — zero ou mais caracteres

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

## `?` — exatamente um caractere

- Identifica **apenas 1** caractere naquela posição.

```bash
# Arquivos que iniciam com "m" e têm 1 caractere após o inicial
ls m?

# Arquivos que iniciam com "m" e têm 2 caracteres após o inicial
ls m??
```

---

## `[a-z]` — faixa / conjunto entre colchetes

- Define um **padrão entre colchetes**, limitando uma faixa de caracteres para **um único caractere** naquela posição.

```bash
# Arquivos que iniciam com "m" e têm na segunda posição um caractere entre "a" e "t"
ls m[a-t]*

# Arquivos que iniciam com "m" e têm na segunda posição um caractere entre "a" e "v"
ls m[a-v]*

# Arquivos que iniciam com "m" e NÃO têm "v" como segundo caractere
ls m[^v]*

# Arquivos que iniciam com "m" e NÃO têm (t..v) como segundo caractere
ls m[^t-v]*
```

> Dica: dentro de `[]`, **o padrão vale para 1 posição**.  
> Se você precisa de “um ou mais caracteres depois”, combine com `*` (como nos exemplos acima).

---

## `{}` — expansão de chaves (brace expansion)

- Expansão de chaves **gera combinações de strings** (não é um “curinga” de caracteres, mas é muito usada junto com globbing).

```bash
# Arquivos que iniciam com "x", depois "zd" OU "ze", e seguem com qualquer coisa
ls x{zd,ze}*
```

---

## Combinando padrões

```bash
# Inicia com "a", depois 1 caractere, depois "t", e segue com qualquer coisa
ls a?t*

# 1º caractere qualquer, 2º caractere "z", e segue com qualquer coisa
ls ?z*
```

---

## Boas práticas rápidas

- Use aspas **somente** quando quiser **impedir** a expansão do shell:
  - `echo "*.log"` (imprime literalmente `*.log`)
  - `ls *.log` (lista arquivos `.log`)
- Se um padrão não encontrar nada, alguns shells podem:
  - manter o texto como está, ou
  - gerar erro (dependendo da configuração).  
  No `zsh`, isso pode ser ajustado via opções como `nomatch`.
