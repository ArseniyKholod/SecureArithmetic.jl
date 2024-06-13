# SecureArithmetic.jl

[![Docs-stable](https://img.shields.io/badge/docs-stable-blue.svg)](https://securearithmetic-jl.lakemper.eu/stable)
[![Docs-dev](https://img.shields.io/badge/docs-dev-blue.svg)](https://securearithmetic-jl.lakemper.eu/dev)
[![Build Status](https://github.com/sloede/SecureArithmetic.jl/workflows/CI/badge.svg)](https://github.com/sloede/SecureArithmetic.jl/actions?query=workflow%3ACI)
[![Coveralls](https://coveralls.io/repos/github/sloede/SecureArithmetic.jl/badge.svg)](https://coveralls.io/github/sloede/SecureArithmetic.jl)
[![Codecov](https://codecov.io/gh/sloede/SecureArithmetic.jl/branch/main/graph/badge.svg)](https://codecov.io/gh/sloede/SecureArithmetic.jl)
[![License: MIT](https://img.shields.io/badge/License-MIT-success.svg)](https://opensource.org/license/mit/)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.10544790.svg)](https://doi.org/10.5281/zenodo.10544790)

SecureArithmetic.jl is a Julia package for performing cryptographically secure arithmetic
operations using fully homomorphic encryption. It currently provides a backend for
OpenFHE-secured computations using [OpenFHE.jl](https://github.com/sloede/OpenFHE.jl), and
an unencrypted backend for fast verification of a computation pipeline.


## Getting started

### Prerequisites
If you have not yet installed Julia, please [follow the instructions for your
operating system](https://julialang.org/downloads/platform/).
[SecureArithmetic.jl](https://github.com/sloede/SecureArithmetic.jl) works with Julia v1.8
and later on Linux and macOS platforms, and with Julia v1.9 or later on Windows platforms.

### Installation
Since SecureArithmetic.jl  is a registered Julia package, you can install it by executing
the following commands in the Julia REPL:
```julia
julia> import Pkg; Pkg.add("SecureArithmetic")
```
If you plan on running the examples in the
[`examples`](https://github.com/sloede/SecureArithmetic.jl/tree/main/examples) directory,
you also need to install OpenFHE.jl:
```julia
julia> import Pkg; Pkg.add("OpenFHE")
```

### Usage
The easiest way to get started is to run one of the examples from the
[`examples`](https://github.com/sloede/SecureArithmetic.jl/tree/main/examples) directory by
`include`ing them in Julia, e.g.,
```julia
julia> using SecureArithmetic

julia> include(joinpath(pkgdir(SecureArithmetic), "examples", "simple_real_numbers.jl"))
================================================================================
Creating OpenFHE context...
CKKS scheme is using ring dimension 16384

================================================================================
Creating unencrypted context...

================================================================================
simple_real_numbers with an OpenFHE context
Input x1: [0.25, 0.5, 0.75, 1.0, 2.0, 3.0, 4.0, 5.0]
Input x2: [5.0, 4.0, 3.0, 2.0, 1.0, 0.75, 0.5, 0.25]

Results of homomorphic computations:
x1 = [0.24999999999993638, 0.500000000000056, 0.7500000000000366, 0.9999999999999498, 2.0000000000000333, 3.0000000000000675, 3.9999999999999902, 4.99999999999997]
x1 + x2 = [5.2499999999999485, 4.499999999999966, 3.7500000000000533, 3.0000000000000466, 3.000000000000019, 3.7499999999999836, 4.499999999999986, 5.249999999999975]
x1 - x2 = [-4.749999999999893, -3.4999999999999805, -2.249999999999964, -0.9999999999998668, 0.9999999999999534, 2.249999999999984, 3.5000000000000973, 4.749999999999956]
4 * x1 = [1.0000000000004539, 1.9999999999998535, 3.000000000000176, 4.000000000000274, 7.999999999998697, 12.000000000000373, 15.999999999998332, 20.00000000000011]
x1 * x2 = [1.2500000000002318, 2.000000000000054, 2.2499999999994893, 1.9999999999998272, 2.000000000000205, 2.25000000000003, 1.9999999999997906, 1.2499999999996558]
x1 shifted circularly by -1 = [0.4999999999998632, 0.749999999999976, 0.9999999999999369, 1.9999999999999858, 2.9999999999998677, 4.000000000000045, 5.000000000000059, 0.25000000000002087]
x1 shifted circularly by 2 = [3.9999999999999973, 4.99999999999995, 0.2499999999999567, 0.49999999999996825, 0.7500000000000793, 0.9999999999998956, 2.00000000000004, 2.999999999999985]

================================================================================
simple_real_numbers with an Unencrypted context
Input x1: [0.25, 0.5, 0.75, 1.0, 2.0, 3.0, 4.0, 5.0]
Input x2: [5.0, 4.0, 3.0, 2.0, 1.0, 0.75, 0.5, 0.25]

Results of homomorphic computations:
x1 = [0.25, 0.5, 0.75, 1.0, 2.0, 3.0, 4.0, 5.0]
x1 + x2 = [5.25, 4.5, 3.75, 3.0, 3.0, 3.75, 4.5, 5.25]
x1 - x2 = [-4.75, -3.5, -2.25, -1.0, 1.0, 2.25, 3.5, 4.75]
4 * x1 = [1.0, 2.0, 3.0, 4.0, 8.0, 12.0, 16.0, 20.0]
x1 * x2 = [1.25, 2.0, 2.25, 2.0, 2.0, 2.25, 2.0, 1.25]
x1 shifted circularly by -1 = [0.5, 0.75, 1.0, 2.0, 3.0, 4.0, 5.0, 0.25]
x1 shifted circularly by 2 = [4.0, 5.0, 0.25, 0.5, 0.75, 1.0, 2.0, 3.0]
```


## Referencing
If you use SecureArithmetic.jl in your own research, please cite this repository as follows:
```bibtex
@misc{schlottkelakemper2024securearithmetic,
  title={{S}ecure{A}rithmetic.jl: {S}ecure arithmetic operations in {J}ulia using fully homomorphic encryption},
  author={Schlottke-Lakemper, Michael},
  year={2024},
  howpublished={\url{https://github.com/sloede/SecureArithmetic.jl}},
  doi={10.5281/zenodo.10544790}
}
```


## Authors
SecureArithmetic.jl was initiated by [Michael Schlottke-Lakemper](https://www.uni-augsburg.de/fakultaet/mntf/math/prof/hpsc)
(University of Augsburg, Germany), who is also its principal maintainer.


## License and contributing
SecureArithmetic.jl is available under the MIT license (see [LICENSE.md](LICENSE.md)).
Contributions by the community are very welcome! For larger proposed changes, feel free
to reach out via an issue first.
