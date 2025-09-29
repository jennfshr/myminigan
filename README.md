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
            vim
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
(minigan_torch_env) root@88f25d453432:~/myminiGan# spack spec
[+]  minigan@1.0.0 build_system=generic platform=linux os=ubuntu24.04 target=aarch64
[+]      ^py-horovod@master~cuda~rocm build_system=python_pip commit=413253cf1898a525f458c6780e7d7b0b0945c633 controllers:=mpi frameworks:=pytorch tensor_ops=mpi platform=linux os=ubuntu24.04 target=aarch64 %c,cxx,fortran=gcc@13.3.0
[+]          ^cmake@3.31.8~doc+ncurses+ownlibs~qtgui build_system=generic build_type=Release platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]              ^curl@8.15.0~gssapi~ldap~libidn2~librtmp~libssh~libssh2+nghttp2 build_system=autotools libs:=shared,static tls:=openssl platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]                  ^nghttp2@1.65.0 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^compiler-wrapper@1.0 build_system=generic platform=linux os=ubuntu24.04 target=aarch64
[e]          ^gcc@13.3.0~binutils+bootstrap~graphite~mold~nvptx~piclibs~profiled~strip build_system=autotools build_type=RelWithDebInfo languages:='c,c++,fortran' platform=linux os=ubuntu24.04 target=aarch64
[+]          ^gcc-runtime@13.3.0 build_system=generic platform=linux os=ubuntu24.04 target=aarch64
[e]          ^glibc@2.39 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64
[+]          ^openmpi@5.0.8+atomics~cuda~debug+fortran~gpfs~internal-hwloc~internal-libevent~internal-pmix~ipv6~java~lustre~memchecker~openshmem~rocm~romio+rsh~static~two_level_namespace+vt+wrapper-rpath build_system=autotools fabrics:=none romio-filesystem:=none schedulers:=none platform=linux os=ubuntu24.04 target=aarch64 %c,cxx,fortran=gcc@13.3.0
[+]              ^autoconf@2.72 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64
[+]              ^automake@1.16.5 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]              ^gnuconfig@2024-07-27 build_system=generic platform=linux os=ubuntu24.04 target=aarch64
[+]              ^hwloc@2.11.1~cairo~cuda~gl~level_zero~libudev+libxml2~nvml~opencl+pci~rocm build_system=autotools libs:=shared,static platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]                  ^libpciaccess@0.17 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]                      ^util-macros@1.20.1 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64
[+]              ^libevent@2.1.12+openssl build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]              ^libtool@2.4.7 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]                  ^findutils@4.10.0 build_system=autotools patches:=440b954 platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]              ^openssh@9.9p1+gssapi build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]                  ^krb5@1.21.3+shared build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]                      ^bison@3.8.2~color build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]                  ^libedit@3.1-20240808 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]              ^perl@5.42.0+cpanm+opcode+open+shared+threads build_system=generic platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]                  ^berkeley-db@18.1.40+cxx~docs+stl build_system=autotools patches:=26090f4,b231fcc platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]              ^pmix@6.0.0~munge~python build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]              ^prrte@4.0.0 build_system=autotools schedulers:=none platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]                  ^flex@2.6.3+lex~nls build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^pkgconf@2.5.1 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^py-cffi@1.17.1 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]              ^py-pycparser@2.21 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^py-cloudpickle@3.0.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]              ^py-flit-core@3.12.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]          ^py-packaging@25.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]          ^py-pip@25.1.1 build_system=generic platform=linux os=ubuntu24.04 target=aarch64
[+]          ^py-psutil@6.1.1 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^py-pytorch-lightning@1.5.3 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]              ^py-future@1.0.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]              ^py-pydeprecate@0.3.1 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]              ^py-tensorboard@2.11.2 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                  ^py-absl-py@1.4.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                  ^py-google-auth@2.27.0~aiohttp build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                      ^py-cachetools@5.2.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                      ^py-pyasn1-modules@0.2.8 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                          ^py-pyasn1@0.4.8 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                      ^py-rsa@4.9 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                  ^py-google-auth-oauthlib@0.4.6 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                      ^py-requests-oauthlib@1.3.1 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                          ^py-oauthlib@3.2.2~rsa~signals~signedtoken build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                  ^py-grpcio@1.48.2 build_system=python_pip patches:=6be44fb platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]                      ^c-ares@1.28.1~ipo build_system=cmake build_type=Release generator=make platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]                      ^py-coverage@7.10.0~toml build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]                      ^py-cython@0.29.36 build_system=python_pip patches:=c4369ad platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]                      ^re2@2024-07-02~icu~ipo+pic+shared build_system=cmake build_type=Release generator=make platform=linux os=ubuntu24.04 target=aarch64 %cxx=gcc@13.3.0
[+]                          ^abseil-cpp@20240722.0~ipo+shared build_system=cmake build_type=Release cxxstd=14 generator=make platform=linux os=ubuntu24.04 target=aarch64 %cxx=gcc@13.3.0
[+]                  ^py-markdown@3.4.1 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                  ^py-tensorboard-data-server@0.6.1 build_system=python_pip commit=6acf0be88b5727e546dd64a8b9b12d790601d561 patches:=8cbd5fe,ce5d221 platform=linux os=ubuntu24.04 target=aarch64
[+]                      ^rust@1.85.0+dev~docs+src build_system=generic platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]                          ^libgit2@1.8.0~curl~ipo+mmap+ssh build_system=cmake build_type=Release generator=make https=system platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]                              ^pcre@8.45~jit+multibyte+pic+shared+static+utf build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]                          ^libssh2@1.11.1+shared build_system=autotools crypto=openssl platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]                          ^rust-bootstrap@1.85.0 build_system=generic platform=linux os=ubuntu24.04 target=aarch64
[+]                              ^patchelf@0.17.2 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]                  ^py-tensorboard-plugin-wit@1.8.1 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                  ^py-werkzeug@3.1.3 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]              ^py-torchmetrics@1.8.1~image build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                  ^py-lightning-utilities@0.11.2 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]          ^py-pyyaml@6.0.2+libyaml build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]              ^libyaml@0.2.5 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^py-wheel@0.45.1 build_system=generic platform=linux os=ubuntu24.04 target=aarch64
[+]          ^python-venv@1.0 build_system=generic platform=linux os=ubuntu24.04 target=aarch64
[+]      ^py-matplotlib@3.0.0~animation~fonts+image~latex~movies backend=agg build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^freetype@2.13.2+pic+shared build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^libpng@1.6.47~ipo~pic build_system=cmake build_type=Release generator=make libs:=shared,static platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^py-cycler@0.12.1 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]          ^py-kiwisolver@1.4.8 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64 %cxx=gcc@13.3.0
[+]              ^py-cppy@1.3.1 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]              ^py-setuptools-scm@8.2.1+toml build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                  ^git@2.48.1+man+nls+perl+subtree~svn~tcltk build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]                      ^libidn2@2.3.7 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]                          ^libunistring@1.2 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]                      ^pcre2@10.44~jit+multibyte+pic build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^py-pillow@11.3.0~avif~freetype~imagequant+jpeg~jpeg2000~lcms~tiff~webp~xcb+zlib build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^py-pyparsing@3.1.2 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]          ^py-python-dateutil@2.8.2 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]              ^py-six@1.17.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]      ^py-numpy@1.26.4 build_system=python_pip patches:=873745d platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^openblas@0.3.30~bignuma~consistent_fpcsr+dynamic_dispatch+fortran~ilp64+locking+pic+shared build_system=makefile symbol_suffix=none threads=none platform=linux os=ubuntu24.04 target=aarch64 %c,cxx,fortran=gcc@13.3.0
[+]          ^py-cython@3.1.3 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^py-meson-python@0.18.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]              ^meson@1.8.2 build_system=python_pip patches:=0f0b1bd platform=linux os=ubuntu24.04 target=aarch64
[+]              ^py-pyproject-metadata@0.9.1 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]      ^py-setuptools@79.0.1 build_system=generic platform=linux os=ubuntu24.04 target=aarch64
[+]      ^py-torch@2.8.0~caffe2~cuda~custom-protobuf~debug+distributed+fbgemm~gloo+kineto~metal~mkldnn+mpi+numa+numpy+openmp+qnnpack~rocm+tensorpipe~test~ucc+valgrind+xnnpack build_system=python_pip commit=ba56102387ef21a3b04b357e5b183d48f0afefc7 patches:=5e56556,e5a030a,f4cd8de platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^cpuinfo@2025-03-21~ipo build_system=cmake build_type=Release commit=5e3d2445e6a84d9599bee2bf78edbb4d80865e1d generator=ninja platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^eigen@3.4.0~ipo~nightly~rocm build_system=cmake build_type=Release generator=make platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^fp16@2020-05-14~ipo build_system=cmake build_type=Release commit=4dfe081cf6bcd15db339cf2680b9281b8451eeb3 generator=ninja platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^fxdiv@2020-04-17~ipo build_system=cmake build_type=Release commit=b408327ac2a15ec3e43352421954f5b1967701d1 generator=ninja platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^ninja@1.13.0+re2c build_system=generic platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]              ^re2c@3.1 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^numactl@2.0.18 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]              ^m4@1.4.20+sigsegv build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]                  ^libsigsegv@2.14 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^nvtx@3.2.1+python build_system=generic patches:=8f82f00 platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^protobuf@3.13.0~ipo+shared build_system=cmake build_type=Release generator=make patches:=9b6dcfa platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^psimd@2020-05-17~ipo build_system=cmake build_type=Release commit=072586a71b55b7f8c584153d223e95687148a900 generator=ninja platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^pthreadpool@2023-08-29~ipo build_system=cmake build_type=Release commit=4fe0e1e183925bf8cfa6aae24237e724a96479b8 generator=ninja platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^py-astunparse@1.6.3 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]          ^py-filelock@3.19.1 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]              ^py-hatch-vcs@0.5.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]              ^py-hatchling@1.27.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                  ^py-pathspec@0.12.1 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                  ^py-pluggy@1.5.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                  ^py-trove-classifiers@2025.5.9.12 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                      ^py-calver@2025.4.17 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]          ^py-fsspec@2024.10.0+http build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]              ^py-aiohttp@3.11.16 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]                  ^py-aiohappyeyeballs@2.6.1 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                      ^py-poetry-core@2.1.2 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]                  ^py-aiosignal@1.2.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                  ^py-attrs@25.3.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                      ^py-hatch-fancy-pypi-readme@25.1.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                  ^py-frozenlist@1.5.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]                      ^py-expandvars@1.1.1 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                  ^py-multidict@6.1.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]                  ^py-propcache@0.3.1 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]                  ^py-yarl@1.18.3 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^py-jinja2@3.1.6~i18n build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]              ^py-markupsafe@2.1.3 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^py-networkx@2.7.1+default~extra build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]          ^py-protobuf@3.13.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^py-pybind11@3.0.0+ipo build_system=cmake build_type=Release generator=ninja platform=linux os=ubuntu24.04 target=aarch64 %cxx=gcc@13.3.0
[+]              ^py-scikit-build-core@0.11.5~pyproject build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64 %c,cxx,fortran=gcc@13.3.0
[+]          ^py-requests@2.32.3~socks build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]              ^py-certifi@2025.7.14 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]              ^py-charset-normalizer@3.3.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]              ^py-idna@3.4 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]              ^py-urllib3@2.1.0~brotli~socks build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]          ^py-sympy@1.13.3 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]              ^py-mpmath@1.3.0 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]          ^py-tqdm@4.67.1~notebook~telegram build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]          ^py-typing-extensions@4.14.1 build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64
[+]          ^sleef@3.8~ipo build_system=cmake build_type=Release generator=ninja platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^valgrind@3.25.1+boost+mpi+only64bit~ubsan build_system=autotools libs:=shared,static platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]              ^boost@1.88.0+atomic~charconv+chrono~clanglibcpp~cobalt~container~context~contract~conversion~coroutine~date_time~debug+exception~fiber~filesystem~graph~graph_parallel~icu~iostreams~json~locale~log~math~mpi~mqtt5+multithreaded~nowide~numpy~pic~program_options~python~random~regex~serialization+shared~signals2~singlethreaded~stacktrace+system~taggedlayout~test+thread~timer~type_erasure~url~versionedlayout~wave build_system=generic cxxstd=11 patches:=a440f96 visibility=hidden platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]      ^py-torchvision@0.23.0~ffmpeg+jpeg~nvjpeg+png~video_codec~webp build_system=python_pip platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^libjpeg-turbo@3.0.4~ipo~jpeg8~partial_decoder+pic build_system=cmake build_type=Release generator=make libs:=shared,static platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]              ^nasm@2.16.03 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]      ^python@3.11.11+bz2+crypt+ctypes+dbm~debug+libxml2+lzma~optimizations+pic+pyexpat+pythoncmd+readline+shared+sqlite3+ssl~tkinter+uuid+zlib build_system=generic patches:=13fa8bf,b0615b2,ebdca64,f2fd060 platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^bzip2@1.0.8~debug~pic+shared build_system=generic platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]              ^diffutils@3.12 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^expat@2.7.1+libbsd build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]              ^libbsd@0.12.2 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]                  ^libmd@1.1.0 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^gdbm@1.25 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^gettext@0.23.1+bzip2+curses+git~libunistring+libxml2+pic+shared+tar+xz build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]              ^libiconv@1.18 build_system=autotools libs:=shared,static platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]              ^libxml2@2.13.5~http+pic~python+shared build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]              ^tar@1.35 build_system=autotools zip=pigz platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]                  ^pigz@2.8 build_system=makefile platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]                  ^zstd@1.5.7+programs build_system=makefile compression:=none libs:=shared,static platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^gmake@4.4.1~guile build_system=generic platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^libffi@3.4.8 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^libxcrypt@4.4.38~obsolete_api build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^ncurses@6.5-20250705~symlinks+termlib abi=none build_system=autotools patches:=7a351bc platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]          ^openssl@3.4.1~docs+shared build_system=generic certs=mozilla platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
[+]              ^ca-certificates-mozilla@2025-08-12 build_system=generic platform=linux os=ubuntu24.04 target=aarch64
[+]          ^readline@8.3 build_system=autotools patches:=21f0a03 platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^sqlite@3.50.4+column_metadata+fts+rtree build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^util-linux-uuid@2.41 build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^xz@5.6.3~pic build_system=autotools libs:=shared,static platform=linux os=ubuntu24.04 target=aarch64 %c=gcc@13.3.0
[+]          ^zlib-ng@2.2.4+compat+new_strategies+opt+pic+shared build_system=autotools platform=linux os=ubuntu24.04 target=aarch64 %c,cxx=gcc@13.3.0
spack install --add minigan # should build minigan
```
```sh
(minigan_torch_env) root@88f25d453432:~/myminiGan# spack find -L
==> In environment minigan
==> 1 root specs
-- no arch / no compilers ---------------------------------------
[+] 3jc7li3xllfb6nwkmxnd3i476c76v2x3 minigan

