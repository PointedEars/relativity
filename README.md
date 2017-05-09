`relativity.sty`
---
Relativistic calculations and plots for LaTeX2ε

# Table of Contents
  - [Dependencies](#dependencies)
  - [Features](#features)
    - [Calculations](#calculations)
      - Helpers
        * [`\FPevalr[digits=0]{\command}{expression}`](#-fpevalr-digits-0---command--expression-)
        * [`\FPnegr{digits}{\command}{expression}`](#-fpnegr-digits---command--expression-)
        * [`\FPnegval{expression}`](#-fpnegval-expression-)
        * [`\FProundval{expression}{digits}`](#-fproundval-expression--digits-)
      - Commands for global values
        * [`\solSI`](#-solSI)
        * [`\setsol{value}`](#setsol-value-)
        * [`\resetsol`](#-resetsol)
      - Main commands
        * [`\combinespeeds{\command}{speed1}{speed2}`](#-combinespeeds--command--speed1--speed2-)
        * [`\lencon{\command}{length}{speed}`](#-lencon--command--length--speed-)
        * [`\lorentz{\command}{speed}`](#-lorentz--command--speed-)
        * [`\lorentzr[digits=4]{\command}{speed}`](#-lorentzr-digits-4---command--speed-)
        * [`\lorentztospeed{\command}{factor}`](#-lorentztospeed--command--factor-)
        * [`\lorentztospeedr[digits=0]{\command}{factor}`](#-lorentztospeedr-digits-4---command--factor-)
        * [`\lorentztrafo{\newspace}{\newtime}{oldspace}{oldtime}{speed}`](#-lorentztrafo--newspace---newtime--oldspace--oldtime--speed-)
        * [`\spacetimeintv{\command}{x₁}{t₁}{x₂}{t₂}`](#-spacetimeintv--command--x---t---x---t--)
        * [`\timedil{\command}{time}{speed}`](#-timedil--command--time--speed-)
    - [Plots](#plots)
      - Environment
        * [`\spacetimediagramdefaults`](#-spacetimediagramdefaults)
        * [`\begin{spacetimediagram}[options]…\end{spacetimediagram}`](#-begin-spacetimediagram--options---end-spacetimediagram-)
      - Commands
        * [`\lightlike[style][x_shift=0][t_shift=0]{speed}`](#-lightlike-style--x-shift-0--t-shift-0--speed-)
        * [`\lightlike*[style][x_shift=0][t_shift=0]`](#-lightlike--style--x-shift-0--t-shift-0-)
        * [`\spacelike[style][time][x_shift=0][t_shift=0]{speed}`](#-spacelike-style--time--x-shift-0--t-shift-0--speed-)
        * [`\timelike[style][x_shift=0][t_start=0]{t_end}`](#-timelike-style--x-shift-0--t-start-0--t-end-)
        * [`\worldline[style]{term}`](#-worldline-style--term-)
        * [`\worldline*[style][x_shift=0][t_shift=0]{speed}`](#-worldline--style--x-shift-0--t-shift-0--speed-)

# Dependencies

`relativity.sty` uses

  - [fp](https://www.ctan.org/pkg/fp) for relativistic symbols
    and calculations;
  - [PGFPlots](http://pgfplots.sourceforge.net/) for drawing spacetime diagrams,
    and
  - [xparse](https://www.ctan.org/pkg/xparse) for commands with star parameter
    and multiple optional arguments.

# Features

## Calculations

### Helpers

#### `\FPevalr[digits=0]{\command}{expression}`
Define *`\command`* as the result of the `fp` *`expression`*, **rounded** to *`digits`*.

#### `\FPnegr{digits}{\command}{expression}`
Define *`\command`* as the **negative value** of *`expression`* rounded to *`digits`*.

#### `\FPnegval{expression}`
Generate the **negative value** of *`expression`*.

#### `\FProundval{expression}{digits}`
Generate the value of *`expression`* **rounded** to *`digits`*.

### Commands for global values

#### `\solSI`
Value of the **speed of light** as defined in the International System of Units (SI): 299'792'458 (meters per second).

#### `\setsol{value}`
Set the value of the **speed of light** (`\sol`) to *`value`*.

Use `\setsol{1}` to specify coordinates in light-years and years, or light-seconds and seconds aso., and speed in factors of c.

#### `\resetsol`
Equivalent to `\setsol{\solSI}`. Invoked initially.

### Main commands

#### `\combinespeeds{\command}{speed1}{speed2}`
**Relativistic velocity "addition"**: Define *`\command`* as the combined
speed in multiples of the speed of light, according to Lorentz transformation,
of the speeds *`speed1`* and *`speed2`*.

#### `\lencon{\command}{length}{speed}`
**Length contraction**: Define *`\command`* as the observed contracted length of *`length`* for the relative speed *`speed`*.

#### `\lorentz{\command}{speed}`
Define *`\command`* as the **Lorentz factor** for *`speed`* (see `\setsol`).

#### `\lorentzr[digits=4]{\command}{speed}`
Define *`\command`* as the **Lorentz factor** for *`speed`* (see `\setsol`),
rounded to *`digits`* (default: 4).

#### `\lorentztospeed{\command}{factor}`
Define *`\command`* as the **relative speed** for the Lorentz factor *`factor`* (`\setsol{1}` for a result in factors of c).

#### `\lorentztospeedr[digits=0]{\command}{factor}`
Define *`\command`* as the **relative speed** for a Lorentz factor *`factor`*
(`\setsol{1}` for a result in factors of c), rounded to *`digits`* (default: 0).

#### `\lorentztrafo{\newspace}{\newtime}{oldspace}{oldtime}{speed}`
Define *`\newspace`* as the space coordinate and *`\newtime`*
as the time coordinate after **Lorentz transformation**
of space coordinate *`oldspace`* and time coordinate *`oldtime`*
for a relative speed *`speed`* (see [`\setsol`](#setsol-value--)).

#### `\spacetimeintv{\command}{x₁}{t₁}{x₂}{t₂}`
Define *`\command`* as the **spacetime interval** between
spacetime coordinates (*`x₁`*, *`t₁`*) and (*`x₂`*, *`t₂`*).

#### `\timedil{\command}{time}{speed}`
**Time dilation**: Define *`\command`* as the observed dilated time of `time` for the relative speed `speed`.

## Plots

### Environment

#### `\spacetimediagramdefaults`
Default PGFPlots `axis` options for spacetime diagrams (see [`spacetimediagram`](#-begin-spacetimediagram--options---end-spacetimediagram-)):

```latex
axis x line=middle,
axis y line=middle,
xlabel={$x$},
ylabel={$t$}
```

#### `\begin{spacetimediagram}[options]…\end{spacetimediagram}`
Adds a new spacetime diagram environment with PGFPlots `axis` options `\spacetimediagramdefaults` augmented with *`options`* (optional).

##### Example

```latex
% Preamble
\usepackage{relativity}

% Main
\setsol{1}
\FPeval{\goodspeed}{0.6}
\FPeval{\badlaunchyear}{4}
\FPeval{\badlaunchyeartwo}{3}
\FPeval{\badspeed}{3}
\FPeval{\badspeedtwo}{1.5}
\newcommand{\goodcolor}{green}
\newcommand{\badcolor}{red}

\begin{spacetimediagram}[
  xmin=0,
  ymin=0, ymax=10,
  domain=0:10,
  grid
]
  \lightlike[dotted]

  \spacelike[\goodcolor]{\goodspeed}
  \foreach \t in {1, ..., 8}{
    \spacelike[\goodcolor, dashed][\t]{\goodspeed}
  }

  \worldline[\goodcolor]{1/\goodspeed * x}
  \worldline*[\goodcolor, very thick]{\goodspeed}

  \lightlike[\badcolor, dotted, thick][0][\badlaunchyear]
  \timelike[\badcolor, very thick]{\badlaunchyear}
  \worldline*[\badcolor, very thick][0][\badlaunchyear]{\badspeed}
\end{spacetimediagram}
```

### Commands

#### `\lightlike[style][x_shift=0][t_shift=0]{speed}`
Draws a light-like worldline in style *`style`* (optional),
origin shifted in the x-direction by *`x_shift`* (default: 0),
and in the t-direction by *`t_shift`* (default: 0);
draws only the worldline for the relative speed sgn(`speed`) (default: 1).

Use the PGFPlots `domain` option to limit the x-range.

#### `\lightlike*[style][x_shift=0][t_shift=0]`
Draws light-like worldlines (for both c and -c) in style *`style`* (optional),
origin shifted in the x-direction by *`x_shift`* (default: 0),
and in the t-direction by *`t_shift`* (default: 0).

#### `\spacelike[style][time][xshift=0][tshift=0]{speed}`
Draws a space-like worldline in style *`style`* (optional) for relative speed *`speed`*
and time *`time`* (default: 0)
shifted in the x-direction by *`x_shift`* (default: 0),
and in the t-direction by *`t_shift`* (default: 0).

#### `\timelike[style][x_shift=0][t_start=0]{t_end}`
Draws a time-like worldline in style *`style`* (optional)
parallel to the time axis (not function-based)
at x = *`x_shift`* (default: 0) from t = *`t_start`* (default: 0)
to t = *`t_end`* (mandatory, no default).

#### `\worldline[style]{term}`
Draws a worldline in style *`style`* (optional)
based on *`term`* for the temporal coordinate
(use x for the spatial coordinate) (mandatory)

#### `\worldline*[style][x_shift=0][t_shift=0]{speed}`
Worldline in style *`style`* (optional)
  * based on constant relative speed *`speed`* (mandatory)
  * shifted in the x-direction by *`x_shift`* (default: 0),
  * and in the t-direction by *`t_shift`* (default: 0).
