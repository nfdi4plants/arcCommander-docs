# arcCommander_docs

After initializing this template please run the following commands to get started:

1. `dotnet tool restore`, will restore local dotnet tools _fornax_ and _paket_.
2. `dotnet paket install`, will download the Nfdi4Plants.Fornax library.
3. `cd src` -> `dotnet fornax watch`

Done! 🎉 You can now open your static website on http://127.0.0.1:8080

## Docs 

Check out the docs for usage [here](https://nfdi4plants.github.io/web-components-docs/docs/SupportedStaticSiteGenerators.html#fornax).

## Update @nfdi4plants/web-components 

_Might need to install rollup globally before._

1. `npm install @nfdi4plants/web-components@latest`
2. `rollup --config rollup.config.js`

## Update Nfdi4Plants.Fornax

`dotnet paket update Nfdi4Plants.Fornax`

## Schedule automatic updates for gh-pages

See [here](https://nfdi4plants.github.io/web-components-docs/docs/ScheduledUpdates.html).