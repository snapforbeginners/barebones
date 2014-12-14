# Barebones

This is a barebones Snap server. It contains a few routes and shows
how a more complicated website could be constructed.

# Using the Image

The image is available on the docker registry:

```
docker pull snapforbeginners/barebones
```

The Snap server runs on port `8000`, so we'll use that same port on
the host:
```
docker run -it -p 8000:8000 snapforbeginners/barebones
```

# Building

To build a new image, we need to clone this repository and run `docker
build`.

```
git clone git@github.com:snapforbeginners/barebones.git
cd barebones
docker build -t barebones .
```

then we can run it as before:

```
docker run -it -p 8000:8000 barebones
```

# Exercise Answers

1. Run the image using: `docker run -it -p 8000:8000
   snapforbeginners/barebones`
   Access the container by typing in either `boot2docker ip` or
   `localhost` into the browser's URL bar. (ex: `localhost:8000`)
2. [getParam](https://hackage.haskell.org/package/snap-core-0.9.6.3/docs/Snap-Core.html#v:getParam)
3.

We can add a handler to the end of the chain that has no
routing restrictions:

```haskell
site :: Snap ()
site =
    ifTop (writeBS "hello world") <|>
    route [ ("foo", writeBS "bar")
          , ("echo/:echoparam", echoHandler)
          ] <|>
    dir "static" (serveDirectory "/opt/server/static") <|>
    catchAll

catchAll :: Snap ()
catchAll = writeBS "An error occurred"
```
