<!-- Authors: Mikaël Cugnet, Florian Gallois, Angel Kirchev and Dr. Denys Dutykh (Mathematics Department, Khalifa University of Science and Technology, Abu Dhabi, UAE) -->

# NEOLAB: a Scilab tool to simulate the negative electrode of lead-acid batteries

---

**Authors**: Mikaël Cugnet, Florian Gallois, Angel Kirchev, Denys Dutykh

**Latest version**: 1.0

**Supported Scilab version**: 6.1.0

**Licence**: GNU Lesser General Public License, version 2.1 or (at your option) any later version

**Article**: SoftwareX 22, 101394 (2023), https://doi.org/10.1016/j.softx.2023.101394

---

Responding to the need of a growing community of students and researchers who want to get involved in the field of
electrochemical storage systems, NEOLAB offers a new tool dedicated to a modelling domain where almost no open-source
solutions exist. Physics-based models of batteries require extensive knowledge in thermodynamics, electrochemistry,
mathematics, material and computer sciences. Based on the idea that a minimum working example is the best way to learn
gradually how to model a battery, NEOLAB provides a solution to simulate the behaviour of the negative electrode of
lead-acid batteries and a framework to investigate other primary and secondary technologies.

![Graphical abstract of the article: the battery, its negative electrode against the separator, the one-dimensional grid across the current collector, the active material and the separator, and the measured and simulated electrode voltages](images/Graphical_Abstract.png)

The graphical abstract of the article: from the battery to its negative electrode, the one-dimensional grid across the
electrode, and the electrode voltage against the capacity, measured (dashed) and simulated (solid), for discharges at
rates from 0.05C to 12C.

The model is a system of differential-algebraic equations for three unknowns, the interfacial voltage, the porosity of
the electrode and the concentration of the acid, which express the conservation of charge, of volume and of species
across the thickness of the electrode, on a grid of equally spaced nodes (10 in the shipped scripts). Each main script
sets its parameters (more than thirty constants for one electrode), then simulates, for eight rates from 0.05C to 12C,
a discharge at the recorded constant current followed by a rest, over the times of the experimental records of
`src/data/data.sod`.
The equations are integrated by `dassl`, the solver of differential-algebraic systems of Scilab, which uses backward
differentiation formulas; the script prints the computing time of each simulation and plots the electrode voltage
against the capacity and against time, measured and simulated. A study of the equations, the solvers, the tolerances and
the dimensionless form is given in the article cited below.

![Measured and simulated electrode voltages against time for the eight discharge rates](images/Uneg_wrt_t.png)

The electrode voltage against time, measured (dashed) and simulated (solid), for the eight rates from 0.05C to 12C: a
discharge at constant current followed by a rest.

---

## How to run

Open Scilab 6.1.0 in the folder `src` and execute one of the main scripts, for instance

```scilab
exec("main_dassl_dim.sce", -1)
```

or open the script in SciNotes, the editor of Scilab, and run it. The script first clears the workspace and asks at the
prompt for the path of the folder `src`, which holds the residue functions and the data:

```text
Enter the path (Ex: C:\Lead_Electrode) :
```

The answer is typed without quotation marks, for instance `C:\Users\me\NEOLAB\src` on Windows or `/home/me/NEOLAB/src`
on Linux. The scripts then load the residue function with `exec(path+'\res_dassl_dim.sci')` and the data with
`load(path+"\data\data.sod")`; these paths are written with the separators of Windows, which Scilab 2024.1 also accepted
on Linux in a test. A path with accented letters is to be avoided, as the comment of the scripts says.

The scripts were written for Scilab 6.1.0. In Scilab 2024.1 they stop at line 18, `xdel(winsid())`, since the function
`xdel` no longer exists; with that line replaced by `close(winsid())`, `main_dassl_dim.sce` runs to the end, its sixteen
simulations taking about 2 s, with warnings that `dassl` and `jetcolormap` are obsolete and will be removed in Scilab
2026.0.0.

The user has the choice to proceed with the dimensional or the dimensionless form of the equations, and to repeat the
simulations for relative tolerances from 10⁻⁵ to 10⁻¹¹ (the absolute tolerance being ten times smaller), counting the
calls of the residue function.

---

## Files and folders

| File or folder | Description |
|----------|-------------|
| `images` | the two pictures of this page |
| `src` | the source code |
| `src/data/data.sod` | the experimental data: the time, current, capacity and electrode voltage recorded during discharges at the eight rates and the following rests |
| `src/main_dassl_dim.sce` | main routine, dimensional equations, solved by `dassl` with the relative tolerance 10⁻⁶ |
| `src/main_dassl_adim.sce` | main routine, dimensionless equations, solved by `dassl` with the relative tolerance 10⁻⁶ |
| `src/main_dassl_dim_tol.sce` | main routine, dimensional equations, repeated for the relative tolerances 10⁻⁵ to 10⁻¹¹ |
| `src/main_dassl_adim_tol.sce` | main routine, dimensionless equations, repeated for the relative tolerances 10⁻⁵ to 10⁻¹¹ |
| `src/res_dassl_dim.sci` | residue function of the dimensional equations |
| `src/res_dassl_adim.sci` | residue function of the dimensionless equations |
| `src/res_dassl_dim_tol.sci` | residue function of the dimensional equations, counting its calls |
| `src/res_dassl_adim_tol.sci` | residue function of the dimensionless equations, counting its calls |
| `LICENSE` | the licence |
| `CITATION.cff` | the citation of the article, for the button "Cite this repository" |

---

## How to cite

If you use NEOLAB, please cite the article:

M. Cugnet, F. Gallois, A. Kirchev and D. Dutykh, NEOLAB: a Scilab tool to simulate the negative electrode of lead-acid
batteries, SoftwareX 22, 101394 (2023).

https://doi.org/10.1016/j.softx.2023.101394

```bibtex
@article{Cugnet2023,
  author = {Cugnet, Mika{\"e}l and Gallois, Florian and Kirchev, Angel and Dutykh, Denys},
  title = {{{NEOLAB}}: {{A Scilab}} Tool to Simulate the {{Negative Electrode}} of {{Lead-Acid Batteries}}},
  journal = {SoftwareX},
  year = 2023,
  month = may,
  volume = {22},
  pages = {101394},
  doi = {10.1016/j.softx.2023.101394}
}
```

The button "Cite this repository" in the right-hand column of this page gives the same reference, read from
`CITATION.cff`. The article is open access, and its supplementary material states the equations in full.

---

## Problems or questions

This repository is a copy of the original repository of NEOLAB,

https://github.com/FlorianGallois/NEOLAB

where problems and questions are best raised; the article gives the address of its corresponding author, Mikaël Cugnet
(CEA, Liten).