-- linux-ubuntu24.04-aarch64 / %c,cxx,fortran=gcc@13.3.0 --------
xuzc5gy5xgpjtsaltwmjlrezsqigyowl openblas@0.3.30
xiswdkq4qtmlircs3uthjsktuljbxyby openmpi@5.0.8
ws54wr2rjyz2xi4qchobbmmfizsmcdpx py-horovod@master
ndqbkbhikftrl6jrrrmgpa43cizzwcxh py-scikit-build-core@0.11.5

-- linux-ubuntu24.04-aarch64 / %c,cxx=gcc@13.3.0 ----------------
t6f4thyf3m7oybj5otv7fq5do7yehnyz berkeley-db@18.1.40
x4n5jbvtjp6hmyti6tmmjfis7kaogxud bison@3.8.2
szvtlsu67usb7ufgobwdigsollozawee boost@1.88.0
pgdidsf2r5cvexg3vt5flwlv76ubg5w7 c-ares@1.28.1
srsctdygluhk5ufzxzp6psdyebo7myj6 cmake@3.31.8
uprljctntwdait5d62c64yg77smbaxzl cpuinfo@2025-03-21
tukzjujncbiscidlytzxuohsjqmukrxi curl@8.15.0
vrtzjtvqzndovfxqjb3agx26k6gaznp2 eigen@3.4.0
5vjsymhs54duxzblosqorsigxy4d5kf7 expat@2.7.1
6goij2bilq75qhh3cud5wg5ws4wke4nk flex@2.6.3
nojygsdnovtqxzkfhl6bvgartyiorptv fp16@2020-05-14
jpqvtrflkkxszgln4smrwsx7rwhnjurz fxdiv@2020-04-17
qybgohi2bixm2hl3clidvwdqk7f6iam3 gettext@0.23.1
eheyx2peafsuveb4ocbpgr6y3k3a5ikk hwloc@2.11.1
px2kc255tj5l67h2xqpmmzdxiygywxbp krb5@1.21.3
w2jhc56zcxy62tqvgzkim36dwxnbumsp libffi@3.4.8
m5ycqlfaxcrglawsxsjegtpn7h2fkp67 libjpeg-turbo@3.0.4
z5u55ygqzb6aatk7zhfo4qsm44amuzqv libpng@1.6.47
mcsoby4a2wgwupgvewwmzs7nlidszlkg m4@1.4.20
dmrgq4tsf32kz2ig54tfuf3c3miejrqq ncurses@6.5-20250705
n2adi5xmcfdhd7bh6bkotc2drywstbsq nghttp2@1.65.0
gpik5cu2ind5nxreaw54kxkhmssrhcpz ninja@1.13.0
fgqtplanxdhbutwootqjsskhwncasr4p nvtx@3.2.1
wkvppjz7b4koynfav5vglhcbc6u3qhol openssh@9.9p1
6ccwule5cjua6rn4lboed5tllyw4r4zt openssl@3.4.1
f4kzwvwggscuwgdkr346rz2dojzsasi2 patchelf@0.17.2
bsyl25adxwlytmqfx3hro7ple3rsomuz pcre@8.45
ry4i2whbmaz2mdne24kpq5tjc7yx6ahc protobuf@3.13.0
akzwvvhfczzxakaatrqacxkdkmap6b4q psimd@2020-05-17
jksrxoamlwxv2tdph56j5cd5f26is2ei pthreadpool@2023-08-29
j2vsl2p6prttnvqprki4kx6pceiiw6g6 py-cython@0.29.36
6uxqunmd6fraxe4murks3g6etmf4ekei py-cython@3.1.3
emdcfgnmzw7xxrbplzmaicrox37cxjlw py-grpcio@1.48.2
4yek7aqs2yvg2snfoyadygkcdpykzoih py-matplotlib@3.0.0
6ydbah6upjvdcd3ybmxryutf4av2a43f py-numpy@1.26.4
z3q4wsgpnbqpz63vuxwufolcskjkaadd py-torch@2.8.0
g6rbrumgpmfggo6kn5i6fgvydx3nmiaz py-torchvision@0.23.0
g5hdeymeyh5muyljbvqvif6y57cdas67 python@3.11.11
dscucgzarn4uka524uaaedbh32dkjzus re2c@3.1
3ruvz4qnh3itlog3iy6bggu4qnvmqhud rust@1.85.0
fxuhh7vl4w7sa6wem7unkco3jpkkwdfv valgrind@3.25.1
or25urhbkwpflentd3watzesj24o5uog zlib-ng@2.2.4
xyfbmadpchsmbcava7xnvaa2evubaujb zstd@1.5.7

