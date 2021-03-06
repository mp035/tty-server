[![Build Status](https://travis-ci.com/elisescu/tty-server.svg?branch=master)](https://travis-ci.com/elisescu/tty-server)

# tty-server

Server side for [tty-share](https://github.com/elisescu/tty-share).


## Docker

The server can be built into a docker image as follows:

    docker build -t tty-server .

To run the container, type:

    docker run \
      -p 6543:6543 -p 5000:5000 \
      -e URL=http://localhost:5000 \
      --cap-drop=all --rm \
      tty-server

where you can replace `URL` by whatever will be the publicly visible URL of the server.

After this, clients can be connected as follows:

    tty-share -useTLS=false -server localhost:6543

In the above command, 6543 is the default port where `tty-server` listens for
incoming shares (i.e. `tty-share` clients), and 5000 is the port of the web
interface through which remote users can connect. You can override the
defaults by specifying a different port mapping on the command line, e.g.
`-p 7654:6543 -p 80:5000` to listen on `7654` and serve on `80`.
