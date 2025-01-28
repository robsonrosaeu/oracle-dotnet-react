# Use a imagem mais recente do Node.js como base
FROM node:current-alpine AS build

# Defina o diretório de trabalho dentro do container
WORKDIR /app

# Copie os arquivos necessários para o container
COPY package.json package-lock.json ./

# Instale as dependências
RUN npm install

# Copie o restante dos arquivos do projeto
COPY . .

# Compile a aplicação para produção
RUN npm run build
    
# Use a imagem do Nginx para servir os arquivos estáticos
FROM nginx:alpine

# Copie o arquivo de configuração do Nginx
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copie os arquivos estáticos do build para o diretório de publicação do Nginx
COPY --from=build /app/dist /usr/share/nginx/html

# Exponha a porta 80
EXPOSE 80

# Comando para iniciar o Nginx
CMD ["nginx", "-g", "daemon off;"]
