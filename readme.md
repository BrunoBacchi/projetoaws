<!DOCTYPE html>
<html lang="pt-BR">
  <head>
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Noto+Sans:ital,wght@0,100..900;1,100..900&display=swap"
      rel="stylesheet"
    />
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Configuração de Servidor Web AWS</title>
    <style>
      body {
        font-family: "Noto Sans", serif;
      }
      img {
        max-width: 80%;
        height: auto;
        display: block;
        margin: 10px auto;
      }
      h1,
      h2,
      h3,
      h4,
      p {
        margin: 10px 0;
        text-align: center;
        font-family: Arial, sans-serif;
      }
      img {
        padding-bottom: 5%;
      }
    </style>
  </head>
  <body>
    <h1>Configuração de Servidor Web AWS</h1>
    <h2>Etapa 1: Configuração do Ambiente</h2>
    <h3>1. Criar uma VPC na AWS</h3>
    <p>
      Configurar a VPC com 2 sub-redes públicas e 2 privadas, além de um
      Internet Gateway.
    </p>
    <img
      src="Parte 1 Projeto - Criando VPC e ECS2/VPC criando.PNG"
      alt="Screenshot da configuração da VPC"
    />

    <h3>2. Criar uma instância EC2</h3>
    <h4>
      Selecionar uma AMI baseada em Linux, associar a uma sub-rede pública e
      configurar um Security Group.
    </h4>
    <p>Clicando em Instances, vamos em "Launch Instances"</p>
    <img
      src="Parte 1 Projeto - Criando VPC e ECS2/Print 2 - Criando EC2.PNG"
      alt="Screenshot da criação da instância EC2"
    />
    <h3>- Escolha a versão ubuntu</h3>
    <img
      src="Parte 1 Projeto - Criando VPC e ECS2/Print 3 - Escolhendo o Ubuntu.PNG"
      alt="Screenshot da escolha do ubuntu"
    />
    <h3>1- Descendo um pouco, marque a VPC - Required com a VPC que criamos</h3>
    <h4>
      2- Em Subnets, marcamos uma subnet com ip público: Exemplo 10.0.0.0/20
    </h4>
    <h4>3- Em Auto-assign public IP marque Enable</h4>
    <img
      src="Parte 1 Projeto - Criando VPC e ECS2/Print 4 - Escolhendo a VPC criada, adicionando IP Pública e em security group escolhendo ela.PNG"
      alt="Escolhendo a VPC criada"
    />

    <h3>3. Acessar a instância via SSH</h3>
    <p>
      Vá em instances de novo, Marque sua instancia e abaixo vá em Security.
    </p>
    <img
      src="Parte 1 Projeto - Criando VPC e ECS2/Print 5 - Clicando em EC2 e depois em instancias, marcamos a nossa instancia e vamos em Security.PNG"
      alt="Screenshot do acesso via SSH"
    />

    <p>Em inbound Rules, clique em edit inbound rules.</p>
    <img
      src="Parte 1 Projeto - Criando VPC e ECS2/Print 6 - Vamos em inbound rules e vamos clicar em Edit inbound rules.PNG"
      alt=""
    />

    <p>
      Em edit inbound rules, crie em add rule e crie um HTTP e um SSH, clique em
      source e marque com anywhere o HTTP e o SSH com seu IP.
    </p>
    <img
      src="Parte 1 Projeto - Criando VPC e ECS2/Print 7 - Em edit inbound Rules crie em add rule um HTTP com anywhere ip, e um SSH com seu ip.PNG"
      alt=""
    />

    <p>
      Volte para instances e vá para Outbound rules, crie 2 rules, HTTP e HTTPS
      e coloque anywhere nos dois.
    </p>
    <p>E com isso a primeira parte está feita!</p>
    <img
      src="Parte 1 Projeto - Criando VPC e ECS2/Print 8 - Volte e vá para Outbound rules, crie 2 rules, HTTP e HTTPs em Anywhere ip.PNG"
      alt=""
    />

    <h2>Etapa 2: Configuração do Servidor Web</h2>
    <p>
      1 Baixe o WSL e o Ubuntu mais recente pelo Microsoft Store. <br /><br />

      2 Baixe o Visual Studio Code e em extensões, baixe o remote WSL.
      <br /><br />

      3 Vá ao canto inferior esquerdo e clica no sinal de "><" <br /><br />

      4 Marque o "Connect to WSL" e faça seu login <br /><br />

      5 Volte para o navegador, em EC2, Marque sua instancia em instancias,
      clique em Connect. <br /><br />

      6 Copie o exemplo, a última linha <br /><br />

      7 Crie um terminal no Visual Studio Code, e cole o exemplo, e logue na sua
      instancia. <br /><br />

      8 Entre no wsl para acessar o dektop para trazer a chave pem para o
      servidor. <br /><br />

      <code>cd /mnt/c/Users/"Seu usuário"/Desktop/</code> <br /><br />

      Move para o WSL <br /><br />

      <code>mv chave3.pem /home/"Seu usuário"/</code> <br /><br />

      Feito.
    </p>
    <img
      src="Parte 2 - Configurando ambiente/1 Print 1 entrando no servidor.PNG"
      alt="Screenshot da instalação do Nginx"
    />

    <h2>Etapa 3: Instalação do Nginx</h2>
    <p>
      buscar e instalar atualizações: <br /><br />

      <code>sudo apt update</code> <br /><br />

      <code>sudo apt upgrade -y</code> <br /><br />

      fazer a instalação do ngnix: <br /><br />

      <code>sudo apt install nginx</code> <br /><br />

      verificar se ele está ativo: <br /><br />

      <code>sudo systemctl status nginx</code> <br /><br />

      para alterar a pagina da web: <br /><br />

      <code>cd var/www/html/index.html</code> <br /><br />

      edite o arquivo com nano index.html <br /><br />

      EDITE O que quiser, pois este será o html que aparecerá na sua página,
      aqui esle está funcionando.
    </p>
    <img
      src="Parte 3 - Instalação do Nginx/Print Nginx funcionando.PNG"
      alt="Screenshot da página HTML criada"
    />

    <h2>Parte 4: Monitoramento</h2>
    <p>
      Depois de logado na máquina pelo VSCODE, dê os comandos: <br /><br />

      <code>sudo su</code><br /><br />

      <code>cd /var/www/html</code><br /><br />

      (dê um "ls" para para mostrar os arquivos) <br /><br />

      (crie um arquivo, eu dei o nome de monitor.sh, veja abaixo) <br /><br />

      <code>nano monitor.sh</code> (vai criar o arquivo .sh e utilizar o editor
      nano) <br /><br />

      cole o script do outro txt. <br /><br /><br />

      se observar bem, nas primeiras linhas está: <br />
      "SITE_URL" <br />
      "LOG_FILE" <br />
      "DISCORD_WEBHOOK" <br /><br />

      o SITE_URL você deverá por o ip público que sua instancia EC2 tem.
      <br /><br />

      - o LOG_FILE você deverá criar um arquivo, no caso o meu eu criei como
      monitoramento.log, você deverá criar no mesmo caminho utilizando o nano, e
      deixo o arquivo novo em branco. <br /><br />

      - o DISCORD_WEBHOOK, é o aplicativo de mensagem que utilizei para
      notificar se o servidor está funcionando, você deverá criar um grupo,
      selecionar um canal de mensagem, em configurações > integrações > web
      hooks > e novo web hook > clicar no boot escolhido, "Copiar URL do
      webhook" e substituir a que está no script <br /><br />
    </p>
    <div style="text-align: center">
      <a href="Parte 4 - Monitoramento/2 Script do monitoramento.txt">
        Aqui está o Script</a
      >
    </div>
    <img
      src="Parte 4 - Monitoramento/monitor sh.PNG"
      alt="Screenshot da configuração do Nginx"
    />

    <h2>Etapa 2: Crontab</h2>
    <p>
      Vamos utilizar o contrab pois ele será o responsável por executar e
      notificar repetidamente para nós, siga o passo a passo: <br /><br />

      digite no terminal: <br />

      <code>crontab -e</code> <br /><br />

      copie e cole este código abaixo no final da linha do crontab -e <br />
      <br />

      <code>*/1 * * * * /var/www/html/monitor.sh</code> <br />
      <br />

      salve o arquivo e volte para onde o monitor.sh está
      <code>cd /var/www/html/</code> <br /><br />

      transforme o monitor.sh em executável <br /><br />
      <code>chmod +x monitor.sh</code> <br /><br />

      execute o arquivo monitor.sh <code>(./ monitor.sh)</code> <br /><br />

      todos os preparativos para a automação estão feitos, para conferir, vá em
      <code>/var/log/monitoramento.log</code> <br /><br />
      e entre no arquivo usando o nano, e vejá se está notificando. <br /><br />
    </p>
    <img src="Parte 4 - Monitoramento/monitoramento log.PNG" alt="" />

    <p>
      caso queira ver de outra forma, entre no discord e no grupo onde você
      criou com o bot, e vejá se está notificando.
    </p>
    <img
      src="Parte 4 - Monitoramento/discord.PNG"
      alt="Screenshot do script de monitoramento"
    />
  </body>
</html>
