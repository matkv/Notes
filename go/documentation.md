# Go documentation

First we must install the Go documentation - on Manjaro/Arch this can be done using this command:

```bash
sudo pacman -S go-tools
```

We can launch the official Go documentation locally by running `godoc -http :8000` - this will run a web server that hosts Go documentation and makes it possible to access it by opening http://localhost:8000/pkg/.

