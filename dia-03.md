# Dia 03

## Comandos internos
Executado mais rápido que comando externo.  
Como identificar se um comando é interno?  

```bash
man builtins
```

```bash
which ls
```

Existem comandos que são internos e externos. Como saber qual está sendo executado?  
Sempre é executado o comando interno, pois é mais rápido.  

```bash
# Informa se o comando está sendo executado internamente ou externamente
type ls
```

touch - Cria arquivo vazio sem a necessidade de abrir editor de arquivos.  
```bash
touch nome-arquivo
```

ls - 
```bash
# Lista arquivos, sem listar diretório atual e diretório anterior
ls -A
```

```bash
# Não lista arquivo com ~ no final. São arquivos de backupo
ls -B
```

```bash
# Utiliza cores para diferenciar diretórios de arquivos
ls --color=auto
```

```bash
# Apenas padrão convencional
ls --color=never
```

```bash
# Lista arquivos de dois diretórios simultaneamente
ls pasta1 pasta2
```

```bash
# Lista, apenas, informação do diretório e não do conteúdo dentro do diretório
ls -lha -d pasta1
```

```bash
# Lista e classifica ordenando pela ultima alteração
ls -lha -f
```

```bash
# Adiciona separador para identificar arquivos de diretórios
ls -F
```
/ - Diretório
@ - Link simbólico
= - Socket
* - Executável

```bash
# Aculta coluna que informa o grupo
ls -lG
```

```bash
# Converte nome do usuário e grupo para id do usuário e id do grupo
ls -ln
```

```bash
# Oculta links simbólicos da listagem de arquivos
ls -lL
```

```bash
# Exibe listagem de arquivos sem listar os grupos, apenas os donos dos arquivos
ls -lo
```

```bash
# Exibe listagem de arquivos equivalente ao -f, mas não identifica executáveis e links simbólicos
ls -lp
```

```bash
# Exibe listagem de arquivos e classifica por data da ultima alteração. Mais atuais no início
ls -lt
```

```bash
# Exibe listagem de arquivos e classifica por data da ultima alteração. Mais atuais no final
# utilizado para logs
ls -lt
```

mkdir - Cria diretório.  
