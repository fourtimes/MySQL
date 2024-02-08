To install MySQL on macOS, you can use Homebrew, which is a popular package manager for macOS. Follow these steps:

**1. Install Homebrew:**

If you don't have Homebrew installed, you can install it by running the following command in your terminal:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
**2. Install MySQL:**

Once Homebrew is installed, you can use it to install MySQL. Run the following command:

```bash
brew install mysql
```
**3. Start MySQL:**

After the installation is complete, you can start the MySQL service. Use the following command:

```bash
brew services start mysql
```
This command will start MySQL and set it up to start automatically on system boot.

**4. Secure MySQL Installation:**

By default, MySQL is not secured. To secure your installation, run the following command and follow the on-screen prompts:

```bash
mysql_secure_installation
```
This command will prompt you to set a root password, remove anonymous users, disallow root login remotely, and remove the test database.

**5. Access MySQL:**

You can access the MySQL shell by running the following command:

```bash
mysql -u root -p
```
Enter the root password you set during the secure installation.
