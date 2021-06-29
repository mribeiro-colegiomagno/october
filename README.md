# Instalação do Apache

Instale o Apache usando o gerenciador de pacotes do Ubuntu, apt:

    sudo apt update
    sudo apt install apache2

# Firewall
Ativar o Firewall:

    sudo ufw app list

Você verá um resultado como este:

Output
Available applications:
  Apache
  Apache Full
  Apache Secure
  OpenSSH

Para permitir apenas o tráfego na porta 80, use o perfil Apache:

    sudo ufw allow in "Apache"

 Você pode verificar a alteração com:

    sudo ufw status

# Instalação do Mysql

Novamente, utilize o apt para adquirir e instalar este software:

    sudo apt install mysql-server
    sudo mysql_secure_installation


Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 1
Digite 1

Digite 'Yes' para as outras perguntas

# Instalação do PHP

Para instalar esses pacotes, execute:

    sudo apt install php libapache2-mod-php php-mysql

Assim que a instalação terminar, você pode executar o seguinte comando para confirmar sua versão PHP:

    php -v

# Comandos Mysql
Criar o database:

    CREATE DATABASE nomedabase;

Agora, crie um usuário e lhe conceda privilégios completos sobre o banco de dados personalizado que acabou de criar. 

    CREATE USER 'usuario'@'%' IDENTIFIED WITH mysql_native_password BY 'Senha';

Agora, precisamos dar a este usuário permissão para o banco de dados magno:

    GRANT ALL ON usuario.* TO 'nomedabase'@'%';

Em seguida, saia do shell do MySQL:

    exit

Agora você pode testar se o novo usuário tem as permissões adequadas fazendo login no console MySQL novamente:
Observe a flag -p neste comando, a qual irá solicitar a senha utilizada ao criar o usuário .
Após fazer login no console do MySQL, confirme que você tem acesso ao banco de dados:

    mysql -u usuario -p

importar arquivo sql

    use nomedabase;
    source /var/www/html/dump.sql ;
    show tables;

# FTP do conteúdo

Subir conteúdo da pasta para:

    /var/www/html/

# Permissões dos diretórios

    sudo chown -R www-data:www-data /var/www/html/vendor
    sudo chown -R www-data:www-data /var/www/html/storage

# Arquivo de credenciais  .Env

    APP_DEBUG=true
    APP_URL=http://seu.ip.local.aqui
    DB_CONNECTION=mysql
    DB_HOST=localhost
    DB_PORT=3306
    DB_DATABASE='nomedabase'
    DB_USERNAME='usuario'
    DB_PASSWORD='Senha'
    
 # Arquivo de configuração apache2.conf
 
 
 Edite o arquivo apache2.conf
 
    sudo nano /etc/apache2/apache2.conf
    
Localize o trecho: 

    <Directory /var/www/html>
        Options Indexes FollowSymLinks
        AllowOverride None
        Require all granted
    </Directory>
    
e mude para;

    <Directory /var/www/html>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
    
então,

    sudo service apache2 restart
 
