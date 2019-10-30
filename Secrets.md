### The secrecy

This part of buildbot is responisble for keeping things secure, it allows you to pass variables/passwords/tokens safely to your builds without revealing it in the console or logs.

In order to allow this we need to do two things. 

First create a folder with files where the secrets live.

``` bash
master 
 -> secret
     -> user
     -> password
```
The user and password are simple files and their content is the secret.

Then we add the following lines to the master.

This is to tell buildbot the provider.

``` python
c['secretsProviders'] = [secrets.SecretInAFile(dirname = r"d:\GitRepos\master\secret")]
```

This is to use the value from the secret in our case username.

``` python
 steps.ShellCommand(command = ["fsutil","file","createnew",util.Secret("user"),0])
```