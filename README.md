# Atividade sobre docker - Compass UOL


# :pushpin: Atividade de aws e docker
- 1.0. Conceitos iniciais
- 2.0. Configurações iniciais:
- 2.1. Modificação da tabela de rotas;
- 2.2. Criação de um grupo de segurança para o Load Balancer;
- 2.3. Modificação no grupo de segurança padrão(default);
- 2.4. Criação de um grupo de destino;
- 2.5. Criação do Balanceador de carga;
- 3.0. Criação de uma instancia EC2;
- 4.0. Configurações na instancia; 

## Conceitos iniciais
* Docker: plataforma Open Source escrito em Go que facilita a criação e administração de contêineres.
* Docker Engine: software base de container que consiste em um servidor Docker daemon.
* Docker Compose: ferramenta responsável pela definição e execução de múltiplos containers com base em script de instalação.
* Docker Machine: ferramenta que possibilita criar e manter ambientes docker em máquinas virtuais, ambientes de nuvem e até mesmo em máquina física.
* Wordpress: sistema de Gerenciamento de Conteúdo.
* MYSQL: sistema gerenciador de banco de dados relacional que é utilizado para gerir bases de dados.

## Configurações iniciais:
* modificação da tabela de rotas: Iniciamente, entramos do sistema: https://us-east-1.console.aws.amazon.com/console/home?region=us-east-1# e efetuamos o login
em seguida, acessamos VPC padrão e clicamos no painel, procurarmos "tabela de rotas", em seguida seleccionamos a sub - rede privada A e modificamos o seu destino e alvo,
por fim, salvamos as alterações.

* Criação de um grupo de segurança para o Load Balancer: clicamos na seção "grupos de segurança", e em "criar grupo de segurança", em seguida, adicionamos nome e descrição ao grupo,
e selecionamos a VPC padrão, por fim, adicionamos as regras de entrada: http -- tcp -- 80 -- 0.0.0.0/0 e salvamos as alterações realizadas.

* Modificação no grupo de segurança padrão(default): na seção de "grupos de segurança", clicamos no grupo padrão(default), clicamos em ações e em "editar regras de entrada", selecionamos a VPC padrão, e adicionamos as regras:
HTTP -- TCP -- 80 -- (grupo de segurança criado para o load balancer) 
NFS -- TCP -- 2049 -- (grupo de segurança padrão(default))
SSH -- TCP -- 22 -- MY IP

* Criação de um grupo de destino: na seção de "grupos de destino", clicamos em "criar grupo", selecionamos "instancias", atribuimos um nome ao grupo, selecionamos uma VPC, adicionamos 200,302 em "códigos de sucesso" nas configurações avançadas,
em seguida clicamos em "proximo" e "criar grupo de destino".

* Criando um balanceador de carga: na seção "Load Balancer", clicamos em "criar load balancer", em seguida, "aplication load balancer", "criar", atribuimos um nome, selecionamos o schema "voltado para a internet", selecionamos a VPC padrão, selecionamos
as zonas : us-east-1a e us-east-1b e as suas sub-redes privateSubnet1A e privateSubnet2B, selecionamos o grupo de segurança criado para o load balancer e clicamos em "criar".

* Criação de uma instancia EC2: no painel do console EC2, clicamos em "executar instancia", adicionamos nome e etiquetas, selecionamos a imagem "Amazon Linux", o tipo da instancia "t3.small", armazenamento GP2 de 16GB, par de chaves e configuramos a rede com: a VPC, sub-rede, firewall e grupo de segurança padrão(default).
no arquivo user.data.sh, criamos o script que irá realizar o processo de instalaçao do docker e docker compose na nossa instancia. 

* Configurações na instancia: na instancia, montamos o NFS dado, criamos o arquivo "docker-compose.yml" para criar o wordpress e o MYSQL, por fim, executamos esse arquivo.

## :construction: Status da atividade
Concluída