-- linux-ubuntu24.04-aarch64 / %c=gcc@13.3.0 --------------------
bypskr2caoui2dnx66rxos27ujz2spn7 automake@1.16.5
6dtoehuw4lir6qdxwu3w3z7jhjnoin2w bzip2@1.0.8
vytmwu533x7hpjaahrxkz2zstpbrmam4 diffutils@3.12
utmdufk65srushji7p5bmm2ddpfquaj7 findutils@4.10.0
wwdiustl45q5vbdzvgq2ebrkwuqfcoxa freetype@2.13.2
ylqxqszkqgczomyupz5ft4z7m3yaxonw gdbm@1.25
3lbxjrsbeh5ssiq3kparopedas75mp2i git@2.48.1
nbybixnmj4rhfms2d3xdjwqlbi4yjahx gmake@4.4.1
me7zzjnqxlmwmdn6nq3t4r6rcnyqgrtb libbsd@0.12.2
xo434kxc6edarodq4gpubn26eshzlxih libedit@3.1-20240808
lppg3gxtz3j5przc45o52tbbzncxjkqa libevent@2.1.12
w5dlm3v4tdm7ipbnefswqtqech5qfcqm libgit2@1.8.0
tc34zisbpmycnxlghkhkkpaqtw77qswa libiconv@1.18
mwlgmvjtdoq7wblm44vrz6y4dvi5dfa6 libidn2@2.3.7
u4vpokjq5nl5mea6j4nsq6lbg73xybat libmd@1.1.0
zwsbr47hk54s2jvycqydgzyh4chncqvt libpciaccess@0.17
cyprinxzugqb5ajaq7kffedxga6fwghb libsigsegv@2.14
sfyeafwozvyiaonksi5woxbijn3ef475 libssh2@1.11.1
5mnpsvss4bqgyzqi3q76dhoydgkmf4su libtool@2.4.7
pkp7e4s36glehh2dko7jvuayr7app2g4 libunistring@1.2
qqm3vw52flhv4p3swhsajawkdtxbry3a libxcrypt@4.4.38
37psmdiwovmdvs7nx4nilmsql4pilx4t libxml2@2.13.5
bsfs3oiya5giykxuhnxfcyhnbef3c6dd libyaml@0.2.5
bthin72u6ub5uhxcbds3fsrtpcmr2ugj nasm@2.16.03
khydkrg3yojckdbeanjw467ayu7v7bfb numactl@2.0.18
5lpzbt3pnck24yhdyvnx6d5jwkzdcr7v pcre2@10.44
vnm6pwzu4v2w4g2p5sgwgjxg7ad3jch2 perl@5.42.0
xkrguk6ojop2vw4iglpvcsekcidxg2b7 pigz@2.8
o5tshy7rubrtuod2n2wni3bkuoduewoh pkgconf@2.5.1
wiai5aw2ttufhbvy35zg2gmnbceuleqy pmix@6.0.0
pzokbkcnqmoye2mlfcxf46rsmxtjdqho prrte@4.0.0
miwwvxbnvlhpw3hveq5jbtl4brsnr54d py-aiohttp@3.11.16
dcgteozidd57jdcln7msd2wigfio7rk3 py-cffi@1.17.1
vloltr6vcqh4dgg6sybnecbjamvdbloi py-coverage@7.10.0
iaj5mv2cnco3hswqsv3ei5xritxtzspc py-frozenlist@1.5.0
k7agak4sqeoa3qibfcdalfukegn6qwyd py-markupsafe@2.1.3
ivuk6nveftlr2wtbnanlg4yw55mld3ve py-meson-python@0.18.0
sc6y4ppi7f342titadptyjycthd6tjd6 py-multidict@6.1.0
rvcrdon6pwp4gpgbvhg6kujukxt4xpiq py-pillow@11.3.0
zwghxx5j7ea7375c56oux7obodhft467 py-poetry-core@2.1.2
ywdumkyum5d74buqnxnfa3embzsaqocb py-protobuf@3.13.0
ak2jszic3eflz264vcdodly6ap7hmoje py-psutil@6.1.1
v7p4nwfcncg6etnml5ltq76xcgt43fve py-pycparser@2.21
hvmksyt6mhnm5v65bji25u2ebsg5wxoa py-yarl@1.18.3
uqq3sfjcw7ct7t7u5rjduvm62bmfiqpk readline@8.3
hsfeqsqhd5h7wvuywz64oxu657zgkalt sleef@3.8
ixzicvcpqr3nzklaepcssvrxcmtf74b2 sqlite@3.50.4
pa6jlkskbbkxl3ug6ouegwxv525qikam tar@1.35
lprqdvyq2u5yv37kvo2jseefcuiyrzyp util-linux-uuid@2.41
zt4dzgohwddcwqx3nkcy7wwemim2suc3 xz@5.6.3

