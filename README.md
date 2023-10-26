# Let's Play with Backstage

<https://killercoda.com/playgrounds/scenario/ubuntu>

```text
sudo apt-get install -y python g++ build-essential
```

```text
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
```

```text
nvm --version
```

```text
nvm install 18
```

```text
node --version
```

```text
npm install --global yarn
```

```text
yarn --version
```

```text
npx @backstage/create-app@latest
```

## NGINX

```text
apt-get update
```

```text
apt-get install -y nginx
```

You can then the installation of NGINX with the _Traffic Port Accessor_ on port 80.

```text
vi backstage.conf
```

```nginx
server {
  listen 80;

  location / {
    proxy_pass http://localhost:3000/;
  }
}
```

```text
rm /etc/nginx/sites-enabled/default
```

```text
cp backstage.conf /etc/nginx/sites-available
```

```text
ln -s /etc/nginx/sites-available/backstage.conf /etc/nginx/sites-enabled/backstage.conf
```

```text
service nginx configtest
```

```text
service nginx reload
```

```text
service nginx status
```

## Backstage Configuration

```text
cd backstage
```

Use the _Traffic Port Accessor_ to get the URL accessing the port 7007, and use it to update the `baseUrl` of the `backend` within the `app-config.yaml`file.

```text
vi app-config.yaml
```

```yaml
backend:
  baseUrl: https://91715300-6655-48c4-90bd-e77d1fbb4c56-10-244-3-99-7007.spch.r.killercoda.com
```

***Warning:*** the code above is just an example, you will have to use your own Killercoda URL, and **BE CAREFUL** not to put a training slash at the end of the URL!

```text
yarn dev
```

Wait to see the line `[0] webpack compiled successfully` and use the _Traffic Port Accessor_ on port 80.

## References

* <https://backstage.io/docs/getting-started/>

* <https://github.com/laverdet/isolated-vm#requirements>

* <https://github.com/nvm-sh/nvm#install--update-script>

* <https://classic.yarnpkg.com/en/docs/install>
