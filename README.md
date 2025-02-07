# 21cmCLAST

[![License: GPL v3](https://img.shields.io/badge/license-GPLv3-green.svg)](https://www.gnu.org/licenses/gpl-3.0)

[![Static Badge](https://img.shields.io/badge/physics-cosmology-darkblue)](https://en.wikipedia.org/wiki/Cosmology)
[![Static Badge](https://img.shields.io/badge/physics-21cm-yellow)](https://en.wikipedia.org/wiki/Hydrogen_line)
[![Static Badge](https://img.shields.io/badge/tools-CLASS-green)](https://github.com/lesgourg/class_public)

**A semi-numerical cosmological simulation code for the radio 21-cm signal including non cold dark matter scenarios.**

In this code we introduce several features to [**21cmFAST**](https://github.com/21cmfast/21cmFAST)[^1][^2] related to non cold dark matter and primordial magnetic fields effects on the matter power spectrum, structure formation, and evolution of the intergalactic medium between cosmic dawn and reionization. See [**exo21cmFAST**](https://github.com/gaetanfacchinetti/exo21cmFAST)[^3] for a modifier version of 21cmFAST that includes the effect of exotic energy injection from dark matter decay or annihilation.

This package is part of a set of codes which can be combined together to produce forecast or constraints from late-time Universe observables (such as 21cm) on exotic scearios of dark matter and more. Some of these packages are forks of previously existing repositories, some have been written from scratch
- [exo21cmFAST](https://github.com/gaetanfacchinetti/exo21cmFAST) forked from [this repository](https://github.com/21cmfast/21cmFAST)
- [HYREC-2](https://github.com/gaetanfacchinetti/HYREC-2) forked from [this repository](https://github.com/nanoomlee/HYREC-2)
- [MontePython](https://github.com/gaetanfacchinetti/montepython_public) forked from [this repository](https://github.com/brinckmann/montepython_public)
- [21cmCAST](https://github.com/gaetanfacchinetti/21cmCAST)
- [NNERO](https://github.com/gaetanfacchinetti/NNERO)


## Installing the ncdm / pmf branch of 21cmCLAST


This code comes in two flavour, one specially built for non cold dark matter and one for primordial magnetic fields. Both contains similarities and are destined to be merged after developmeent. However, for now, to install one of the two main branches of **21cmCLAST** run either one of this command
```
$ git clone https://github.com/gaetanfacchinetti/21cmCLAST.git --branch ncdm --single-branch
$ git clone https://github.com/gaetanfacchinetti/21cmCLAST.git --branch pmf --single-branch
```
On your terminal then go to the main folder (containing the file `config.py`) and run

```bash
$ pip install [-e] .
```


## What is new / different in 21cmCLAST?

**21cmCLAST** comes with different improvements to work with non standard cosmologies. 
- It implements the sharp-k cutoff for the evaluation of the variance of the matter power spectrum (usefull for instance for an accurate determination of the halo mass function in a warm dark matter scenario).
- Normalisation of the matter power spectrum can be done either using $\sigma_8$ or $\ln ({10}^{10} A_{\rm s})$.
- Many additional cosmological parameters are included: warm dark matter mass and fraction, neutrino masses, interaction strength between neutrinos and dark matter, primordial magnetic field primordial spectrum, ...
- Seamless coupling to CLASS. When `POWER_SPECTRUM` in `user_params` is set to `CLASS` the python wrapper of 21cmFAST will call [**CLASS**](https://github.com/lesgourg/class_public)[^4] provided that it is installed and pass the necessary information to the C-code of 21cmFAST. Note that not all input parameters of CLASS can be called and modified from 21cmFAST.
- Similarly, for primordial magnetic fields, we have coupled 21cmFAST to a python wrapped version of `HYREC` that can be downloaded here [gaetanfacchinetti/HYREC-2](https://github.com/gaetanfacchinetti/HYREC-2)
- A set of wrapping function has been added either for quick C-code evaluations and debugging.


## Using 21cmCLAST
 
All modifications compared to 21cmFAST happen under the hood and should be transparent for the user. Check `user_params` and `cosmo_params` in `inputs.py` for the new functionalities. In order to use the new wrapping function, all have a similar signature:
```python
my_result = py21cmfast.<my_function>(a, (b, c, d, ...,) *, user_params, cosmo_params, flag_options, astro_params)
```
where `a`, `b`, `c`, ... are arguments to pass, like an array of modes `k` on which to compute the matter power spectrum when `<my_function> = matter_power_spectrum`, or an array of mass and a redshift for the halo mass function `<my_function> = dndm`. 

## Credits

If you use **21cmCLAST** or parts of the new functionnalities not already present in 21cmFAST please cite at least one of the following paper that is relevant to your usage:

- V. Dandoy, C. Doering, G. Facchinetti, L. Lopez-Honorez, J. R. Schwagereit (in prep.)
- G. Facchinetti, *Teaching reionization to the machine: a method for combing constraints on non cold dark matter* (in prep.)
- G. Facchinetti, A. Korochkin, L. Lopez-Honorez (in prep.)


[^1]: Andrei Mesinger, Steven Furlanetto, and Renyue Cen, *21cmFAST: A Fast, Semi-Numerical Simulation of the High-Redshift 21-cm Signal* [[arXiv:1003.3878](https://arxiv.org/abs/1003.3878)]

[^2]: Andrei Mesinger and Steven Furlanetto, *Efficient Simulations of Early Structure Formation and Reionization* [[arXiv:0704.0946](https://arxiv.org/abs/0704.0946)]

[^3]: Gaétan Facchinetti, Laura Lopez-Honorez, Yuxiang Qin, Andrei Mesinger *21cm signal sensitivity to dark matter decay* [[arXiv:2308.16656]](https://arxiv.org/abs/2308.16656)

[^4]: Diego Blas, Julien Lesgourgues, Thomas Tram, *CLASS II: Approximation schemes* [[arXiv:1104.2933]](https://arxiv.org/abs/1104.2933)