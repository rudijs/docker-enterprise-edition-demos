## Install Docker Trusted Registry

In this demo we are installing the DTR on the same virtual machine as the UCP control plane UI.

Both of these service want to use port 443, this will clash.

So we'll change the UCP UI to use port 444 and allow the DTR to use port 443.

1. Open [https://192.168.88.10/manage/settings/clusterconfig](https://192.168.88.10/manage/settings/clusterconfig) and change *Controller Port* to **444**
2. Click *Save*
3. Open [https://192.168.88.10:444/login/](https://192.168.88.10:444/login/)
4. Open [https://192.168.88.10:444/manage/settings/dtr](https://192.168.88.10:444/manage/settings/dtr)
  - Select the *UCP NODE* (ubuntu xenial)
  - Check *Disable TLS verification for UCP*
  - Copy to Clipboard
  - Execute

Example:

```
docker run -it --rm docker/dtr install \  
--ucp-node ubuntu-xenial \  
--ucp-username admin \  
--ucp-url https://192.168.88.10:444 \  
--ucp-insecure-tls
```

Setup will take a few minutes, once the command line prompt returns you can check by reloading [https://192.168.88.10:444/manage/settings/dtr](https://192.168.88.10:444/manage/settings/dtr)

You should see *Installed DTRs: 192.168.88.10*

Open the DTR admin here: [https://192.168.88.10] then login as user *admin*

## Organization and Repository Setup 

In the DTR admin UI:

1. Click *Organizations* > *New Organization* > *Organization Name* > **viseo** > *Save*
2. Click *Organizations* > *viseo* >  *Add user* > *New* > Username **jenkins** > Password **password** > *Save*
3. Click *Organizations* > *viseo* > *Repositories* > *Add repository* > *Repository Name* > **docker-demo-web-app** > *Save*

## Local DNS resolution

1. Update `/etc/hosts`
2. `sudo vi /etc/hosts`
3. Add the entry:
4. `192.168.88.10 local.dtr`

## Commandline access setup

1. Download the DTR CA certificate
  - `sudo curl -k https://local.dtr/ca -o /usr/local/share/ca-certificates/local.dtr`
2. Refresh the list of certificates to trust
  - `sudo update-ca-certificates`
3. Restart the Docker daemon
  - `sudo service docker restart`


