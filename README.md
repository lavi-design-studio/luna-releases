# Luna releases

Signed builds of **Luna**, a small browser for Windows with nothing in the way.
This repository holds releases only. An installed Luna checks here once a day,
downloads a newer `Luna-win-x64.zip`, verifies its `.sig` against Luna's release
key (ECDSA P-256), and puts it in place the next time Luna closes.

Each release has two files:

- `Luna-win-x64.zip`: the app (Windows 10/11 x64, needs the .NET 9 Desktop Runtime and the WebView2 runtime)
- `Luna-win-x64.zip.sig`: its signature
