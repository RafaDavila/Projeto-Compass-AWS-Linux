# Projeto-Compass-AWS-Linux
Primeira atividade proposta pela Compass UOL

Primeira parte: 

Requisitos AWS :
-Gerar uma chave pública para acesso ao ambiente;
-Criar 1 instância EC2 com o sistema operacional Amazon Linux 2 (Família t3.small, 16 GB SSD);
-Gerar 1 Elastic IP e anexar à instância EC2;
-Liberar as portas de comunicação para acesso público: (22/TCP, 111/TCP e UDP, 2049/TCP/UDP, 80/TCP, 443/TCP).

AWS >> Geração de chave pública para acesso ao ambiente

Como podemos criar a chave tanto durante a criação da instância como antes, criaremos antes como manda a atividade, apenas siga os passos:
1) No console AWS, fui ao para o Painel EC2;
2) No menu posicionado ao lado esquerdo da tela, fui até a seção Rede e Segurança e cliquei em Pares de Chaves;
3) Na próxima tela, no lado superior direito, cliquei em Criar par de chaves;
4) Dei um nome a chave;
5) Mantenha as configurações restantes e na opção Formato de arquivo de chave privada, selecionei o formato .ppk, necessário para acessar a instância via Putty(metodo que vou fazer essa atividade)
6) Após criar uma chave, salvei.
![image](https://github.com/RafaDavila/Projeto-Compass-AWS-Linux/assets/113639519/9d4a4745-f252-4aa6-8bf1-ca2c49ea6b51)


AWS >> Criar 1 instância EC2 com o sistema operacional Amazon Linux 2 (Família t3.small, 16 GB SSD) 

1) No painel EC2, desca até achar o botão "Executar instância" e cliquei;
2) Coloquei as tags que foram passadas;
3) Escolhi "Linux" e a versão mostrada abaixo:
![image](https://github.com/RafaDavila/Projeto-Compass-AWS-Linux/assets/113639519/4118982c-535e-4d8d-bf9e-bf37153730ce)
4) Escolhi o tipo de instância "t3.small", como requerido;
5) Coloquei o par de chaves criado anteriormente;
6) Deixei marcado criar um grupo de segurança e Permitir tráfego SSH de qualquer lugar como abaixo:
![image](https://github.com/RafaDavila/Projeto-Compass-AWS-Linux/assets/113639519/d4e82ca5-ba4b-4e57-8e3f-75a46dbf8b2a)
7) Em armazenamento, coloque 1x 16DB de gp2.

AWS >> Gerar 1 Elastic IP e anexar à instância EC2

1) Certifiquei que tinha um GATEAWAY de internet antes;
   
2)Na página do serviço EC2, no menu lateral esquerdo, em Rede e Segurança, fui em "IPs elásticos";

3)Cliquei em Alocar endereço IP elástico;

4)Por padrão, o Grupo de borda de Rede já vem selecionado, assim como o Conjunto de endereços IPv4 públicos da Amazon;

5)Depois da criação, selecione o IP na lista, fui em Ações no menu superior e depois em Associar endereço IP elástico;

6)Selecionei a instância EC2 criada anteriormente;

7)Usei o endereço de IP privado que a AWS coloca como padrão;

8)Marquei a opção Permitir que o endereço IP elástico seja reassociado e clique em Associar.

AWS >> Liberar as portas de comunicação para acesso público 
![image](https://github.com/RafaDavila/Projeto-Compass-AWS-Linux/assets/113639519/9f4a5dcc-aa0a-4967-8ee9-e5218490f327)
1)Na página do serviço EC2, no menu lateral esquerdo, em Rede e Segurança, cliquei em Security groups;

2)Selecione o grupo de segurança que foi criado com a instância EC2;

3)Cliquei em Regras de entrada, na parte inferior, e depois, do lado direito da tela, em Editar regras de entrada;

4)Coloquei as regras conforme passado pela Compass.