-- linux-ubuntu24.04-aarch64 / %cxx=gcc@13.3.0 ------------------
uwteceu2atae5llwqkamx6twytp3mm75 abseil-cpp@20240722.0
ssxqtvhuhyuc3cfsz6otx7kulhdbsyrb py-kiwisolver@1.4.8
xrah475in7sriz2ahen7n2dv2f27zmwx py-pybind11@3.0.0
wdruku67br3xrq6tlg2l76c34c7akktt re2@2024-07-02

-- linux-ubuntu24.04-aarch64 / no compilers ---------------------
jbjy2jjr5yw6a2lztltsavcozxrk4mat autoconf@2.72
bz7aucfjdl2iqxotwdcyjoaw5e4g63kb ca-certificates-mozilla@2025-08-12
ocr6cd2bboo4q5ya5fk4honb4uh4ivkb compiler-wrapper@1.0
7lbazxfv5ptconj53y6ml2fh2a54qb7k gcc@13.3.0
ypfptwbk5f4z4crtb5q4dgeucx6quqzy gcc-runtime@13.3.0
wqjtbsviuku7636hcyn654wbxpxra6gr glibc@2.39
vqf355fusxq5rws2qayopto23rgvrjbr gnuconfig@2024-07-27
4wtki5odctziybvhxllzkvuev5vxsun6 meson@1.8.2
3jc7li3xllfb6nwkmxnd3i476c76v2x3 minigan@1.0.0
cgd6qzgxlkdxi7kmjffxj5iozkgwbtxm py-absl-py@1.4.0
rioej5plajy2p5krjgishbojoxyycwxv py-aiohappyeyeballs@2.6.1
pcu2nb5tkdzl6hrqdseayoo6z774dgvw py-aiosignal@1.2.0
mlfyxnmcdqso562so5pi44svqficz6q7 py-astunparse@1.6.3
ubjskfexeqxk6relgqlozsfjz5hfnpco py-attrs@25.3.0
t2bw27y7kksi6z7hcklebvxelnfcfn6i py-cachetools@5.2.0
ddbp3j67o2t4q24jeqj4z7oljhzns43s py-calver@2025.4.17
vqqqrvqq7e3kr6aj33uoildxzajpetm3 py-certifi@2025.7.14
3ubvdd544jvtkbkuwi7qqrkl3qtuqgkn py-charset-normalizer@3.3.0
sgjm2fsbgzd467oapluotsjx7ugs3ae3 py-cloudpickle@3.0.0
6hv4xkx5vsvcsgtbwlvewxgp42lk2rco py-cppy@1.3.1
73v7g27m2ycqhn5wqhqq2jhiwpoazyxj py-cycler@0.12.1
y4zio2lpadpnt2lrtp6772pgznlwf6iz py-expandvars@1.1.1
eeuilkejrvgcgomq4nfgzxqfagihopfu py-filelock@3.19.1
ccoisacdfjkilyaysvbpcirl46g3tna6 py-flit-core@3.12.0
37mjy2gb2ydqfi22eabyw223aanyyjqa py-fsspec@2024.10.0
f7vbioyvkg5hq66n4crgmasqhvzry332 py-future@1.0.0
xs7gwg4azmbdmyg2cf6z4f5v63xttq3t py-google-auth@2.27.0
h372dmhhu6d2yeuaqejwjkpil644a4qt py-google-auth-oauthlib@0.4.6
od6lzv4nvmbfud4sopyaoe2izbwsph5l py-hatch-fancy-pypi-readme@25.1.0
atnmbkkpa7sw64iajgaau2uvwupiylrw py-hatch-vcs@0.5.0
boagovn2ckg2r6y75o3fmupgnvf4nnum py-hatchling@1.27.0
6ahr252vuvgfmllxoe2jxs2cjypvvyor py-idna@3.4
5ajc7vmgttcqlyrusp5ohnkhoijy4xky py-jinja2@3.1.6
4ov6k6ddci2u74ey4bc4midctdj6oo5b py-lightning-utilities@0.11.2
w5qundhra3ocmthnu7czzekzwfesakh7 py-markdown@3.4.1
jd4foa5k7chzzqu4kuypw5aplwfxkxm2 py-mpmath@1.3.0
3a7vbhq536zaoa5xwhb7wwzpv34z3w3c py-networkx@2.7.1
s77g5yzadhvc3btjogpwqngp6ktgnitj py-oauthlib@3.2.2
32bsneln5gpm5w2ynltrnlkszv7bjksm py-packaging@25.0
ix67xlwzbauzrdq34za5xcqentn5johm py-pathspec@0.12.1
qub4nt2xkehtqtajalbizkitpwfaupac py-pip@25.1.1
lg2gmsj6apcaep5fvxqdgfvfsvjild4p py-pluggy@1.5.0
a67cwxf6k3lsen3fmnh7ocqzjf5f535c py-propcache@0.3.1
oqqqbestfy3ihysgtednvsrbnhyonetw py-pyasn1@0.4.8
gp5zd2dlwewzfijmcvtzw5ingkmfgjak py-pyasn1-modules@0.2.8
ogr6atrpjnic5i5xm24zrdboj5hakbpj py-pydeprecate@0.3.1
o44pt6uxukxmwannov6r54cwkdco36id py-pyparsing@3.1.2
jnxw2ftbnh72hlcbjaiq6rnzkx5mjepe py-pyproject-metadata@0.9.1
nt6zeypok72arun6s6nmbykk7lqcdkjc py-python-dateutil@2.8.2
ruysq654estmgnthyvvorr3wj2tugznv py-pytorch-lightning@1.5.3
f46qwixtkyivbswk5lxg2lzpfl2mxkud py-pyyaml@6.0.2
hmnrbw52gxenmhlqzpmnqypwvyygx5cx py-requests@2.32.3
a2obzue525wfkyr4ircitmkc5doebevy py-requests-oauthlib@1.3.1
rzpxffz3x3ko4nsj3tq6je2teyyvnp6k py-rsa@4.9
vqp6r34uwnzqqipu3vdvyuuujjowlsup py-setuptools@79.0.1
qvftw2ywbt2ljiiq2suijzrgthtznasw py-setuptools-scm@8.2.1
2g7ouljcyjebsgbusock3xafsayql7ci py-six@1.17.0
ftuuwjba2hralvifx7yfepaq4wrzcnro py-sympy@1.13.3
hxf5wqroc5rzfjxozyla6qchcsqj5rf4 py-tensorboard@2.11.2
y6vbe7om4zrxtbzc6n2jlslxpkpii22x py-tensorboard-data-server@0.6.1
pcb5dmbwbnkvx2yih4wejtansxohp4w2 py-tensorboard-plugin-wit@1.8.1
b4audouzsd7wjvwj24hx3gsdjpx7efaz py-torchmetrics@1.8.1
xbfyw7njunau3unoqg2ugko277d2xls6 py-tqdm@4.67.1
up5ancfdgmwgflxzic6ire2msfjsviun py-trove-classifiers@2025.5.9.12
fvhazscaunmsunod2oucuxlbiueoe3xb py-typing-extensions@4.14.1
wqvgf4zsktz3tqvbza5k5cs6whcqkkod py-urllib3@2.1.0
e2df34jqofkduc2o2a5mue7qqzfzs2wp py-werkzeug@3.1.3
j4rjzww5lqw5tiukidutdldkngdvl4ea py-wheel@0.45.1
kq4guj4pxmujjcoayyp4vxljp7mh2sxv python-venv@1.0
ncxe2mxsq27cileoov2ybyelocdmpsza rust-bootstrap@1.85.0
4of2rir5bcobslsbtaaoyoxlq3rlfxnf util-macros@1.20.1
==> 172 installed packages
==> 0 concretized packages to be installed (show with `spack find -c`)
```
### Spack load minigan
```sh
spack load minigan
spack find -p minigan
(minigan_torch_env) root@88f25d453432:~/myminiGan# spack find -p minigan
 ==> In environment minigan
