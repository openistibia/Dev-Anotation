
# Anotações de desenvolvimento
***Tutorial: Protocol 12.x assets***

### 1. Instalando as bibliotecas basicas de compilação

Para instalar use apt-get

```
sudo apt update
sudo apt dist-upgrade
sudo apt install git cmake build-essential autoconf libtool ca-certificates curl zip unzip tar pkg-config ninja-build libglew-dev libx11-dev ccache linux-headers-$(uname -r)
```
Atualizando o CMAKE
```
sudo apt remove --purge cmake
hash -r
sudo apt install snapd
sudo snap install cmake --classic
cmake --version
```
Atualizando o GCC
```
sudo add-apt-repository ppa:ubuntu-toolchain-r/test -y
sudo apt update
sudo apt install gcc-11 g++-11
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-11 100 --slave /usr/bin/g++ g++ /usr/bin/g++-11 --slave /usr/bin/gcov gcov /usr/bin/gcov-11
sudo update-alternatives --set gcc /usr/bin/gcc-11
gcc-11 --version
g++-11 --version
```
### 2. Instalando VCPKG manualmente
```
cd ~
git clone https://github.com/microsoft/vcpkg
cd vcpkg
./bootstrap-vcpkg.sh
cd ..
```
### 4. Instalando otclient

Baixe a sources compile e rode!
```
git clone git://github.com/openistibia/otclient.git
cd otclient && mkdir build && cd build
cmake -DCMAKE_TOOLCHAIN_FILE=~/vcpkg/scripts/buildsystems/vcpkg.cmake .. --preset linux-release
cmake --build linux-release
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
