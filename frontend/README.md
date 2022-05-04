# Frontend

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 13.3.4.

## Installation - Ubuntu
```sh

curl -sL https://deb.nodesource.com/setup_16.x | sudo bash -
sudo apt -y install nodejs
npm install -g @angular/cli
```

## .dockerignore
Add directories and files which are not required for docker image creation.
e.g node_modules, .vscode, README.md, etc.

## Generate angular production build and create an image
### Dockerfile
```sh
#stage 1
FROM node:16.15 as build
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . /app
RUN npm run build --prod

#stage 2
FROM nginx:alpine
COPY --from=build /app/dist/frontend /usr/share/nginx/html
```

### Create doker build
```sh
# cd frontend
docker build -t <image-name>:tag .
```

### Run docker container
```sh
# cd frontend
docker run -d -p 8080:80 --name <container-name> <image-name>:<tag>
```

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The application will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via a platform of your choice. To use this command, you need to first add a package that implements end-to-end testing capabilities.

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.io/cli) page.
