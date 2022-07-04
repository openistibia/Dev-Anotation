
# Anotações de desenvolvimento
***Tutorial: Protocol 12.x assets***

### 1. Instalando as bibliotecas basicas de compilação

Para instalar use apt-get

```
sudo apt install -y build-essential cmake git libasio-dev libphysfs-dev liblua5.1-dev libssl-dev libglew-dev libvorbis-dev libopenal-dev zlib1g-dev liblzma-dev nlohmann-json3-dev
```
Se estiver usando o ubuntu na versão 18.04, você vai precisar desta biblioteca
```
sudo apt-get install -y libogg-dev
```
### 2. Instalando biblioteca protobuff manualmente

Protobuff ubuntu apt está desatializado e você tem que baixar e compilar manualmente!

Primeiro, baixe o código fonte:
```
git clone https://github.com/protocolbuffers/protobuf.git
cd protobuf
git checkout v3.19.4 # or find latest stable version

git submodule update --init --recursive
./autogen.sh
```
Agora compile
```
./configure
make
sudo make install
sudo ldconfig # refresh shared library cache.
```
### 3. Instalar g++-11

Verifique a versão do g++
```
g++ -v
```
se a versão não for a versão g++-11, você precisa instalar ela:
```
sudo add-apt-repository -y ppa:ubuntu-toolchain-r/test
sudo apt update
sudo apt install -y g++-11
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-11 110
```

### 4. Instalando otclient

Baixe a sources compile e rode!
```
git clone git://github.com/openistibia/otclient.git
cd otclient && mkdir build && cd build
cmake ..
make
```
## 5. Abrindo o otclient

Depois que tudo finaliar! na pasta raiz do client use.
```
./otclient
```
### 6. Dica

Caso queira acelerar o processo voce pode usar a tag -j para setar a quantidade de nucelos utilizados na compilação!
Exemplo para usar 8 nucelos:
```
make -j8
```
