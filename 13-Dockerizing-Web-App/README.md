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

## 0 Masuk Ke Folder Baru Project
```sh
cd ~/amin
mkdir latihan-docker-image
cd latihan-docker-image
```

## 1 Inisiasi Project NPM

```sh
npm init
```

## 2 Instalasi Package-Package

```sh
npm install express
```

## 3 Copy Script Backendnya

file : [index.js](./index.js) doang

## 4 Copy dockerfile nya

file : [dockerfile](./dockerfile) doang

## 5 Build dockerfile Jadi Docker Image

```sh
docker build -t pawx-insan:0.1.0 .
```
