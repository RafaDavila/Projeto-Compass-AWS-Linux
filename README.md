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
1) No console AWS, vá para o Painel EC2;
2) No menu posicionado ao lado esquerdo da tela, vá até a seção Rede e Segurança e clique em Pares de Chaves;
3) Na próxima tela, no lado superior direito, clique em Criar par de chaves;
4) De um nome a chave;
5) Mantenha as configurações restantes e na opção Formato de arquivo de chave privada, selecione o formato .ppk, necessário para acessar a instância via Putty(metodo que vou fazer essa atividade)
6) Clique em criar chave, e guarde em um lugar seguro.
![image](https://github.com/RafaDavila/Projeto-Compass-AWS-Linux/assets/113639519/9d4a4745-f252-4aa6-8bf1-ca2c49ea6b51)


AWS >> Criar 1 instância EC2 com o sistema operacional Amazon Linux 2 (Família t3.small, 16 GB SSD) 

1) No painel EC2, desca até achar o botão "Executar instância" e clique;
2) Escolha o para a instância, e coloque as tags que foram passadas;
3) Escolha "Linux e a versão mostrada abaixo:
![image](https://github.com/RafaDavila/Projeto-Compass-AWS-Linux/assets/113639519/4118982c-535e-4d8d-bf9e-bf37153730ce)
4) Escolha o tipo de instância "t3.small", como requerido;
5) Escolha o par de chaves criado anteriormente;
6) Deixe marcado criar um grupo de segurança e Permitir tráfego SSH de qualquer lugar como abaixo:
![image](https://github.com/RafaDavila/Projeto-Compass-AWS-Linux/assets/113639519/d4e82ca5-ba4b-4e57-8e3f-75a46dbf8b2a)
7) Em armazenamento, coloque 1x 16DB de gp2.

AWS >> Gerar 1 Elastic IP e anexar à instância EC2

1) Certifique que tenha um GATEAWAY de internet antes;
2)Na página do serviço EC2, no menu lateral esquerdo, em Rede e Segurança, clique em IPs elásticos;
3)Clique em Alocar endereço IP elástico;
4)Por padrão, o Grupo de borda de Rede já vem selecionado, assim como o Conjunto de endereços IPv4 públicos da Amazon;
Clique em Alocar;
5)Depois da criação, selecione o IP na lista, clique em Ações no menu superior e depois em Associar endereço IP elástico;
6)Selecione a instância EC2 criada anteriormente;
7)Coloque o endereço de IP privado que a AWS irá indicar;
8)Marque a opção Permitir que o endereço IP elástico seja reassociado e clique em Associar.

AWS >> Liberar as portas de comunicação para acesso público 
![image](https://github.com/RafaDavila/Projeto-Compass-AWS-Linux/assets/113639519/9f4a5dcc-aa0a-4967-8ee9-e5218490f327)
1)Na página do serviço EC2, no menu lateral esquerdo, em Rede e Segurança, clique em Security groups;
2)Selecione o grupo de segurança que foi criado com a instância EC2;
3)Clique em Regras de entrada, na parte inferior, e depois, do lado direito da tela, em Editar regras de entrada;
4)Coloque as regras conforme passado pela Compass.

Nessa atividade eu usarei o PuTTY, um client SSH gratuito para o Windows, baixei em seu site oficial, tanto no Windows como em uma máquina virtual com Linux, no meu caso, Debian.

PuTTY >> Acessando a instância via PuTTY


1)Com o PuTTY aberto, vá em "Session";
2)Coloque o DNS público da instância(terminado com "amazonaws.com") em "Host Name (or IP adress)
3)Vá em Connection>>SSH>>Auth>>Credentials, em "public-key authentication, na caixa Private Key file for authentication, clique em Browse, selecione o arquivo do par de chaves em formato .ppk;
4)Clique em "open" no login de usuário, coloque "ec2-user"

Linux >> Montando o sistema de arquivos do EFS na máquina


