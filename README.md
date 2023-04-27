## build

`docker run --rm --name slate -v ./build:/srv/slate/build -v ./source:/srv/slate/source slatedocs/slate build`

## run

`docker run --rm --name slate -p 4567:4567 -v ./source:/srv/slate/source slatedocs/slate serve`

check http://localhost:4567 in your browser
