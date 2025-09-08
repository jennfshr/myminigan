# myminigan
instructions for building minigan in a ubuntu container

## Spack
### Clone Spack
```sh
git clone https://github.com/spack/spack.git -b develop myspack
```

### Setup Spack env
```sh
source myspack/share/spack/setup-env.sh
```

### APT package requirements
```sh
apt update -y
apt install gcc \
            gfortran \
            python3 \
            python3-pip \
            cmake \
            git \
            unzip \
            vi
```

### Spack Environment Create
```sh
spack env create myminigan
spack env list # should show this new env
spack env activate myminigan
spack env status # should show myminigan is active
```

### Find compilers in myminigan context
```sh
spack compiler find
spack compiler list # should list gfortran and gcc
```

### Spack Spec Minigan
```sh
spack info minigan # will show package information
spack spec minigan # shows concrete spec file to build out minigan and its tpls
spack install --add minigan # should build minigan
```