==> 1 root specs
-- no arch / no compilers ---------------------------------------
[+] minigan

-- linux-ubuntu24.04-aarch64 / no compilers ---------------------
minigan@1.0.0  /myspack/opt/spack/linux-aarch64/minigan-1.0.0-3jc7li3xllfb6nwkmxnd3i476c76v2x3
==> 1 installed package
==> 0 concretized packages to be installed (show with `spack find -c`)
(minigan_torch_env) root@88f25d453432:~/myminiGan#  pushd /myspack/opt/spack/linux-aarch64/minigan-1.0.0-3jc7li3xllfb6nwkmxnd3i476c76v2x3
```
### Setup PYTHONPATH to use the right site-packages
```sh
export PYTHONPATH=/myspack/var/spack/environments/minigan/.spack-env/view/lib/python3.11/site-packages
```

### Test pytorch
```sh
pushd /myspack/opt/spack/linux-aarch64/minigan-1.0.0-3jc7li3xllfb6nwkmxnd3i476c
76v2x3/pytorch
python3 minigan_driver.py --help
root@88f25d453432:/myspack/opt/spack/linux-aarch64/minigan-1.0.0-3jc7li3xllfb6nwkmxnd3i476c
76v2x3/pytorch# python3 minigan_driver.py --help

-----------------------------------------

