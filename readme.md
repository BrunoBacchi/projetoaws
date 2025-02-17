# Configuração de Servidor Web AWS 🚀

## Etapa 1: Configuração do Ambiente

### 1. Criar uma VPC na AWS
Configurar a VPC com 2 sub-redes públicas e 2 privadas, além de um Internet Gateway.

![Screenshot da configuração da VPC](Parte%201%20Projeto%20-%20Criando%20VPC%20e%20ECS2/VPC%20criando.PNG)

### 2. Criar uma instância EC2
Selecionar uma AMI baseada em Linux, associar a uma sub-rede pública e configurar um Security Group.

Clicando em Instances, vá em "Launch Instances".

![Screenshot da criação da instância EC2](Parte%201%20Projeto%20-%20Criando%20VPC%20e%20ECS2/Print%202%20-%20Criando%20EC2.PNG)

Escolha a versão Ubuntu:

![Screenshot da escolha do Ubuntu](Parte%201%20Projeto%20-%20Criando%20VPC%20e%20ECS2/Print%203%20-%20Escolhendo%20o%20Ubuntu.PNG)

Configuração de rede:
1. Marque a VPC criada anteriormente.
2. Escolha uma subnet com IP público (exemplo: 10.0.0.0/20).
3. Em "Auto-assign public IP", marque "Enable".

![Escolhendo a VPC criada](Parte%201%20Projeto%20-%20Criando%20VPC%20e%20ECS2/Print%204%20-%20Escolhendo%20a%20VPC%20criada,%20adicionando%20IP%20P%C3%BAblica%20e%20em%20security%20group%20escolhendo%20ela.PNG)

### 3. Acessar a instância via SSH
Vá em "Instances" novamente, marque sua instância e clique em "Security".

![Screenshot do acesso via SSH](Parte%201%20Projeto%20-%20Criando%20VPC%20e%20ECS2/Print%205%20-%20Clicando%20em%20EC2%20e%20depois%20em%20instancias,%20marcamos%20a%20nossa%20instancia%20e%20vamos%20em%20Security.PNG)

Em "Inbound Rules", clique em "Edit inbound rules".

![Screenshot da configuração do inbound rules](Parte%201%20Projeto%20-%20Criando%20VPC%20e%20ECS2/Print%206%20-%20Vamos%20em%20inbound%20rules%20e%20vamos%20clicar%20em%20Edit%20inbound%20rules.PNG)

Adicione as regras:
- **HTTP** com "Anywhere".
- **SSH** com seu IP.

![Screenshot das regras de inbound](Parte%201%20Projeto%20-%20Criando%20VPC%20e%20ECS2/Print%207%20-%20Em%20edit%20inbound%20Rules%20crie%20em%20add%20rule%20um%20HTTP%20com%20anywhere%20ip,%20e%20um%20SSH%20com%20seu%20ip.PNG)

Para "Outbound Rules", adicione HTTP e HTTPS com "Anywhere".

![Screenshot das regras de outbound](Parte%201%20Projeto%20-%20Criando%20VPC%20e%20ECS2/Print%208%20-%20Volte%20e%20v%C3%A1%20para%20Outbound%20rules,%20crie%202%20rules,%20HTTP%20e%20HTTPs%20em%20Anywhere%20ip.PNG)

## Etapa 2: Configuração do Servidor Web

1. Baixe o WSL e o Ubuntu mais recente pela Microsoft Store.
2. Instale o Visual Studio Code e a extensão "Remote - WSL".
3. No VS Code, clique no ícone "><" e selecione "Connect to WSL".
4. No EC2, marque sua instância e clique em "Connect".
5. Copie a última linha do exemplo de conexão SSH.
6. No terminal do VS Code, cole o comando e conecte-se à instância.

```bash
cd /mnt/c/Users/"Seu usuário"/Desktop/
mv chave3.pem /home/"Seu usuário"/
```

![Screenshot do acesso ao servidor](Parte%202%20-%20Configurando%20ambiente/1%20Print%201%20entrando%20no%20servidor.PNG)

## Etapa 3: Instalação do Nginx

Atualizar pacotes e instalar o Nginx:

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install nginx
sudo systemctl status nginx
```

Para alterar a página da web:
```bash
cd /var/www/html/
nano index.html
```

![Screenshot da página HTML criada](Parte%203%20-%20Instala%C3%A7%C3%A3o%20do%20Nginx/Print%20Nginx%20funcionando.PNG)

## Etapa 4: Monitoramento

Depois de logado na máquina pelo VS Code, execute:
```bash
sudo su
cd /var/www/html/
nano monitor.sh
```

Cole o script do monitoramento e personalize os campos:
- `SITE_URL`: coloque o IP público da sua instância EC2.
- `LOG_FILE`: crie um arquivo `monitoramento.log` e deixe em branco.
- `DISCORD_WEBHOOK`: crie um webhook no Discord para receber notificações.

[Script de monitoramento](Parte%204%20-%20Monitoramento/2%20Script%20do%20monitoramento.txt)

![Screenshot da configuração do monitoramento](Parte%204%20-%20Monitoramento/monitor%20sh.PNG)

## Etapa 5: Configuração do Crontab

Edite o crontab:
```bash
crontab -e
```

Adicione a linha:
```bash
*/1 * * * * /var/www/html/monitor.sh
```

Torne o script executável e execute-o:
```bash
chmod +x monitor.sh
./monitor.sh
```

Verifique os logs:
```bash
cat /var/log/monitoramento.log
```

![Screenshot do log de monitoramento](Parte%204%20-%20Monitoramento/monitoramento%20log.PNG)

Se quiser conferir as notificações, acesse o Discord e verifique o canal configurado.

![Screenshot do Discord](Parte%204%20-%20Monitoramento/discord.PNG)

---

