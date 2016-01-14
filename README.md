# SugarCRM VagrantON Stacks

SugarCRM VagrantON Stacks it's built on top and dependent by [SugarCRM Engineering Stacks](https://github.com/sugarcrm/stacks).

## Advantages

VagrantON provides flexibility on top of VM Stacks such as:

 * fast and easy configurable, including shared folders and forwarded ports;
 * can run and control multiples stacks on the same time (ex: `vagrant up php55`);
 * private network ip as secondary adapter;
 * integrated with PHPStorm;
 * easy to use and control each stack trough local config.yml file;
 

## Install

### A. Easy steps by yourself

```bash
git clone https://github.com/svnvcristea/vagrantON.git
cd vagrantON
mkdir stacks
curl https://api.github.com/repos/sugarcrm/stacks/tarball/master -s -L -u gituser:gitpassword > stacks/stacks.tar.gz
tar -xzf stacks/stacks.tar.gz -C stacks --strip 1
rm stacks/stacks.tar.gz
vagrant up
```

**! Without your [`config/_private.yml`](config/_private.yml) in place will use the `DEFAULT_STACK:` configurations from [`config/config.yml`](config/config.yml)**

## Configure VagrantON

```bash
cp config/_private.yml.dist ./config/_private.yml
nano config/_private.yml
```

It's very easy con configure it by changing values in the [`config/_private.yml`](config/_private.yml)

## Stacks

Supported Stacks are:
```yaml
stacks: [db2, mts, oracle, oracle12c, php54, php55, php56, phpenv, qa-php53, qa-php54, ubuntu-driver]
```
So, `vagrant up` with ACTIVE_STACK = php54 in [`config/_private.yml`](config/_private.yml) will start the 'php54' stack by default. 
In case you will send the name of the stack from cli, the ACTIVE_STACK will be overwritten with the stack sent.
This mean that `vagrant up oracle12c` will start the 'oracle12c' stack.

### 1st vON Stack

When you want to start the box, just type `vagrant up` from this directory in a terminal window, it will load the base box into VirtualBox and boot it.  Once it's booted, it will run the provision scripts, downloading everything that is needed for it to run.

Once the box has been provisioned, you can access it by typing in `vagrant ssh` from the same terminal window.  It will log you in as the vagrant user, which has unrestricted sudo access.

Detail about the box can be found in the stacks/[README](stacks/README.md) file for the stacks as to what is installed and how it configured.

### Additional vON Stack

In order to start an additional VM stack just place the stack name after vagrant up : `vagrant up php56`
or change the value of ACTIVE_STACK from your [`config/_private.yml`](config/_private.yml) and `vagrant up`

## PHPStorm integration

From PHPStorm Menu `File -> Settings -> Tools -> Vagrant` :
 * set at `Instance folder:` your folder `~/vagrantOn`
 * add at `Environment variables` a new variable:
   * `Name` : `ACTIVE_STACK` and 
   * `Value` : `php55` (or the name of the stack) 
