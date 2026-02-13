# Dia 02

## Principais comandos
ssh - Acessar outras máquinas linux. @ vem de at/na  
```bash
ssh nome-usuario@ip-da-maquina
```

cat - Visualizar conteúdo de arquivo  
```bash
cat /etc/os-release
```

pwd - Visualizar caminho absoluto do diretório atual  

cd - Altera o diretório de trabalho do shell  
```bash
cd /etc/apt/apt.conf.d/
```

```bash
# Vai para diretório /root
cd
```

```bash
# Retorna para ultimo diretório acessado
cd -
```

```bash
# Vai para diretório home do usuário logado
cd ~
```

```bash
# Vai para diretório acima do diretório atual
cd ..
```

```bash
# Vai para diretório quatro níveis acima do atual
cd ../../../../
```

ls - Lista informações sobre arquivos do diretório corrente  
```bash
# Mostra todos os arquivos, inclusive os ocultos
ls -a
```

```bash
# Mostra todos os arquivos, inclusive os ocultos em lista formatada
ls -la
```

```bash
# Mostra todos os arquivos, inclusive os ocultos em lista formatada legível para humanos. Tamanho de arquivos 1K, 234M, 2G
ls -lha
```
clear | CTRL + l - Limpa informações no terminal  
```bash
clear
```

history - Mostra na tela lista de comandos digitados  
```bash
history
```

su - - Assume usuário root. Logado como usuário root e vai está no diretório home do diretório root  
```bash
su -
```
CTRL + d - Utilizado para sair  

more - Pagina listagem de informações no shell. Lista somente para o final do arquivo  
```bash
ls -lha | more
```

less - Pagina listagem de informações no shell. Lista para cima e para baixo  
```bash
ls -lha | less
```
df - Visualizar informações sobre sistema de arquivos  
```bash
df -h
```

## Símbolos do shell  

~ - Simboliza diretório home do usuário corrente (logado no momento)  
$ - Simboliza quem está logado, nesse caso é um usuário comum  
\# - Simboliza quem está logado, nesse caso é o usuário root  

## Tipos de shell  
Interface para usuário interagir com sistema  

bash - Padrão na maioria das distros linux  
sh - Shell original  
zsh - Muito utilizado  

## Referências de diretórios  
. - Diretório atual  
.. - Diretório um nível acima  

## Autocomplete
tecla tab - Autocomplete de comandos, diretórios ou arquivos  

## Tipos de arquivos
\- - Arquivo  
d - Diretório  
l - Link simbólico. Um arquivo faze referência para arquivo original  
c - Dispositivos de caractere (transfere informação)  
b - Dispositivos de bloco (Armazenamento). HD, SSD, pendrive  

## Estuturas de diretórios
/bin - Binários do sistema. Arquivos executáveis essenciais para o linux. Todos os usuarios podem executar esse binários  

/boot - Arquivos essenciais para inicialização dos sistema. Armazena o kernel do linux  

/dev - Arquivos de dispositivos. Tudo no linux é arquivo  
ex1.: sda, sda1, sda2 - Discos sata  
ex2.: nvme0, nvme0n1, nvme0n1p1 - Discos nvme  
ex3.: tty (porta serial)
ex4.: psaux (mouse)















