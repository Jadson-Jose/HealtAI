FROM node:16-alpine

# Define o diretório de trabalho
WORKDIR /app

# Copia os arquivos package.json e package-lock.json (se houver)
COPY package.json package-lock.json* ./

# Instala as dependências
RUN npm install

# Copia o restante do código
COPY . .

# Expõe a porta (ajuste se necessário)
EXPOSE 3000

# Inicia a aplicação
CMD ["npm", "start"]
