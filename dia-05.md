# Aula 05 — Comandos diversos (Linux)

> Objetivo: consolidar utilitários úteis para administração e manipulação de arquivos, com exemplos diretos e observações práticas.

---

## 1) Atributos de arquivos (além de permissões)

### `chattr`
Altera **atributos** de arquivos e diretórios em sistemas de arquivos Linux (ex.: ext2/3/4).  
Atributos **não são** as mesmas coisas que permissões (`chmod`).

> **Atenção:** normalmente requer privilégios de **root** e alguns atributos podem “travar” o arquivo/diretório. Use com cuidado.

**Exemplos**
```bash
chattr +i nome-arquivo           # adiciona atributo imutável (não altera/remove)
chattr -i nome-arquivo           # remove atributo imutável

chattr +i nome-diretorio         # adiciona atributo imutável ao diretório
chattr -i nome-diretorio         # remove atributo imutável do diretório

chattr +a nome-arquivo           # append-only: só permite adicionar conteúdo
echo "teste" >> nome-arquivo     # exemplo prático para append-only

chattr +a nome-diretorio         # append-only em diretório: impede remoções dentro do diretório

chattr +a +i *                   # aplica atributos em arquivos do diretório atual (atenção ao impacto)

chattr +c nome-arquivo           # compactação transparente (pode não existir em todos FS/kernels)
chattr +s nome-arquivo           # deleção “segura” (não confiável em ext4 / setups modernos)

chattr +S nome-arquivo           # tenta forçar escrita imediata (sincronização)
chattr +D nome-diretorio         # escrita síncrona para atualizações de diretório

chattr +d nome-arquivo           # exclui de backups feitos por ferramentas específicas (ex.: dump)
```

### `lsattr`
Lista os atributos de arquivos e diretórios.

**Exemplos**
```bash
lsattr nome-arquivo              # atributos do arquivo
lsattr -d nome-diretorio         # lista atributos do diretório (não dos conteúdos)
```

---

## 2) Recorte e extração de partes do texto

### `cut`
Extrai partes de linhas usando delimitador, posições de caracteres ou bytes.

**Exemplos**
```bash
cut -d ":" -f 1 nome-arquivo     # campo 1 usando ":" como delimitador
cut -d ":" -f 1-3 nome-arquivo   # campos 1 a 3 (intervalo)

cut -b 1-4 nome-arquivo          # por byte (útil para dados em ASCII/byte a byte)
cut -c 1-4 nome-arquivo          # por caractere (conta caracteres; pode variar com multibyte)
```

---

## 3) Comparação de arquivos e diretórios

### `cmp`
Compara dois arquivos **byte a byte**.

**Exemplos**
```bash
cmp nome-arquivo1 nome-arquivo2  # compara dois arquivos (aponta a primeira diferença)

cmp -s nome-arquivo1 nome-arquivo2
echo $?                          # 0=iguais | 1=diferentes | 2=erro (ex.: arquivo inexistente)
```

### `diff`
Compara arquivos de forma legível e é base para patches.

**Exemplos**
```bash
diff nome-arquivo1 nome-arquivo2     # diferença entre arquivos
diff -u nome-arquivo1 nome-arquivo2  # formato unificado (muito usado em reviews)

diff -r dir1 dir2                    # compara diretórios recursivamente
```

---

## 4) Localização de comandos e arquivos relacionados

### `whereis`
Localiza caminhos relacionados a um comando (binário, código-fonte e/ou man pages, quando disponíveis).

**Exemplo**
```bash
whereis ls
```

### `which`
Mostra o caminho do executável que será usado pelo shell (respeita o `PATH`).

**Exemplo**
```bash
which ls
```

> Dica: para ambientes com aliases/funções, considere `type -a <comando>` para investigar melhor.
