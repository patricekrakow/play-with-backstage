# Let's Play with Backstage

With the procedure below, you can install your very own installation of Backstage on an Ubuntu Killercoda playground available at <https://killercoda.com/playgrounds/scenario/ubuntu>.

## Prerequisities

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

## Backstage

```text
npx @backstage/create-app@latest
```

```text
cd backstage
```

Use the _Traffic Port Accessor_ to get the URL accessing the ports 3000 and 7007, and use them to update the `baseUrl` of repsectively the `app` and the `backend` within the `app-config.yaml`file.

```text
vi app-config.yaml
```

***Warning.*** You need to update the `baseUrl` of the `app` to avoid the "Invalid Host header" error, **but** because of the Killercoda proxy, Backstage is not hit with the `https://` protocol, but with the `http://` protocol, so you MUST change the URL given by the _Traffic Port Accessor_, replacing `https://` by `http://` as illustrated below!

```yaml
app:
  baseUrl: http://d68f4aab-b3e7-4b97-a55e-e6b33267b180-10-244-3-249-3000.spch.r.killercoda.com
  listen:
    host: 0.0.0.0
    port: 3000
backend:
  baseUrl: https://d68f4aab-b3e7-4b97-a55e-e6b33267b180-10-244-3-249-7007.spch.r.killercoda.com
  listen:
    port: 7007
```

***Warning:*** the code above is just an example, you will have to use your own Killercoda URL, and **BE CAREFUL** not to put a training slash at the end of the URL!

```text
yarn dev
```

Wait to see the line `[0] webpack compiled successfully` and use the _Traffic Port Accessor_ on port 3000.

## References

* <https://backstage.io/docs/getting-started/>

* <https://github.com/laverdet/isolated-vm#requirements>

* <https://github.com/nvm-sh/nvm#install--update-script>

* <https://classic.yarnpkg.com/en/docs/install>
