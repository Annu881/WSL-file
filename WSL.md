## Installation on Windows (WSL)#### Setting up WSL
1. Install WSL (Windows Subsystem for Linux) if not already installed. Follow the [official guide](https://learn.microsoft.com/en-us/windows/wsl/install).
   - Install Ubuntu as the default distribution (you can choose another Linux distribution, but these instructions assume Ubuntu).
     2. Open a terminal and update your system:
   ```bash
   sudo apt update && sudo apt upgrade -y
   3. Set up WSL2 as the default version:
   ```powershell
   wsl --set-default-version 2
   Cloning From GitHub
To clone the repository, either use the Git GUI if you have one installed or enter the following commands:

git clone https://github.com/CircuitVerse/CircuitVerse.git --recursive
cd CircuitVerse
Note: If you want to contribute, first fork the original repository and clone your forked repository into your local machine. If you don't do this, you will not be able to make commits or change any files.

git clone https://github.com/<username>/CircuitVerse.git --recursive
cd CircuitVerse
Use git submodule update --init to get the contents of the submodule if you missed using the --recursive option while cloning the repository or if you have already done so.
Dependencies
Installation guide link and commands has been added to each dependency. You can skip the installation of the dependency if it is already installed.

Git - using a GUI such as SourceTree or GitHub Desktop can help
sudo apt install git
RVM
sudo apt install curl gnupg
gpg --keyserver keyserver.ubuntu.com --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
curl -sSL https://get.rvm.io | bash -s stable
Ruby 3.2.1
rvm install 3.2.1
rvm use 3.2.1
Redis 7.0 [atleast]
sudo apt install lsb-release curl gpg
curl -fsSL https://packages.redis.io/gpg | sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/redis.list
sudo apt-get update
sudo apt-get install redis
ImageMagick - Image manipulation library
sudo apt install imagemagick
Node.js 16.x
curl -sL https://deb.nodesource.com/setup_16.x | sudo bash
sudo apt-get update && sudo apt-get install -y nodejs
Yarn
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update && sudo apt install -y yarn
CMAKE
sudo apt install cmake
OpenSSL
sudo apt install openssl
libpq-dev
sudo apt-get install libpq-dev
PostgreSQL (12) - Database
sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql.service
sudo systemctl enable postgresql.service
   
   ```---#### Setup
> **Note:** PostgreSQL and Redis *must* be running. PostgreSQL must be configured with a default user.1. Install Ruby bundler:
   ```bash
   gem install bundler
   ```2. Install Ruby dependencies:
   ```bash
   bundle install
   ```3. Install Yarn dependencies:
   ```bash
   yarn
   ```4. Configure your PostgreSQL database in `config/database.yml` (copy `config/database.example.yml` for the template):
   ```bash
   cp config/database.example.yml config/database.yml
   ```
   - **Note:** Update the Postgres credentials to match your running database.5. Create database:
   ```bash
   bundle exec rails db:create
   ```6. Run database migrations:
   ```bash
   bundle exec rails db:migrate
   ```7. Seed the database with some data:
   ```bash
   bundle exec rails db:seed
   ```8. Generate RSA keypairs:
   ```bash
   openssl genrsa -out ./config/private.pem 2048
   openssl rsa -in ./config/private.pem -outform PEM -pubout -out ./config/public.pem
   ```9. Run the application server, background job queue, and asset compiler:
   ```bash
   bin/dev
   ```Navigate to `localhost:3000` in your web browser to access the website.---#### Additional Notes for WSL
- Install `libssl-dev` for OpenSSL development headers if missing:
   ```bash
   sudo apt install libssl-dev
   ```- If you face issues with file permissions or file changes not reflecting, ensure you are using WSL2 and the project directory is located within the WSL filesystem (`/home`), not the Windows file system (`C:\`).
learn.microsoft.comlearn.microsoft.com
Install WSL
Install Windows Subsystem for Linux with the command, wsl --install. Use a Bash terminal on your Windows machine run by your preferred Linux distribution - Ubuntu, Debian, SUSE, Kali, Fedora, Pengwin, Alpine, and more are available. (93 kB)
https://learn.microsoft.com/en-us/windows/wsl/install
