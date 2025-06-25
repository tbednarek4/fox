# FOX — Friedel Oscillation eXtension

Authors: Tomasz Bednarek, James Pogrebetsky, Michał Tomza, Alexandra Siklitskaya & Adam Kubas.

![FOX logo](https://github.com/tbednarek4/fox/blob/main/misc/logo-fox.png)
Logo generated with ChatGPT.

## Aim of the program
Based on the modern condensed matter physics and via inclusion of many-body effects, we supplement the ORCA [1] limited description of the metallic semi-infinite bulk with the proper point-charge embedding. [2]

## Usage of the program
The user is most welcome to read our [`manual.pdf`](https://github.com/tbednarek4/friedel-oscillation-extension/blob/main/manual.pdf) for more details.

Currently, the program (`generator.o`) is compiled for the Ubuntu operating system and has been tested on versions 18.04 LTS, 20.04 LTS, and 24.04 LTS. For other operating systems, such as Windows or macOS, the provided executable can still be used through a virtual machine running Ubuntu, or via the Windows Subsystem for Linux (WSL) in the case of Windows.

Generation of the point-charge embedding is carried out with the executable `generator.o`. The executable requires the binary data file `model.bin`, which contains the response of Pt(111) sampled at a vast real-space grid, and computed using the theoretical approach described in our paper [2]. Both files are available inside the [`execs`](https://github.com/tbednarek4/friedel-oscillation-extension/tree/main/execs) directory in this repository. 

Tip: In case of the error `bash: ./generator.o: Permission denied`, it is advisable to give an executable permission via the `chmod +x ./generator.o` command.

### Execution of the program
To display help and exit: `./generator.o --help`.

Command usage:
```
./generator.o [-i] <filename> -d <float> -o <int>
./generator.o [--input] <filename> --dipole <float> --order <int>
```

The `-i` or `--input` flag is optional; the input filename can be provided directly as the first positional argument. This flag specifies the input file, which must be either in ORCA input format (`*.inp`) [2] or in XYZ format (`*.xyz`). Only a single input file is supported per run, and only files with these two extensions are accepted.

The `-d` or `--dipole` flag specifies the effective $z$-component of the dipole moment of the adsorbed CO molecule, in units of eÅ. We recommend using values from Ref. [3]. A positive value corresponds to an effective positive charge on the carbon atom and a negative charge on the oxygen atom.

The `-o` or `--order` flag defines the order $n$ (or diameter) of the embedding point charge arrangement. The corresponding physical diameter $d$ of the embedding is calculated as: $d = (n - 1)\cdot\frac{a \sqrt{3}}{2}$, where $a = 2.812\textrm{ }Å$ is the Pt-Pt bond length.

To generate embedded point charges for the atop adsorption site of CO on Pt(111) using the recommended dipole moment, and assuming the geometry is provided in the file `orca-atop.inp`, the following command can be used (for the maximum tested order of 15): `./generator.o orca-atop.inp --dipole 0.089 --order 15`.

### Note regarding input files
The program is currently calibrated for the $\textrm{Pt}_{13}$ cluster (extracted from the Pt(111) surface), which is provided in the [`Pt13.xyz`](https://github.com/tbednarek4/friedel-oscillation-extension/blob/main/example/Pt13.xyz) file. The surface layer corresponds to $z = 0$, contains 7 Pt atoms, and is centered at $(x, y) = (0, 0)$. The CO molecule should be positioned in the vacuum region defined by $z < 0$ (see exemplary ORCA input files `orca-*.inp` for atop/bridge/hollow/reference adsorption sites in the [`example`](https://github.com/tbednarek4/friedel-oscillation-extension/tree/main/example) directory).

### Output of the program
The program outputs a file named `<filename>-<order>.pc` (where `<filename>` is the name of the input file w/o `.inp` or `.xyz` extension, and `<order>` is the embedding size) containing embedded point charges around the cluster and right-away compatible with ORCA.

### Recommended dipole moment values for the most frequent adsorption sites of CO at Pt(111)
According to the Ref. [3], the most optimal effective $z$-component dipole moments of CO at Pt(111) are:
- atop position: 0.0890 eÅ,
- bridge position: -0.0500 eÅ,
- hollow position: -0.0790 eÅ,
- reference position: 0.0254 eÅ,

where positive values signify an effective positive charge on the carbon atom, and an effective negative charge on the oxygen atom.

## Source code availability
The full source code for this project is not publicly available in this repository. However, it can be provided upon reasonable request for academic or non-commercial purposes. If you are interested in accessing the code, please contact us at this email: fox@ichf.edu.pl.

Please briefly describe your intended use or research interest in the project when reaching out.

## Citation
If you use this software or any part of its methodology in your research, please cite the following paper:

- T. Bednarek, J. Pogrebetsky, M. Tomza, A. Siklitskaya and A. Kubas. *Effective model describing long-range interactions
on metal surfaces*. In preparation **2025**

Proper citation helps support our research and allows others to find the original work. Thank you!

## References
[1] T. Bednarek, J. Pogrebetsky, M. Tomza, A. Siklitskaya and A. Kubas. *Effective model describing long-range interactions
on metal surfaces*. In preparation **2025**.

[2] F. Neese, F. Wennmohs, U. Becker and C. Riplinger. *The ORCA quantum chemistry program package*. The Journal of Chemical Physics, 152 224108 **2020**.

[3] P. Deshlahra, J. Conway, E. E. Wolf, and W. F. Schneider. *Influence of Dipole–Dipole Interactions on Coverage-Dependent Adsorption: CO and NO on Pt(111)*. Langmuir 28 (22) 8408-8417 **2012**.

## License CC BY-NC-ND 4.0

Shield: [![CC BY-NC-ND 4.0][cc-by-nc-nd-shield]][cc-by-nc-nd]

This work is licensed under a
[Creative Commons Attribution-NonCommercial-NoDerivs 4.0 International License][cc-by-nc-nd].

[![CC BY-NC-ND 4.0][cc-by-nc-nd-image]][cc-by-nc-nd]

[cc-by-nc-nd]: http://creativecommons.org/licenses/by-nc-nd/4.0/
[cc-by-nc-nd-image]: https://licensebuttons.net/l/by-nc-nd/4.0/88x31.png
[cc-by-nc-nd-shield]: https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg
