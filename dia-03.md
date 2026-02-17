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
\* - Executável  

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

```bash
# Exibe listagem de arquivos e classifica pela data de alteração
ls -lac
```

```bash
# Exibe listagem de arquivos e classifica pela extensão dos arquivos
ls -laX
```

```bash
# Exibe listagem de arquivos e classifica pela extensão dos arquivos, revertendo laX
ls -lXr
```

```bash
# Exibe listagem de arquivos de forma recursiva. Também exibe os itens dentro de diretórios
ls -laR
```

mkdir - Cria diretórios  
```bash
mkdir nome-diretorio
```

```bash
# Cria mais de um diretório em um mesmo comando
mkdir nome-diretorio1 nome-diretorio2
```
 
```bash
# Cria estrutura de diretórios sem que existam
mkdir -p nome-diretorio2/nome-diretorio2_1/nome-diretorio2_1_1
```

tree - Exibe listagem de diretórios e arquivos organizando em níveis  
```bash
tree
```

```bash
# Exibe informações com visual mais atual
tree -A
```

rmdir - Remove diretórios
```bash
# Remove diretórios vazios
rmdir nome-diretorio
```

```bash
# Remove diretórios ou estruturas de diretórios vazios, não remove se houver arquivos dentro dos diretórios
rmdir -p nome-diretorio
```

cat - Exibe conteúdo de arquivos
```bash
cat nome-arquivo
```

```bash
# Exibe número de linhas
cat -n nome-arquivo
```

```bash
# Não exibe linhas em branco repetidas
cat -s nome-arquivo
```

```bash
# Enumera somente linhas que não estão em branco
cat -b nome-arquivo
```

```bash
# Adiciona $ ao final de cada linha
cat -E nome-arquivo
```

```bash
# Converte TAB em ^I
cat -T nome-arquivo
```

zcat - Exibe o que está dentro de arquivos .gz
```bash
zcat nome-arquivo.gz
```

zcat - Exibe o que está dentro de arquivos bz2
```bash
bzcat nome-arquivo.bz2
```

zcat - Exibe o que está dentro de arquivos xz
```bash
xzcat nome-arquivo.xz
```

rm - Remove arquivos ou diretórios
```bash
rm nome-arquivo
```

```bash
# Remove diretórios
rm -r nome-diretório
```

```bash
# Força remoção de diretórios
rm -rf nome-diretório
```

```bash
# Pergunta se realmente que remover arquivo ou diretório
rm -i nome-diretório
```

```bash
# Remove todos os diretórios e arquivos dentro de um diretório, não remove arquivos ocultos
rm -rf *
```

```bash
# Remove todos os arquivos que iniciam com a letra a
rm -rf *a
```

```bash
# Remove todos os arquivos que iniciam com -, vale também para outros caracteres especiais (?, *)
rm -- -
```

cp - Copia arquivos  
sintaxe: cp [origem] [destino]

```bash
# Copia arquivo no mesmo diretório
cp nome-arquivo nome-arquivo2
```

```bash
# Copia arquivo para diretório um nível acima
cp nome-arquivo ..
```

```bash
# Copia arquivo para diretório dentro do diretório atual
cp nome-arquivo nome-diretório/
```

```bash
# Copia vários arquivos para diretório dentro do diretório atual
# Obrigatório que o destino seja um diretório
cp nome-arquivo1 nome-arquivo2 nome-diretório/
```

```bash
# Força cópia de arquivos ou diretórios
cp -rf * nome-diretório/
```

```bash
# Copia dispositivos especiais. Perigoso, tenta ler os dados do hardware e transforma em um arquivo comum
cp -R diretorio-origem diretório-destino/
```

```bash
# Cria link simbólico do nome-arquivo2 para nome-arquivo1
cp -vs nome-arquivo1 nome-arquivo2
```

```bash
# Copia arquivos, somente, se informação da origem for mais atualizada que destino
cp -u nome-arquivo nome-diretorio/
```

```bash
# Copia arquivos verbosamente. Imprime no terminal exatamente o que foi feito
cp -v nome-arquivo nome-diretorio/
```

```bash
# Não copia arquivos que estão em outras partições
cp -x nome-arquivo diretorio-destino/
```

```bash
# Copia preservando artibutos do arquivo, dono, grupo, permissões
cp -p nome-arquivo diretorio-destino/
```

```bash
# Copia referência a links simbólicos, preservando atributos e recursivo
cp -a nome-arquivo diretorio-destino/
```

mv - Move arquivos ou diretórios da origem para destino. Origem é apagada. Utilizado também para renomear arquivos ou diretórios. Utiliza os mesmos parâmetros do comando cp  
```bash
mv nome-arquivo diretorio-destino/
```

```bash
# Modo interativo. Verifica se arquivo existe no destino
mv -i nome-arquivo diretorio-destino/
```

```bash
# Renomeia arquivo
mv nome-arquivo nome-arquivo2
```

SHIFT + page up - Rolagem de conteúdo para cima  

SHIFT + page down - Rolagem de conteúdo para baixo

















