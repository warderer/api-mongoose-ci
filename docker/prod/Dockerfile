# Esta configuración esta pensada para trabajar con Heroku
# Descargar versión de node 12 versión reducida para producción
FROM node:12-slim

WORKDIR /usr/src/app

# Especificamos explicitamente que también se incluya el package-lock.json
# De esta forma es más rápido instalar dependencias por que ya sabe exactamente
# que dependencias especificamente necesita.
COPY package.json package-lock.json ./

# npm ci --production: hace que npm instale a partir de package-lock.json en vez de package.json
# npm cache clean --force: Borra la cache de npm para optimizar espacio
RUN npm ci --production && npm cache clean --force

COPY . .

# El puerto puede ser dinámico, por lo que cuando se cree el puerto
#ARG PORT

#ENV PORT=$PORT

# Indicamos que el entorno es el de producción
ENV NODE_ENV=production


#CMD ["npm", "start"] -> NO se ejecuta con npm.
# Lo anterior hace que NPM encapsule la ejecución y el servidor no sabrá si el servidor "se muere"
# Al ejecutarlo con node, ejecuta un servicio y levanta su propio hilo en el SO, lo que le puede avisar a docker que paso algo
CMD ["node","server.js"]