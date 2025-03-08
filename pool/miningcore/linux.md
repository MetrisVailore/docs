
# Installation of Mining pool miningcore

git clone https://github.com/oliverw/miningcore (git should be installedd btw)
cd miningcore

## Wsl or Linux

updating and installing dependecies 
```bash
   sudo apt update
   sudo apt install -y postgresql postgresql-contrib git cmake build-essential libssl-dev pkg-config libboost-all-dev libsodium-dev libzmq5 libzmq3-dev nginx gcc g++ make
```
### Install dotnet 6 (no longer supported by microsoft)

```bash
  sudo apt remove --purge dotnet* aspnetcore* netstandard*
  sudo apt autoremove
  sudo apt clean
```

### To avoid installing conflicting packages from different sources, create a file with priorities for Microsoft packages:

```bash
  echo -e "Package: dotnet* aspnet* netstandard*\nPin: origin \"packages.microsoft.com\"\nPin-Priority: -10" | sudo tee /etc/apt/preferences.d/99microsoft-dotnet.pref
```

### And finally install dotnet 6
```bash
  sudo apt update
  sudo apt install -y dotnet-sdk-6.0
```

### Database setup

```bash
   sudo -u postgres psql
   CREATE ROLE miningcore WITH LOGIN ENCRYPTED PASSWORD 'your-secure-password';
   CREATE DATABASE miningcore OWNER miningcore;
   \q
   sudo -u postgres psql -d miningcore -f /path/to/miningcore/src/Miningcore/Persistence/Postgres/Scripts/createdb.sql
```

### Compile
Depending on your OS Version run either of these scripts:

```./build-debian-11.sh``` or ```./build-ubuntu-20.04.sh``` or ```./build-ubuntu-21.04.sh```

