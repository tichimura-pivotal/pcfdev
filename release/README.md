# Lattice Release - `lattice.tgz`

Lattice base images are baked with Diego and CF components that Lattice depends on.
A `lattice.tgz` file is used to provision a Lattice base image (for any infrastructure)
with Lattice-specific components. A `lattice.tgz` file is a built release of the
[Lattice repository](https://github.com/cloudfoundry-incubator/lattice).

## Building

To build a `lattice.tgz` file, execute the `release/build` script. You must have the
following dependencies:
- Go 1.4+ with Linux/AMD64 cross compilation support
- A `$GOPATH` and `$PATH` set according to the `.envrc` file in the root of the repository.
  The [direnv](https://github.com/direnv/direnv) tool may be used for this purpose.
- All submodules up-to-date

## Installation

To install a `lattice.tgz` file, first extract the `install` folder at the root of the tarball.
- The `install/common` script must be run on every Lattice instance.
- The `install/cell` script must be run on every Lattice cell
  with the `lattice.tgz` file as the first argument.
- The `install/brain` script must be run on every Lattice brain
  with the `lattice.tgz` file as the first argument.
- These scripts may be run in any order. All of them are necessary to provision a collocated
  Lattice instance.

Other directories inside of the `install` directory contain infrastructure-specific patch scripts.
- These scripts must be executed after the platform-independent install scripts described above.
- These scripts must be named `common`, `cell`, or `brain`, and should be executable in any order.
- These scripts should not depend on the `lattice.tgz` file.