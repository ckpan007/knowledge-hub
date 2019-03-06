
## Understand the ACME protocol
https://ietf-wg-acme.github.io/acme/draft-ietf-acme-acme.html



## Option 1 - Use ACME client to generate certificate (recommended)

### Prerequisites
* You have the access to maintain your own domain name in aws
* You have a A record in aws with IP address
**The A record must associate with an IP**.

### Install ACME client - acme.sh
You can follow official documentation to install [acme.sh](https://github.com/Neilpang/acme.sh#2-or-install-from-git).
**Recommended**: it is recommended to install acme.sh via github.

### Design request url to implement certificate
You need to define the request urls that apply for the certificates.

In case our domain name is **awsdevnew.cpcorecn.net.**, after the cloud foundry deployment, some **CNAME** will be generated such as *.cfapps.awsdevnew.cpcorecn.net, *.cf.awsdevnew.cpcorecn.net.<br/>

After you prepare the expected CNAME, you can execute below command to generate certificate.

```sh
$cpreader@ip-10-0-0-12:~/workspace/cert/acme.sh$   export AWS_ACCESS_KEY_ID=XXXXXXXXXX
$cpreader@ip-10-0-0-12:~/workspace/cert/acme.sh$   export AWS_SECRET_ACCESS_KEY=XXXXXXXXXXXXXXX
$cpreader@ip-10-0-0-12:~/workspace/cert/acme.sh$ ./acme.sh --issue --dns dns_aws -d *.awsdevnew.cpcorecn.net -d awsdevnew.cpcorecn.net
```
Now your certificate key are stored in **/users/cpreader/.acme.sh/*.awsdevnew.cpcorecn.net/**.

## Option 2 - Apply certificate step by step

### Check the ubuntu version
```sh
cpreader@cpreader-1551766050590-3940:/users/cpreader/workspace/landscape-aws-devcnnew$ cat /etc/lsb-release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=16.04
DISTRIB_CODENAME=xenial
DISTRIB_DESCRIPTION="Ubuntu 16.04.5 LTS"
cpreader@cpreader-1551766050590-3940:/users/cpreader/workspace/landscape-aws-devcnnew$
```
So that the ubuntu system is **xenial** version.


### Install necessary plugins for certbot
* Go to [certbot](https://certbot.eff.org/lets-encrypt/ubuntuxenial-haproxy) and choose to use which component

### Install the necessary software in OS
For example, for ubuntu xenial, you need to install below:
```sh
$ sudo apt-get update
$ sudo apt-get install software-properties-common
$ sudo add-apt-repository universe
$ sudo add-apt-repository ppa:certbot/certbot
$ sudo apt-get update
$ sudo apt-get install certbot 
```

### Run command to generate certificate
Below command is the way that using webroot to generate certificate.
```sh
$ sudo certbot certonly --webroot -w /var/www/example -d example.com -d www.example.com -w /var/www/thing -d thing.is -d m.thing.is
```
This command will obtain a single cert for **example.com, www.example.com, thing.is, and m.thing.is**; it will place files below /var/www/example to prove control of the first two domains, and under /var/www/thing for the second pair.

Except the webroot way, you can also use webserver way to generate certificate for **haproxy**. For detail you can access [certbox](https://certbot.eff.org/lets-encrypt/ubuntuxenial-haproxy).

# Reference links
https://letsencrypt.org/getting-started/
https://ietf-wg-acme.github.io/acme/draft-ietf-acme-acme.html
https://certbot.eff.org/lets-encrypt/ubuntuxenial-haproxy
