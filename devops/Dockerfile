FROM node:16-alpine

WORKDIR /app
COPY . /app

RUN apk add --no-cache make m4 gcc g++ git \
    ocaml ocaml-compiler-libs ocaml-ocamldoc opam ocaml-findlib

# Setup OCaml ${{ matrix.ocaml-version }}
RUN opam init -a --disable-sandboxing --compiler=4.14.1

# Install Opam deps
RUN opam install . --deps-only --with-test --yes

# Build PPX
RUN opam exec -- dune build --profile static

# Install Yarn deps
RUN yarn install

# Build ReScript lib
RUN (cd lib; yarn run build)

# Build ReScript examples
RUN (cd examples; yarn run build)

ENTRYPOINT ["tail", "-f", "/dev/null"]