**** BEGIN miniGAN PROXY APPLICATION ****

-----------------------------------------

usage: minigan_driver.py [-h] [--dataset Str] [--dim-mode N] [--kk-mode] [--batch-size N]
                         [--test-batch-size N] [--epochs N] [--disc-lr LR] [--gen-lr LR]
                         [--disc-beta1 B1] [--gen-beta1 B1] [--bn-eps EPS] [--bn-mom MOM]
                         [--leaky-relu LR] [--soft-label LS] [--label-mut LM]
                         [--dg-train-ratio TR] [--num-images N] [--image-dim N]
                         [--num-channels N] [--data-workers N] [--disc-layers N]
                         [--disc-kern-size N] [--disc-filters N] [--disc-kern-stride N]
                         [--disc-padding N] [--gen-layers N] [--gen-kern-size N]
                         [--gen-filters N] [--gen-kern-stride N] [--gen-padding N]
                         [--gen-noise N] [--output-dir Str] [--data-dir Str]
                         [--checkpoint N] [--log-interval N] [--checkpoint-images N]
                         [--profile] [--prof-steps N] [--prof-images N] [--num-threads N]
                         [--num-gpus N] [--no-cuda] [--fp16-allreduce] [--seed S]

MiniGAN proxy app

options:
  -h, --help            show this help message and exit
  --dataset Str         which dataset to use from ("random" or "bird") (default:
                        "random")
  --dim-mode N          2d or 3d mode (default: 2)
  --kk-mode             use kk convolutions
  --batch-size N        input batch size for training (default: 64)
  --test-batch-size N   input batch size for testing (default: 64)
  --epochs N            number of epochs to train (default: 5)
  --disc-lr LR          discriminator learning rate (default: 0.0004)
  --gen-lr LR           generator learning rate (default: 0.0001)
  --disc-beta1 B1       discriminator Adam beta parameter (default: 0.5)
  --gen-beta1 B1        generator Adam beta parameter (default: 0.5)
  --bn-eps EPS          batch norm epsilon (default: 1e-5)
  --bn-mom MOM          batch norm momentum (default: .1)
  --leaky-relu LR       negative slope of leaky relu (default: .2)
  --soft-label LS       soften labels from 0/1 to LS/(1-LS) (default: 0.0)
  --label-mut LM        discriminator label mutation rate (default: 0.0)
  --dg-train-ratio TR   train discriminator N times for each generator training (default:
                        1)
  --num-images N        number of images in training set (default: 1024)
  --image-dim N         dimensions of images (square/cube) (default: 64)
  --num-channels N      number of input channels (default: 1)
  --data-workers N      number of data loader workers (default: 2)
  --disc-layers N       number of discriminator convolutions (default: 3)
  --disc-kern-size N    size of discriminator filter kernel (default: 4)
  --disc-filters N      number of discriminator filters (default: 64)
  --disc-kern-stride N  stride of discriminator filter kernel (default: 2)
  --disc-padding N      image padding for discriminator convolutions (default: 1)
  --gen-layers N        number of generator transp convolutions (default: 3)
  --gen-kern-size N     size of generator filter kernel (default: 4)
  --gen-filters N       number of generator filters (default: 64)
  --gen-kern-stride N   stride of generator filter kernel (default: 2)
  --gen-padding N       image passing for generator transposed convolutions (default: 1)
  --gen-noise N         size of generator noise vector input (default: 100)
  --output-dir Str      output directory (default: "./output")
  --data-dir Str        data directory (default: "../data/bird_images")
  --checkpoint N        epochs between checkpoints (default: 1)
  --log-interval N      batches between logging training status (default: 32
  --checkpoint-images N
                        number of images to save during checkpoint (default: 16
  --profile             profile layers instead of running GAN training
  --prof-steps N        number of dummy steps in profiler (default: 3)
  --prof-images N       number of images to profile (default: 1)
  --num-threads N       number of threads to use for CPU (default: 32)
  --num-gpus N          number of gpus available (default: 1)
  --no-cuda             disables CUDA training
  --fp16-allreduce      use fp16 compression during allreduce
  --seed S              random seed (default: 42)
```

### Save state on running container
```sh
# while docker container is running, in a separate shell, do this:
docker image list # see what container images you have in local cache
docker ps # list running containers (should see your current running container) and container id

docker commit <container_id> <container_name>:<tag>
```
e.g.
```sh
jkgreen@s1105469 ~ % docker image list
REPOSITORY                                TAG               IMAGE ID       CREATED         SIZE
ubuntu                                    latest            353675e2a41b   7 days ago      139MB
<none>                                    <none>            9cbed7541129   4 weeks ago     139MB
jkgreen76/ldms-slingshot-switch-sampler   latest            693f466f5cd4   2 months ago    1.46GB
<none>                                    <none>            eebf24097528   2 months ago    1.26GB
foo                                       latest            5fb90c2606cc   2 months ago    1.42GB
moby/buildkit                             buildx-stable-1   832fa7aa1eb3   3 months ago    312MB
tonistiigi/binfmt                         latest            1b804311fe87   6 months ago    108MB
mauwii/ubuntu-act                         22.04             05bf90d6b55c   19 months ago   10GB
jkgreen@s1105469 ~ % docker ps
CONTAINER ID   IMAGE           COMMAND       CREATED          STATUS          PORTS     NAMES
c39a444a79c3   ubuntu:latest   "/bin/bash"   59 minutes ago   Up 59 minutes             gallant_cori
jkgreen@s1105469 ~ % docker commit c39a444a79c3 ubuntu:jkgreen-test
sha256:9c175ee53d76e298eaaaf6a0710eada8b0cb8aec3e426dde0ffe0e7afaf0d0cf
jkgreen@s1105469 ~ % echo $?
0
jkgreen@s1105469 ~ % docker image list
REPOSITORY                                TAG               IMAGE ID       CREATED          SIZE
ubuntu                                    jkgreen-test      9c175ee53d76   15 seconds ago   1.92GB
ubuntu                                    latest            353675e2a41b   7 days ago       139MB
<none>                                    <none>            9cbed7541129   4 weeks ago      139MB
jkgreen76/ldms-slingshot-switch-sampler   latest            693f466f5cd4   2 months ago     1.46GB
<none>                                    <none>            eebf24097528   2 months ago     1.26GB
foo                                       latest            5fb90c2606cc   2 months ago     1.42GB
moby/buildkit                             buildx-stable-1   832fa7aa1eb3   3 months ago     312MB
tonistiigi/binfmt                         latest            1b804311fe87   6 months ago     108MB
mauwii/ubuntu-act                         22.04             05bf90d6b55c   19 months ago    10GB
```

## LDMS+Darshan
### Install dependencies
```bash
sudo apt-get install autoconf -y 
sudo apt-get install pkg-config -y
sudo apt-get update -y

sudo apt-get install hdf5-tools libhdf5-openmpi-dev openmpi-bin -y
sudo apt-get install python3.10 -y 
sudo apt-get install python-dev-is-python3 -y
sudo apt-get install make -y 
sudo apt-get install bison -y 
sudo apt-get install flex -y
sudo apt-get update -y
 
sudo apt update
sudo apt install python3-docutils
sudo apt-get update
sudo apt-get install libjansson-dev -y
```
### Clone LDMS
```bash 
git clone https://github.com/ovis-hpc/ovis.git 
```
### Build LDMS
```bash
cd ovis && mkdir build
./autogen.sh && cd build
../configure --prefix=${HOME}/ovis/build 
make
make install
```
### set-ldms-env.sh 
```bash
cat<<- HERE >set-ldms-env.sh # Create an script to easily setup the LDMS paths and variables
#!/bin/sh
export LDMS_INSTALL_PATH=/home/ubuntu/ovis/build
export LD_LIBRARY_PATH=$LDMS_INSTALL_PATH/lib/:$LD_LIBRARY_PATH
export LDMSD_PLUGIN_LIBPATH=$LDMS_INSTALL_PATH/lib/ovis-ldms
export ZAP_LIBPATH=$LDMS_INSTALL_PATH/lib/ovis-ldms
export PATH=$LDMS_INSTALL_PATH/sbin:$LDMS_INSTALL_PATH/bin:$PATH
export PYTHONPATH=/usr/local/lib/python3.10/dist-packages
 
export COMPONENT_ID="1"
export SAMPLE_INTERVAL="1000000"
export SAMPLE_OFFSET="0"
export HOSTNAME="localhost"
HERE
```
```bash
source set-ldms-env.sh
git clone https://github.com/darshan-hpc/darshan.git
cd darshan
mkdir build
./prepare.sh && cd build/
../configure --with-log-path=${HOME}/darshan/build/logs --prefix=${HOME}/darshan/build/install --with-jobid-env=PBS_JOBID CC=mpicc --enable-ldms-mod --with-ldms=${HOME}/ovis/build
make
make install
```
```bash
cat <<-HERE_DARSHAN>set-ldms-darshan-env.sh #- Create an script to easily setup the Darshan paths and variables:
#!/bin/sh
export DARSHAN_INSTALL_PATH=/home/ubuntu/darshan/build/install/
export LD_PRELOAD=/home/ubuntu/darshan/build/install/lib/libdarshan.so
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$DARSHAN_INSTALL_PATH/lib
export DARSHAN_MOD_ENABLE="DXT_POSIX,DXT_MPIIO"
 
# enable LDMS data collection. No runtime data collection will occur if this is not exported.
export DARSHAN_LDMS_ENABLE=
# determine which modules we want to publish to ldmsd
export DARSHAN_LDMS_ENABLE_MPIIO=
export DARSHAN_LDMS_ENABLE_POSIX=
export DARSHAN_LDMS_ENABLE_STDIO=
export DARSHAN_LDMS_ENABLE_HDF5=
export DARSHAN_LDMS_ENABLE_ALL=
export DARSHAN_LDMS_VERBOSE=
 
# darshanConnector
export DARSHAN_LDMS_STREAM=darshanConnector
export DARSHAN_LDMS_XPRT=sock
export DARSHAN_LDMS_HOST=localhost
export DARSHAN_LDMS_PORT=10444
export DARSHAN_LDMS_AUTH=none
HERE_DARSHAN
```
### Set paths and variables for Darshan:
 
```bash
source ./set-ldms-darshan-env.sh
```

```bash
cat <<-HERE_CONF >darshan_stream_store.conf #- Create the LDMS stream configuration file:
load name=hello_sampler
config name=hello_sampler producer=${HOSTNAME} instance=${HOSTNAME}/hello_sampler stream=darshanConnector component_id=${COMPONENT_ID}
start name=hello_sampler interval=${SAMPLE_INTERVAL} offset=${SAMPLE_OFFSET}
 
load name=stream_csv_store
config name=stream_csv_store path=./streams/store container=csv stream=darshanConnector rolltype=3 rollover=500000
HERE_CONF
```
### [TERMINAL 1] Run the deamon:
```bash
sudo chmod 1777 /var/run/
ldmsd -x sock:10444 -c darshan_stream_store.conf -l /tmp/darshan_stream_store.log -v DEBUG 
cat /tmp/darshan_stream_store.log
ldms_ls -p 10444 -x sock -v -v
ps auwx | grep ldmsd | grep -v grep
``` 

### (If doesn’t work, try:)
```bash
export PATH=$PATH:/home/ubuntu/ovis/build/sbin
source ~/.bashrc
which ldmsd
---->/home/ubuntu/ovis/build/sbin/ldmsd
```
### [TERMINAL 2] Run the python application:
```bash 
source set-ldms-darshan-env.sh
export PROG=mpi-io-test
export DARSHAN_TMP=/tmp/darshan-ldms-test
export DARSHAN_TESTDIR=/home/ubuntu/darshan/darshan-test/regression
export DARSHAN_LOGFILE=$DARSHAN_TMP/${PROG}.darshan
 
mkdir -p $DARSHAN_TMP
cd $DARSHAN_TESTDIR
mpicc $DARSHAN_TESTDIR/test-cases/src/${PROG}.c -o $DARSHAN_TMP/${PROG}
cd $DARSHAN_TMP
./${PROG} -f $DARSHAN_TMP/${PROG}.tmp.dat
```
### Check results collected by the LDMS stream:
```bash
cat /tmp/darshan_stream_store.log
```
