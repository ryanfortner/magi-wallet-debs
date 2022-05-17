# Raspberry Pi Magi Wallet Setup
For RPiOS (Raspberry Pi 4 tested) 64 bit only.

I suggest you increase the swapfile: https://singleboardbytes.com/645/install-magi-wallet-raspberry-pi-4.htm

Clone my fork of the wallet. `git clone https://github.com/ryanfortner/magi`

Enter the wallet directory. `cd magi`

For gui wallet:
```
qmake m-wallet.pro BDB_INCLUDE_PATH=/opt/local/db-4.8.30.NC/include BDB_LIB_PATH=/opt/local/db-4.8.30.NC/lib BDB_LIB_SUFFIX=-4.8
make
```

For magid I added berkeley to make file call:
make -f makefile.unix xCPUARCH=aarch64 CXXFLAGS='-I /opt/local/db-4.8.30.NC/include -L /opt/local/db-4.8.30.NC/lib'

dependencies
```bash
sudo apt-get install build-essential -y
sudo apt-get install libssl-dev -y
#sudo apt-get install libdb4.8-dev
#sudo apt-get install libdb4.8++-dev
sudo apt-get install libgmp-dev -y
sudo apt-get install libminiupnpc-dev -y
sudo apt-get install libboost-all-dev -y
sudo apt-get install libprotobuf-dev libqrencode-dev -y
sudo apt-get install qtchooser -y
sudo apt-get install qt5-qmake -y
sudo apt-get install qtpositioning5-dev -y
sudo apt-get install qttools5-dev-tools -y
```

berkeley-db compile instructions
```bash
wget 'http://download.oracle.com/berkeley-db/db-4.8.30.NC.tar.gz'
# Verify source
echo '12edc0df75bf9abd7f82f821795bcee50f42cb2e5f76a6a281b85732798364ef db-4.8.30.NC.tar.gz' | sha256sum -c
tar -xzvf db-4.8.30.NC.tar.gz
cd db-4.8.30.NC/build_unix
# Build and install DB4.8 under /opt/local/db-4.8.30.NC
../dist/configure --disable-shared --enable-cxx --disable-replication --with-pic --prefix=/opt/local/db-4.8.30.NC --build=aarch64-unknown-linux-gnu
make
sudo make install
```
