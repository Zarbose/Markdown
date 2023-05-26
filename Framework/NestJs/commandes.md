# NestJs

Ce document regroupes les commandes permettant de créer une base de projet avec le framework NestJs
NestJs est un framework utilisant NodeJs et permettant de faciliter la création d'API
Page de [Documentation](https://docs.nestjs.com/openapi/introduction)

### Créer un projet et ajouter les nodes modules
```bash
npm i -g @nestjs/cli
nest new .
npm i --save sequelize pg-hstore pg
npm i --save-dev @types/sequelize
npm i dotenv --save
nest g module /core/database
npm install --save @nestjs/config
npm install sequelize-typescript
```

### Créer un token aléatoire en console
```bash
node -e "console.log(require('crypto').randomBytes(256).toString('base64'));"
```

### Exemple pour la création des modules, services, controllers, ...
```bash
nest g module /modules/users
nest g service /modules/users/services
nest g controller /modules/users/controllers
```

### Installations pour un module d'authentification
```bash
nest g module /modules/auth
nest g service /modules/auth/services/auth --flat
nest g controller /modules/auth/controllers/auth --flat
npm install --save @nestjs/passport passport-local
npm install --save-dev @types/passport-local
npm install bcrypt --save
npm install --save @nestjs/jwt passport-jwt
npm install --save-dev @types/passport-jwt
npm install --save @nestjs/passport @nestjs/jwt passport-jwt
npm install --save-dev @types/passport-jwt
```