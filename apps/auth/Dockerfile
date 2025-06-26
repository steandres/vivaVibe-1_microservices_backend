FROM node:18-alpine AS development

# Instala Nest CLI globalmente
RUN npm install -g @nestjs/cli

# Establece directorio de trabajo
WORKDIR /usr/src/app

# Copiá todo el proyecto
COPY . .

# Instalá TODAS las dependencias del monorepo
RUN npm install

# Compilá solo el microservicio de auth
RUN npm run build auth

FROM node:18-alpine AS production

WORKDIR /usr/src/app

# Copiá archivos ya compilados desde el build anterior
COPY --from=development /usr/src/app/dist ./dist
COPY package.json package-lock.json ./
RUN npm install --only=production

CMD ["node", "dist/apps/auth/main"]
