# Instruções para rodar o projeto

## 1. Clone o repositório e entre na pasta do projeto
  
  ```bash
  git clone https://github.com/PedroPiveta/dockerWordpress.git && cd dockerWordpress
  ```

## 2. Use a CLI do docker para criar um swarm e subir os serviços
  ```bash
  docker swarm init
  ```
  ```bash
  docker stack deploy -c docker-swarm.yml <nome_stack>
  ```

## 3. Configuração do wordpress
  * Acesse localhost:8080 no seu navegador e siga as instruções para criar uma conta no wordpress
  * Vá para página de plugins e instale o plugin do Redis
  * Agora precisaremos alterar umas configurações no wp-config.php do contâiner wordpress
    
    ```bash
    docker ps
    ```
    ```bash
    docker exec -it <id_container_wordpress> bash
    ```
  * Instalamos um editor de texto no contâiner
    ```bash
    apt update && apt install nano
    ```
  * Usamos o nano para modificar o wp-config
    ```bash
    nano wp-config.php
    ```
  * Colamos as 3 seguintes linhas no final do arquivo
    ```
    define('WP_CACHE', true);
    define('WP_REDIS_HOST', 'redis');
    define('WP_REDIS_PORT', 6379);
    ```
    `CTRL+O para salvar e CTRL+X para sair do nano`
  * Agora todos nossos serviços estão configurados e você pode acessá-los usando as seguintes portas:
    - Wordpress: localhost:8080
    - Grafana: localhost:3000  `login: admin  senha: admin`
    - Prometehus: localhost:9090
