`relativity.sty`
---
Relativistic calculations and plots for LaTeX2ε

# Table of Contents
  - [License](#license)
  - [Dependencies](#dependencies)
  - [Features](#features)
    - [Calculations](#calculations)
      - [Helpers](#helpers)
        * [`\FPevalr[digits=0]{\command}{expression}`](#fpevalrdigits0commandexpression)
        * [`\FPnegr{digits}{\command}{expression}`](#fpnegrdigitscommandexpression)
        * [`\FPnegval{expression}`](#fpnegvalexpression)
        * [`\FProundval{expression}{digits}`](#fproundvalexpressiondigits)
      - [Commands for global values](#commands-for-global-values)
        * [`\solSI`](#solsi)
        * [`\setsol{value}`](#setsolvalue)
        * [`\resetsol`](#resetsol)
      - [Main commands](#main-commands)
        * [`\composespeeds{\command}{speed1}{speed2}`](#composespeedscommandspeed1speed2)
        * [`\lencon{\command}{length}{speed}`](#lenconcommandlengthspeed)
        * [`\lorentz{\command}{speed}`](#lorentzcommandspeed)
        * [`\lorentzr[digits=4]{\command}{speed}`](#lorentzrdigits4commandspeed)
        * [`\lorentztospeed{\command}{factor}`](#lorentztospeedcommandfactor)
        * [`\lorentztospeedr[digits=0]{\command}{factor}`](#lorentztospeedrdigits0commandfactor)
        * [`\lorentztrafo{\newspace}{\newtime}{oldspace}{oldtime}{speed}`](#lorentztrafonewspacenewtimeoldspaceoldtimespeed)
        * [`\spacetimeintv{\command}{x₁}{t₁}{x₂}{t₂}`](#spacetimeintvcommandxtxt)
        * [`\timedil{\command}{time}{speed}`](#timedilcommandtimespeed)
    - [Plots](#plots)
      - [Environment](#environment)
        * [`\spacetimediagramdefaults`](#spacetimediagramdefaults)
        * [`\begin{spacetimediagram}[options]…\end{spacetimediagram}`](#beginspacetimediagramoptionsendspacetimediagram)
      - [Commands](#commands)
        * [`\lightlike[style][x_shift=0][t_shift=0]{speed}`](#lightlikestylex_shift0t_shift0speed)
        * [`\lightlike*[style][x_shift=0][t_shift=0]`](#lightlikestylex_shift0t_shift0)
        * [`\spatial[style][time][x_shift=0][t_shift=0]{speed}`](#spatialstyletimexshift0tshift0speed)
        * [`\temporal[style][x_shift=0][t_start=0]{t_end}`](#temporalstylex_shift0t_start0t_end)
        * [`\worldline[style]{term}`](#worldlinestyleterm)
        * [`\worldline*[style][x_shift=0][t_shift=0]{speed}`](#worldlinestylex_shift0t_shift0speed)

# License

Copyright © 2017  Thomas 'PointedEars' Lahn (<PointedEars@web.de>)

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

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
Define *`\command`* as the result of the [fp](#dependencies) expression *`expression`*, **rounded** to *`digits`*.

#### `\FPnegr{digits}{\command}{expression}`
Define *`\command`* as the **negative value** of *`expression`* rounded to *`digits`*.

#### `\FPnegval{expression}`
Generate the **negative value** of *`expression`*.

#### `\FProundval{expression}{digits}`
Generate the value of *`expression`* **rounded** to *`digits`*.

### Commands for global values

#### `\solSI`
Value of the **speed of light** as defined in the International System of Units (SI): 299'792'458 (m∕s).

#### `\setsol{value}`
Set the value of the **speed of light** (`\sol`) to *`value`*.

Use `\setsol{1}` to specify coordinates in light-years and years, or light-seconds and seconds aso., and speed in factors of c.

#### `\resetsol`
Equivalent to [`\setsol{\solSI}`](#setsolvalue). Invoked initially.

### Main commands

#### `\composespeeds{\command}{v₁}{v₂}`
**Relativistic velocity "addition"**: Define *`\command`*
as the speed that is the composition of the relative speeds *`v₁`* and
*`v₂`* (*`v₂`* measured in a frame of reference moving at *`v₁`*, or vice-versa),
each in multiples of the speed of light.

#### `\lencon{\command}{length}{speed}`
**Length contraction**: Define *`\command`* as the observed contracted length of *`length`* for the relative speed *`speed`*.

#### `\lorentz{\command}{speed}`
Define *`\command`* as the **Lorentz factor** for *`speed`* (see [`\setsol`](#setsolvalue)).

#### `\lorentzr[digits=4]{\command}{speed}`
Define *`\command`* as the **Lorentz factor** for *`speed`* (see [`\setsol`](#setsolvalue)),
rounded to *`digits`* (default: 4).

#### `\lorentztospeed{\command}{factor}`
Define *`\command`* as the **relative speed** for the Lorentz factor *`factor`* ([`\setsol{1}`](#setsolvalue) for a result in factors of c).

#### `\lorentztospeedr[digits=0]{\command}{factor}`
Define *`\command`* as the **relative speed** for a Lorentz factor *`factor`*
([`\setsol{1}`](#setsolvalue) for a result in factors of c), rounded to *`digits`* (default: 0).

#### `\lorentztrafo{\newspace}{\newtime}{oldspace}{oldtime}{speed}`
Define the command *`\newspace`* as the space coordinate and the command *`\newtime`* as the time coordinate after **Lorentz transformation**
of the space coordinate *`oldspace`* and the time coordinate *`oldtime`*
(both must be valid [fp](#dependencies) expressions) for a relative speed *`speed`* (see [`\setsol`](#setsolvalue)), such that

  *`\newspace`* = γ (*`oldspace`* + *`speed`* × *`oldtime`*)
  *`\newtime`* = γ (*`oldtime`* + *`speed`*∕`\sol`² × *`oldspace`*)

where

  γ := 1∕√(1 − *`speed`*²∕`\sol`²).

#### `\spacetimeintv{\command}{x₁}{t₁}{x₂}{t₂}`
Define *`\command`* as the **spacetime interval** between
spacetime coordinates (*`x₁`*, *`t₁`*) and (*`x₂`*, *`t₂`*).

#### `\timedil{\command}{time}{speed}`
**Time dilation**: Define *`\command`* as the observed dilated time of `time` for the relative speed `speed`.

## Plots

### Environment

#### `\spacetimediagramdefaults`
Default [PGFPlots](#dependencies) `axis` options for spacetime diagrams (see [`spacetimediagram`](#beginspacetimediagramoptionsendspacetimediagram)):

```latex
axis x line=middle,
axis y line=middle,
xlabel={$x$},
ylabel={$t$}
```

#### `\begin{spacetimediagram}[options]…\end{spacetimediagram}`
Adds a new spacetime diagram environment with [PGFPlots](#dependencies) `axis` options
[`\spacetimediagramdefaults`](#spacetimediagramdefaults) augmented with
*`options`* (optional).

Common options include:

  * `domain=…:…`: Global domain of the x-values. Objects will not be painted beyond this range even if `xmin` is less than the lower boundary or `xmax` is greater than the upper boundary.
  * `grid` (boolean): If set, a grid is painted.
  * `xlabel={$…$}`: Label of the primary spatial axis.  Enclose in braces and `$` signs (for math mode) to use subscripts.
  * `ylabel={$…$}`: Label of the primary temporal axis (ditto)
  * `xmin=…`: Minimum x-value. Can be a mathematical expression.
  * `xmax=…`: Maximum x-value (ditto)
  * `ymin=…`: Minimum t-value (ditto)
  * `ymax=…`: Maximum t-value (ditto)

See the [PGFPlots](#dependencies) documentation for more.

##### Example

```latex
% Preamble
\usepackage{relativity}

% Main
\setsol{1}
\FPeval{\goodspeed}{0.6}
\FPeval{\badlaunchyear}{4}
\FPeval{\badspeed}{3}
\newcommand{\goodcolor}{green}
\newcommand{\badcolor}{red}

\begin{spacetimediagram}[
  xmin=0, xlabel={$x_B$},
  ymin=0, ymax=12, ylabel={$t_B$},
  domain=0:12,
  grid
]
  \lightlike[dotted];

  \spatial[\goodcolor, domain=0:11.5]{\goodspeed}
    [->] node[anchor=north] {$x_G$};
  \foreach \t in {1, ..., 8}{
    \spatial[\goodcolor, dashed, domain=0:11.5][\t]{\goodspeed};
  }

  \worldline[\goodcolor, domain=0:6.9]{1/\goodspeed * x}
    [->] node[anchor=east] {$t_G$};
  \worldline*[\goodcolor, very thick, domain=0:3]{\goodspeed};

  \temporal[\badcolor, very thick]{\badlaunchyear};
  \lightlike[\badcolor, dotted, thick][0][\badlaunchyear];
  \worldline*[\badcolor, very thick, domain=0:3][0][\badlaunchyear]{\badspeed}
    node[anchor=west] {attack};
\end{spacetimediagram}
```

### Commands

**NOTE: Since version 2017/10/14, these commands no longer generate
a trailing semicolon (`;`).  This allows for greater flexibility with
TikZ syntax.**

For example, you can now append ` [->] node[anchor=…] {$…$}` to
a command to draw an arrow and a label at the end of a line; this
is useful for time-like worldlines that serve as temporal axes, and
lines of simultaneity that serve as spatial axes, of moving frames
(see the [example](#example) above).

However, documents written based on earlier versions of the package
may no longer generate syntactically correct PGFPlots syntax.
If you get the error message

```
TeX STOPPED: File ended while scanning use of \pgfplots@addplotimpl@expression@curl\ETC. []
```

or

```
Paragraph ended before \pgfplots@PREPARE@COORD@STREAM@end@ was complete. [ \$COMMAND[…]{…};]
```

**please make sure that all line commands are terminated by `;`**,
as in the [example](#example) above, before reporting an issue.

Also, as a result of the change, **`\spatial` exposes the command
`\relativitygammav`.  Do not use that command** in your documents that use
this package.  The identifier is intentionally prefixed to reduce
the probability of collision with your commands; however, if you happen
to use this command in your document already, as always, you can prevent
its being changed by `relativity.sty` if you enclose `\spatial` in braces:

```latex
  {
    \spatial[\goodcolor, domain=0:11.5]{0.42};
  }
```

#### `\lightlike[style][x_shift=0][t_shift=0][speed=1]`
Draws a light-like worldline
  * in style *`style`* (optional),
  * origin shifted in the x-direction by *`x_shift`* (default: 0),
  * and in the t-direction by *`t_shift`* (default: 0);

Different to `\lightlike*`, this draws only the worldline for the relative speed sgn(`speed`) (default: 1) multiplied by c.

Use the PGFPlots `domain` option to limit the x-range.

**NOTE: *Unlike* with other line commands, *all* arguments
of `\lightlike` are optional** because it is more common, and
therefore should be easier, to draw a light-like worldline
in the rest frame.  For that, just use `\lightlike` or
`\lightlike[style]`.  If you specify the speed within `{…}`,
indicating a *mandatory* parameter, instead of the proper
`[…]`, this will not affect the worldline but may lead
to unexpected results. For a speed of −c, you must therefore
use `\lightlike[…][…][…][-1]`; for such a worldline through
the origin, you can omit `style`, but must specify `x_shift`
and `t_shift` explicitly: `\lightlike[][0][0][-1]`

**Error messages like**

```
…:42: Package tikz Error: Cannot parse this coordinate. [ \end{spacetimediagram}]
```
**are indicative that you specified the speed as a
*mandatory* instead of an *optional* parameter.**

#### `\lightlike*[style][x_shift=0][t_shift=0]{}`
Draws light-like worldlines (for both c and -c)
  * in style *`style`* (optional),
  * origin shifted in the x-direction by *`x_shift`* (default: 0),
  * and in the t-direction by *`t_shift`* (default: 0).

#### `\spatial[style][time][xshift=0][tshift=0]{speed}`
Draws a line of simultaneity
  * in style *`style`* (optional)
  * for relative speed *`speed`*
  * and time *`time`* (default: 0),
  * shifted in the x-direction by *`x_shift`* (default: 0),
  * and in the t-direction by *`t_shift`* (default: 0).

**NOTE: *Unlike* with other line commands, the second optional
parameter of `\spatial` is _not_ `x_shift`, but the `time`
of events that are simultaneous in the respective frame
of reference** because it is more common, and therefore should
be easier, to draw lines of simultaneity where the origins
of the rest frame and the moving frame coincide. For example,
`\spatial[][2]{0.5}` draws the line of simultaneity for a
frame `time=2` in a frame moving at 0.5 c to the right in
the rest frame.

#### `\temporal[style][x_shift=0][t_start=0]{t_end}`
Draws a line of same location in the rest frame
  * in style *`style`* (optional)
  * parallel to the time axis (not function-based)
at x = *`x_shift`* (default: 0)
  * from t = *`t_start`* (default: 0)
  * to t = *`t_end`* (mandatory, no default).

#### `\worldline[style]{term}`
Draws a worldline in style *`style`* (optional)
based on *`term`* for the temporal coordinate
(use `x` for the spatial coordinate) (mandatory)

#### `\worldline*[style][x_shift=0][t_shift=0]{speed}`
Worldline in style *`style`* (optional)
  * based on constant relative speed *`speed`* (mandatory)
  * shifted in the x-direction by *`x_shift`* (default: 0),
  * and in the t-direction by *`t_shift`* (default: 0).
