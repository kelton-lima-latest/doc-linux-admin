# Dia 02

## Principais comandos
ssh - Acessar outras máquinas linux. @ vem de at/na.  
```bash
ssh nome-usuario@ip-da-maquina
```

cat - Visualizar conteúdo de arquivo.  
```bash
cat /etc/os-release
```

pwd - Visualizar caminho completo do diretório atual.  

cd - Altera o diretório de trabalho do shell.  
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

su - - Assumir usuário root. Logado como usuário root e vai está no diretório home do diretório root  
```bash
su -
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