Nessa atividade eu usarei o PuTTY, um client SSH gratuito para o Windows, baixei em seu site oficial, tanto no Windows como em uma máquina virtual com Linux, no meu caso, Debian.

PuTTY >> Acessando a instância via PuTTY


1)Com o PuTTY aberto, fui em "Session";
2)Coloquei o DNS público da instância(terminado com "amazonaws.com") em "Host Name (or IP adress)";
3) Em Connection>>SSH>>Auth>>Credentials, em "public-key authentication, na caixa Private Key file for authentication,  em Browse, selecionei o arquivo do par de chaves em formato .ppk;
4) Em "open" no login de usuário, coloquei "ec2-user"

Linux >> Montando o sistema de arquivos do EFS na máquina

1) Antes de tudo, verifiquei por atualizações com sudo yum update -y;
![Captura de tela 2024-03-30 165238](https://github.com/RafaDavila/Projeto-Compass-AWS-Linux/assets/113639519/9428b1fb-bbd9-4eed-bb16-4e34ce1a46f3)
2) Depois, usei o comando sudo yum install -y amazon-efs-utils para o suporte ao NFS;
3) Utilizei o comando sudo mkdir /mnt/efs para criar um diretório local que servirá como ponto de montagem;
4) Criei o /mnt/efs/rafael
5) Para montar o sistema de arquivos, foi para o painel da AWS, e digita "EFS" na barra de pesquisa, chegando nesta página:
 ![image](https://github.com/RafaDavila/Projeto-Compass-AWS-Linux/assets/113639519/7f769a47-ae23-4620-b468-432756bdbe91)
6) Se não tiver um sistema de arquivos, crie um, e então, selecione ele e vá até detalhes, então, "anexar" copie o código de "montar via DNS";

 Linux >> Configurando Apache

 1) Instalei o Apache com o comando sudo yum install httpd -y;
 2) Iniciei o Apache no sistema com o comando sudo systemctl start httpd;
 3) Verifique se o apache está em execução através do comando sudo systemctl status httpd;
![Captura de tela 2024-03-30 172422](https://github.com/RafaDavila/Projeto-Compass-AWS-Linux/assets/113639519/43e94488-1b7a-4519-9477-1b855c919c58)


LINUX >> Criando um script que valide se o serviço está online ou offline e envie o resultado da validação para o seu diretório no NFS

1)Utilizarei o editor "nano" para criar o script;
2)Executei o comando nano service_status.sh para criar e abrir o arquivo do script.
3) Digitei o script:
![Captura de tela 2024-03-30 175339](https://github.com/RafaDavila/Projeto-Compass-AWS-Linux/assets/113639519/ee969015-3afd-42a6-9caf-d3901a8cca03)
4) Ctrl+x para salvar;
5)Estando no diretório onde o script foi criado e ativado, executei o comando ./service_status.sh para executá-lo.
6)Esse documento pode ser lido com o comando cat + nome do documento: cat httpd-online.txt

Linux >> Preparando a execução automatizada do script a cada 5 minutos
1)Digitei o comando EDITOR=nano crontab -e;
2) Digitei a linha */5 * * * * /[caminho de onde está o script/nome do script].Isso fará o loop de 5 minutos;
3)Aguardei alguns minutos e verifiquei se estava certo com o online, como no caso abaixo:
![Captura de tela 2024-03-30 190504](https://github.com/RafaDavila/Projeto-Compass-AWS-Linux/assets/113639519/3d16daa7-7e85-45b4-a94e-e1435e8c65ad)
4)Usei o comando sudo systemctl stop httpd, para deixar offline, então, após alguns minutos, verifiquei novamente:
![Captura de tela 2024-03-30 184624](https://github.com/RafaDavila/Projeto-Compass-AWS-Linux/assets/113639519/7b3fa05d-76d0-4b10-89e0-a3b2ac6744dd)

E assim termina a atividade! Muito aprendizado e boa prática para testar meus conheciementos tanto no painel AWS, como com os comandos Linux.








