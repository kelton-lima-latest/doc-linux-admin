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

pwd - Visualizar caminho absoluto do diretório atual.  

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

```bash
# Vai para diretório acima do diretório atual
cd ..
```

```bash
# Vai para diretório quatro níveis acima do atual
cd ../../../../
```

ls - Lista informações sobre arquivos do diretório corrente.  
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
clear | CTRL + l - Limpa informações no terminal.  
```bash
clear
```

history - Mostra na tela lista de comandos digitados.  
```bash
history
```

su - - Assume usuário root. Logado como usuário root e vai está no diretório home do diretório root.  
```bash
su -
```
CTRL + d - Utilizado para sair.  

more - Pagina listagem de informações no shell. Lista somente para o final do arquivo.  
```bash
ls -lha | more
```

less - Pagina listagem de informações no shell. Lista para cima e para baixo.  
```bash
ls -lha | less
```
df - Visualizar informações sobre sistema de arquivos.  
```bash
df -h
```

## Símbolos do shell  

~ - Simboliza diretório home do usuário corrente (logado no momento).  
$ - Simboliza quem está logado, nesse caso é um usuário comum.  
\# - Simboliza quem está logado, nesse caso é o usuário root.  

## Tipos de shell  
Interface para usuário interagir com sistema.  

bash - Padrão na maioria das distros linux.  
sh - Shell original.  
zsh - Muito utilizado.  

## Referências de diretórios  
. - Diretório atual.  
.. - Diretório um nível acima.  

## Autocomplete
tecla tab - Autocomplete de comandos, diretórios ou arquivos.  

## Tipos de arquivos
\- - Arquivo.  
d - Diretório.  
l - Link simbólico. Um arquivo faz referência para arquivo original.  
c - Dispositivos de caractere (transfere informação).  
b - Dispositivos de bloco (Armazenamento). HD, SSD, pendrive.  

## Estuturas de diretórios
Tudo no linux é arquivo.

/bin - Binários do sistema. Arquivos executáveis essenciais para o linux. Todos os usuarios podem executar esse binários.  

/boot - Arquivos essenciais para inicialização dos sistema. Armazena o kernel do linux.  

/dev - Arquivos de dispositivos.  
ex1.: sda, sda1, sda2 - Discos sata.  
ex2.: nvme0, nvme0n1, nvme0n1p1 - Discos nvme.  
ex3.: tty (porta serial).  
ex4.: psaux (mouse).  

/etc - Arquivos de configuração do linux.  
ex1.: cat - Visualiza conteúdo de arquivo.  
ex2.: hostname - Nome do dispositivo.  
ex3.: network - Configurações de rede.  

/home - Contém os diretórios home de cada usuário da máquina.  

/lib - Bibliotecas dinâmicas compartilhadas entre os programas. Módulos do kernel.

/lib64 | /lib32 | libx32 - Bibliotecas do sistema e módulos do kernel linux.  

/lost+found - Serve como um local de recuperação para arquivos e fragmentos de dados que se tornam inacessíveis devido à corrupção do sistema de arquivos, crashes repentinos ou desligamento incorreto.  

/media - Ponto de monstagem para dispositivos de mídias removíveis.  
ex1.: pendrive  
ex2.: cdrom  

/mnt - Ponto de montagem temporário.  

/opt - Local padrão reservado para pacotes de software de aplicativos adicionais que não fazem parte do sistema operacional principal.

/proc - Informações virtuais dinâmicas do kernel e processos.  
ex1.: cpuinfo  
ex2.: uptime  

/root - Diretório home do usuário root. Único usuário que tem diretório fora do /home.  

/run - Informação de tudo que está sendo executado desde o útimo boot. Arquivos temporários.  

/sbin - Binários essenciais de uso exclusivo do root.  
ex1.: useradd - Adiciona usuário  
ex2.: deluser - Deleta usuário  
ex3.: shutdown - Desliga dispositivo  

/srv - Local centralizado para arquivos que são servidos a usuários ou clientes através da rede.  
ex1.: conteúdo web  
ex2.: arquivos FTP  

/sys - Fornece uma visão estruturada e hierárquica das estruturas de dados do kernel, dispositivos de hardware, drivers e recursos do sistema.  
ex1.: controle de energia e bateria  
ex2.: brilho de tela  

/tmp - Arquivos temporários. Todo conteúdo armazenado é removido a cada boot.  

/usr - Unix System Resources. É aqui que ficam os executáveis e bibliotecas de todos os principais programas instalados.  

/usr/bin - Armazena executáveis de quase todos os programas instalados pelo usuários.  

/usr/lib - Armazena bibliotecas de quase todos os programas instalados pelo usuários.  

/usr/src - Armazena código fonte de programas.  

/usr/local - É reservada a programas e scripts que você instala manualmente.  
ex1.: script que transfere arquivos entre diretórios.  

/var - Armazena arquivos que mudam frequentemente durante a operação do sistema. Boa prática é mover /var para outro disco para não consumir espaço total do disco do sistema operacional.  
ex1.: /var/logs/  
ex2.: /var/backups/  
ex3.: /var/cache/apt/  
ex4.: /var/lib/docker/  

## Extensões linux
Linux não obriga que os arquivos possuam extensão, mas a organização fica mais simples quando indicado extensão de alguns arquivos.  
.ko - módulos de kernal/drivers  
.so - bibliotecas  
.sh - shell scripts  

## Desligando e reiniciando o Linux  
halt - Desliga a máquina  
reboot - Reinicia a máquina  
shutdown -h now - Desliga a máquina logo após executar o comando  
shutdown -r now - Reinicia a máquina logo após executar o comando  
shutdown -h 18:00 - Desliga a máquinas as 18:00
shutdown -h +30 - Desliga a máquina quando se passar 30 minutos
shutdown -c - Cancela o agendamento de desligar ou reiniciar a máquina  
poweroff - Desliga a máquina  
init 0 - Desliga a máquina  
init 6 - Reinicia a máquina  
