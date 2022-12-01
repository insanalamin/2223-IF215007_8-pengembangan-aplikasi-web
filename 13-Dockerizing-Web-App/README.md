# Instalasi Node menggunakan NVM (1 grup 1 instalasi)

## 1 Install NVM
```sh
curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash 
```

## 2 Refresh .bashrc
```sh
. ~/.bashrc   
```

## 3 Install Node versi 16
```sh
nvm install 16
```

## 4 Gunakan Node versi 16
```sh
nvm use 16
```

# Build Docker Image dari Source Code

## 1 Inisiasi Project NPM

```sh
npm init
```

## 2 Instalasi Package-Package

```sh
npm install express
```

## 3 Coding Script Backendnya

file : [server.js](./server.js) doang

## 4 Tulis dockerfile nya

file : [dockerfile](./dockerfile) doang

## 5 Build dockerfile Jadi Docker Image

```sh
docker build -t pawx-insan:0.1.0 .
```
