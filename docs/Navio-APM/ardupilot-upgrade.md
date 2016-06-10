#### Overview

We're now in process of transitioning our deploy scheme. That's why we strongly encourage you to look into this article.
For a year our users had been asked to install a *deb* package with a ```dpkg -i``` command. This is a rather cumbersome way to get things done.
From now on we deploy the packages to our repository making to possible to use ```apt-get``` out of the box.

#### General warnings

Please, backup your parameters before proceeding!

#### Upgrade

```bash
pi@navio: ~ $ sudo apt-get update
pi@navio: ~ $ sudo apt-get dist-upgrade 
pi@navio: ~ $ sudo apt-get install apm-navio-beta
```
![upgrade-warning](img/navio-upgrade-warning.png)

Read the warning once more and please obey the instructions!

#### Final thoughts

If this tutorial is confusing in any way, please let us now! We'd be glad to help you out and fix the instructions accordingly.
