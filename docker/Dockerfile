# Imagem oficial do PHP
FROM php

# Instala dependências do sistema
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libzip-dev \
    supervisor \
    zip \
    curl \
    nodejs \
    npm \
    && docker-php-ext-install pdo pdo_mysql zip \
    && apt-get clean

# Instala Composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Define diretório de trabalho ANTES de copiar os arquivos
WORKDIR /var/www/html

# Copia o projeto para dentro do container
COPY . .

# Copia configuração do Supervisor
COPY ./docker/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Instala dependências do Laravel e do frontend
RUN composer install
RUN npm install

# Comando para iniciar o Supervisor
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
