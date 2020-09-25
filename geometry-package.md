

# The *geometry* package

This package provides a flexible and easy interface to page dimensions.
You can change the page layout with intuitive parameters. For instance,
if you want to set a margin to 2cm from each edge of the paper,
you can type just `\usepackage[margin=2cm]{geometry}`. 
The page layout can be changed in the middle of the document
with `\newgeometry` command.  

Package *geometry* is copyrighted by Hideo Umeki and David Carlisle
and is licenced under \LaTeX{} Project Public License. 

# Introduction

To set dimensions for page layout in \LaTeX{} is not straightforward. 
You need to adjust several \LaTeX{} native dimensions to place a text area
where you want.
If you want to center the text area in the paper you use, for example, 
you have to specify native dimensions as follows:

```
 \usepackage{calc}
 \setlength\textwidth{7in}
 \setlength\textheight{10in}
 \setlength\oddsidemargin{(\paperwidth-\textwidth)/2 - 1in}
 \setlength\topmargin{(\paperheight-\textheight
                       -\headheight-\headsep-\footskip)/2 - 1in}
```

Without package *calc*, the above example would need
more tedious settings. Package *geometry*  provides an easy
way to set page layout parameters. In this case, what you have to do
is just


```
 \usepackage[text={7in,10in},centering]{geometry} 
```

Besides centering problem, setting margins from each edge of the paper is
also troublesome. But *geometry* also make it easy.
If you want to set each margin to 1.5in, you can type


```
 \usepackage[margin=1.5in]{geometry} 
```

Thus, the *geometry* package has an auto-completion mechanism, in which
unspecified dimensions are automatically determined.
The *geometry* package will be also useful when you have to set page layout
obeying the following strict instructions: for example,


> The total allowable width of the text area is $6.5$ inches wide by $8.75$
> inches high. The top margin on each page should be $1.2$ inches from
> the top edge of the page. The left margin should be $0.9$ inch from 
> the left edge. The footer with page number should be at the bottom
> of the text area.


In this case, using *geometry* you can type

```
 \usepackage[total={6.5in,8.75in},
             top=1.2in, left=0.9in, includefoot]{geometry}
```

Setting a text area on the paper in document preparation system has some
analogy to placing a window on the background in the window system. 
The name *geometry* comes from the `-geometry` option used for specifying
a size and location of a window in X Window System.

# Page geometry

Figure \ref{fig:layout} shows the page layout dimensions defined
in the *geometry* package.
The page layout contains a *total body* (printable area) and *margins*. 
The *total body* consists of a *body* (text area) with an
optional *header*, *footer* and marginal notes (*marginpar*).
There are four margins: *left*, *right*, *top* and
*bottom*. For twosided documents, horizontal
margins should be called *inner* and *outer*.


\begin{tabular}{rcl}
 \emph{paper}&:&\emph{total body} and \emph{margins}\\
 \emph{total body}&:&\emph{body} (text area)\quad
           (optional \emph{head}, \emph{foot} and \emph{marginpar})\\
 \emph{margins}&:&\emph{left} (\emph{inner}), 
    \emph{right} (\emph{outer}), \emph{top} and \emph{bottom}
\end{tabular}


Each margin is measured from the corresponding edge of a paper. 
For example, left margin (inner margin) means a horizontal distance
between the left (inner) edge of the paper and that of the total body.
Therefore the left and top margins defined in *geometry* are different
from the native dimensions `\leftmargin` and `\topmargin`.
The size of a *body* (text area) can be modified by `\textwidth` and
`\textheight`. 

The dimensions for paper, total body and margins have the following
relations.

\begin{eqnarray}
 \label{eq:paperwidth}
 \emph{paperwidth} &=& \emph{left}+\emph{width}+\emph{right} \\
 \emph{paperheight} &=& \emph{top}+\emph{height}+\emph{bottom}
 \label{eq:paperheight}
\end{eqnarray}

\begin{figure}
 {\small
 {\unitlength=.62pt
 \begin{picture}(450,250)(-35,-10)
 \put(20,0){\framebox(170,230){}}
 \put(20,235){\makebox(170,230)[br]{paper}}
 \begingroup\thicklines
 \put(40,30){\framebox(120,170){}}\endgroup
 \put(40,30){\makebox(120,165)[tr]{total body}}
 \put(45,30){\makebox(0,170)[l]{height}}
 \put(40,35){\makebox(120,0)[bc]{width}}
 \put(50,-20){\makebox(120,0)[bc]{paperwidth}}
 \put(10,45){\makebox(0,170)[r]{paper-}}
 \put(10,30){\makebox(0,170)[r]{height}}
 \put(90,200){\makebox(0,30)[lc]{top}}
 \put(90,0){\makebox(0,30)[lc]{bottom}}
 \put(10,70){\makebox(0,0)[r]{left}}
 \put(10,55){\makebox(0,0)[r]{(inner)}}
 \put(200,70){\makebox(0,0)[l]{right}}
 \put(200,55){\makebox(0,0)[l]{(outer)}}
 \put(80,230){\vector(0,-1){30}}\put(80,30){\vector(0,-1){30}}
 \put(80,200){\vector(0,1){30}}\put(80,0){\vector(0,1){30}}
 \put(20,70){\vector(1,0){20}}\put(40,70){\vector(-1,0){20}}
 \put(160,70){\vector(1,0){30}}\put(190,70){\vector(-1,0){30}}
 \multiput(160,30)(5,0){24}{\line(1,0){2}}
 \multiput(160,200)(5,0){24}{\line(1,0){2}}
 \begingroup\thicklines
 \put(280,30){\framebox(120,170){}}\endgroup
 \put(283,133){\makebox(0,12)[l]{textheight}}
 \put(295,130){\vector(0,-1){100}}\put(295,150){\vector(0,1){50}}
 \multiput(280,220)(5,0){24}{\line(1,0){3}}
 \put(280,208){\makebox(120,20)[bc]{head}}
 \multiput(280,207)(5,0){24}{\line(1,0){3}}
 \put(420,225){\makebox(0,0)[l]{headheight}}
 \put(418,225){\line(-2,-1){20}}
 \put(420,213){\makebox(0,0)[l]{headsep}}
 \put(418,213){\line(-2,-1){20}}
 \put(420,12){\makebox(0,0)[l]{footskip}}
 \put(418,12){\line(-2,1){20}}
 \put(280,40){\makebox(120,140)[c]{body}}
 \put(305,45){\vector(-1,0){25}}\put(375,45){\vector(1,0){25}}
 \put(80,230){\vector(0,-1){30}}\put(80,30){\vector(0,-1){30}}
 \put(280,48){\makebox(120,0)[c]{textwidth}}
 \put(280,15){\makebox(120,10)[c]{foot}}
 \multiput(280,14)(5,0){24}{\line(1,0){2}}
 \put(410,30){\dashbox{3}(30,170){}}
 \put(415,30){\makebox(30,170)[l]{marginal note}}
 \put(425,45){\vector(-1,0){15}}\put(425,45){\vector(1,0){15}}
 \put(450,70){\makebox(0,0)[l]{marginparsep}}
 \put(448,70){\line(-3,-1){43}}
 \put(450,45){\makebox(0,0)[l]{marginparwidth}}
 \end{picture}}}
 \caption{
 Dimension names used in the \emph{geometry} package.
 \emph{Width} $=$ \emph{textwidth} and \emph{height} $=$ \emph{textheight} by default.
 \emph{Left}, \emph{right}, \emph{top} and \emph{bottom} are margins. 
 If margins on verso pages are swapped by \emph{twoside} option,
 margins specified by \emph{left} and \emph{right} options
 are used for the inside and outside margins respectively.
 \emph{Inner} and \emph{outer} are aliases of \emph{left} and \emph{right}
 respectively.}
 \label{fig:layout}
\end{figure}

The total body \emph{width} and \emph{height} would be defined:
 \begin{eqnarray}
  \label{eq:width}
  \emph{width} &:=& \emph{textwidth} \quad( +\>  \emph{marginparsep} + \emph{marginparwidth} )\\
  \emph{height} &:=& \emph{textheight} \quad(+\> \emph{headheight} + \emph{headsep} + \emph{footskip} )
  \label{eq:height}
 \end{eqnarray}
 
In Equation (\ref{eq:width}) *width* $:=$ *textwidth* by default, 
while *marginparsep* and *marginparwidth* are included in *width*
if *includemp* option is set *true*. 
In Equation (\ref{eq:height}), *height* $:=$ *textheight* by default. 
If *includehead* is set to *true*, *headheight* and *headsep* are
considered as a part of *height*.
In the same way, *includefoot* takes *footskip* into *height*. 
Figure \ref{fig:includes} shows how these options
work in the vertical direction.

\begin{figure}[H]
  \centering\small
  {\unitlength=.65pt
  \begin{picture}(490,280)(0,-10)
  \put(60,250){\makebox(120,0)[bl]{(a)default}}%
  \put(20,0){\framebox(170,230){}}
  \put(20,230){\makebox(170,15)[r]{paper}}
  \begingroup\thicklines
  \put(40,30){\framebox(120,165){}}\endgroup
  \put(70,165){\vector(0,1){30}}
  \put(55,145){\makebox(0,20)[lc]{textheight}}
  \put(70,145){\vector(0,-1){115}}
  \multiput(40,203)(5,0){24}{\line(1,0){3}}
  \multiput(40,213)(5,0){24}{\line(1,0){3}}
  \multiput(40,10)(5,0){24}{\line(1,0){3}}
  \put(40,203){\makebox(120,20)[bc]{head}}
  \put(40,40){\makebox(120,140)[c]{body}}
  \put(40,11){\makebox(120,10)[c]{foot}}
  \put(150,230){\vector(0,-1){35}}\put(150,30){\vector(0,-1){30}}
  \put(150,195){\vector(0,1){35}}\put(150,0){\vector(0,1){30}}
  \put(160,197){\makebox(0,30)[lc]{top}}
  \put(160,0){\makebox(0,30)[lc]{bottom}}
  \multiput(160,30)(5,0){24}{\line(1,0){2}}
  \multiput(160,195)(5,0){24}{\line(1,0){2}}
  \put(255,250){\makebox(120,0)[bl]
      {(b)includehead and includefoot}}%
  \put(260,0){\framebox(170,230){}}
  \put(260,230){\makebox(170,15)[r]{paper}}
  \begingroup\thicklines
  \put(280,30){\framebox(120,165){}}\endgroup
  \put(310,152){\vector(0,1){25}}
  \put(295,130){\makebox(0,20)[lc]{textheight}}
  \put(310,130){\vector(0,-1){80}}
  \multiput(280,184)(5,0){24}{\line(1,0){3}}
  \multiput(280,177)(5,0){24}{\line(1,0){3}}
  \multiput(280,50)(5,0){24}{\line(1,0){3}}
  \put(280,184){\makebox(120,10)[c]{head}}
  \put(280,40){\makebox(120,140)[c]{body}}
  \put(400,140){\line(1,1){45}}
  \put(437,187){\makebox(50,10)[l]{total body}}
  \put(280,31){\makebox(120,10)[c]{foot}}
  \put(370,230){\vector(0,-1){35}}\put(370,30){\vector(0,-1){30}}
  \put(370,195){\vector(0,1){35}}\put(370,0){\vector(0,1){30}}
  \put(380,197){\makebox(0,30)[lc]{top}}
  \put(380,0){\makebox(0,30)[lc]{bottom}}
  \end{picture}}
  \caption{
    \emph{Includehead} and \emph{includefoot} include the head and foot respectively
    into \emph{total body}. (a) \emph{height} $=$ \emph{textheight} (default).
    (b) \emph{height} $=$ \emph{textheight} $+$ \emph{headheight} $+$ \emph{headsep} $+$ 
    \emph{footskip} if \emph{includehead} and \emph{includefoot}. If the top and bottom
    margins are specified, \emph{includehead} and \emph{includefoot} result in
    shorter \emph{textheight}.
}
  \label{fig:includes}
\end{figure}

Thus, the page layout consists of three parts (lengths) in each
direction: one body and two margins. If the two of them are explicitly
specified, the other length is obvious and no need to be specified.
Figure \ref{fig:Labc} shows a simple model of page dimensions. 
When a length $L$ is given and is partitioned into the body $b$, the
margins $a$ and $c$, it's obvious that

\begin{equation}
   L=a+b+c  \label{eq:Labc}
\end{equation}

The specification with two of the three ($a$, $b$ and $c$) fixed
explicitly is solvable. If two or more are left unspecified
or "underspecified", Equation (\ref{eq:Labc}) cannot be solved
without any other relation between them. If all of them are
specified, then it needs to check whether or not they
satisfy Equation (\ref{eq:Labc}), that is too much specification or
"overspecified".

\begin{figure}[H]
  \centering
  {\unitlength=0.8pt
  \begin{picture}(300,60)(0,-5)
  \begingroup\linethickness{5pt}
  \put(0,5){\textcolor{green}{\line(1,0){60}}}
  \put(60,5){\textcolor{black}{\line(1,0){160}}}
  \put(220,5){\textcolor{green}{\line(1,0){80}}}
  \endgroup
  \put(0,15){\makebox(60,10)[b]{$a$}}
  \put(60,0){\line(0,1){20}}
  \put(60,15){\makebox(160,10)[b]{$b$}}
  \put(220,0){\line(0,1){20}}
  \put(220,15){\makebox(80,10)[b]{$c$}}
  \put(0,0){\line(0,1){50}}
  \put(150,35){\vector(-1,0){150}}
  \put(0,40){\makebox(300,10){$L$}}
  \put(150,35){\vector(1,0){150}}
  \put(300,0){\line(0,1){50}}
  \end{picture}}
  \caption{A simple model of page dimensions.}
  \label{fig:Labc}
\end{figure}

The *geometry* package has auto-completion mechanism that saves the
trouble of specifying the page layout dimensions. For example,
you can set

```
 \usepackage[width=14cm, left=3cm]{geometry}
```

on A4 paper. In this case you don't have to set the right margin.
The details of auto-completion will be described in
Section \ref{sec:rules}.

# User interface

## Commands

The *geometry* package provides the following commands:
 
 - `\geometry{`\meta{options}`}`
 - `\newgeometry{`\meta{options}`}` and `\restoregeometry`
 - `\savegeometry{`\meta{name}`}` and `\loadgeometry{`\meta{name}`}`

`\geometry{`\meta{options}`}`
: changes the page layout according to the options specified in the
argument. This command, if any, should be placed only in the
preamble (before `\begin{document}`).

The *geometry* package may be used as part of a class or another package
you use in your document. The command `\geometry` can overwrite
some of the settings in the preamble. Multiple use of `\geometry`
is allowed and then processed with the options concatenated.
If *geometry* is not yet loaded, you can use only
`\usepackage[`\meta{options}`]{geometry}` instead of `\geometry`.

`\newgeometry{`\meta{options}`}`
: changes the page layout mid-document. The command `\newgeometry` is almost
similar to `\geometry` except that `\newgeometry` disables all
the options specified by `\usepackage` and `\geometry` in
the preamble and skips papersize-related options. 

`\restoregeometry`
: restores the page layout specified in the preamble. This command
has no arguments. See Section \ref{sec:midchange} for details.

`\savegeometry{`\meta{name}`}`
: saves the page dimensions as \meta{name} where you put
this command.

`\loadgeometry{`\meta{name}`}`
: loads the page dimensions saved as \meta{name}. See
Section \ref{sec:midchange} for details.

## Optional argument

The *geometry* package adopts \emph{keyval} interface
\meta{key}`=`\meta{value} for the optional argument to
`\usepackage`, `\geometry` and `\newgeometry`.

The argument includes a list of comma-separated \emph{keyval}
options and has basic rules as follows:

- Multiple lines are allowed, while blank lines are not.
- Any spaces between words are ignored.
- Options are basically order-independent.

(There are some exceptions. See Section \ref{sec:optionorder} for details.)

 For example,

```
 \usepackage[ a5paper ,  hmargin = { 3cm,
               .8in } , height
            =  10in ]{geometry}
```

is equivalent to 

```
 \usepackage[height=10in,a5paper,hmargin={3cm,0.8in}]{geometry}
```

Some options are allowed to have sub-list, e.g. `{3cm,0.8in}`.
Note that the order of values in the sub-list is significant.
The above setting is also equivalent to the followings:

```
 \usepackage{geometry}
 \geometry{height=10in,a5paper,hmargin={3cm,0.8in}}
```

or 

```
 \usepackage[a5paper]{geometry}
 \geometry{hmargin={3cm,0.8in},height=8in}
 \geometry{height=10in}
```

Thus, multiple use of `\geometry` just appends options.

The *geometry* package supports package 
*calc*. For example,

```
 \usepackage{calc}
 \usepackage[textheight=20\baselineskip+10pt]{geometry}
```

## Option types

The *geometry* options are categorized into four types: 

Boolean type

:   takes a boolean value (\emph{true} or \emph{false}). If no value,
    \emph{true} is set by default:
    

    \meta{key} `=` \emph{true} `|` \emph{false}
    
    \meta{key} with no value is equivalent to 
    \meta{key} `=` \emph{true}.
    
    
    **Examples:**  
    `verbose=true`, `includehead`, 
    `twoside=false`


    Paper name is the exception. The preferred paper name should be set
    with no values. Whatever value is given, it is ignored. For
    instance, `a4paper=XXX` is equivalent to `a4paper`.

Single-valued type

:   takes a mandatory value:

    \meta{key} `=` \meta{value}

    **Examples:**  
    `width=7in`, `left=1.25in`,
    `footskip=1cm`, `height=.86\paperheight`


Double-valued type

:   takes a pair of comma-separated values in braces. The two values can
    be shortened to one value if they are identical:
    
    \meta{key}`={`\meta{value1}`,`\meta{value2}`}`

    \meta{key}`=`\meta{value} is equivalent to 
              \meta{key}`={`\meta{value},\meta{value}`}`.


    **Examples:**  
    `hmargin={1.5in,1in}`, `scale=0.8`,
    `body={7in,10in}`

\pagebreak

Triple-valued type

:   takes three mandatory, comma-separated values in braces:
    
    \meta{key}`={`\meta{value1}`,`\meta{value2}`,`\meta{value3}`}`
  
    Each value must be a dimension or null. When you give an empty value
    or `*`, it means null and leaves the appropriate value 
    to the auto-completion mechanism. You need to specify at least one
    dimension, typically two dimensions. You can set nulls for all the 
    values, but it makes no sense.

    **Examples:**  
    `hdivide={2cm,*,1cm}`, `vdivide={3cm,19cm, }`,
    `divide={1in,*,1in}`

# Option details

 This section describes all options available in *geometry*.
 Paper size, drivers and "other options" are not available 
 as arguments of `\newgeometry` (See Section \ref{sec:midchange}).

## Paper size\label{sec:paper}
 
 The options below set paper/media size and orientation.
 
`paper | papername`

:   specifies the paper size by name: 
    
    `paper=`\meta{paper-name}
    
    For convenience, you can specify the paper name without `paper=`.
    For example, `a4paper` is equivalent to `paper=a4paper`.

\meta{paper-name} 

:   specifies paper name.  The value part is ignored even if any.
    For example, the followings have the same effect:
    `a5paper`, `a5paper=true`, `a5paper=false` and so forth.

    `a[0-6]paper`, `b[0-6]paper` and `c[0-6]paper` are ISO A, B and C
    series of paper sizes respectively.

    The JIS (Japanese Industrial Standards) A-series is identical to the
    ISO A-series, but the JIS B-series is different from the ISO B-series.
    `b[0-6]j` should be used for the JIS B-series. 
    
    \meta{paper-name} may be one of: 
   
    `a0paper`, `a1paper`, `a2paper`, `a3paper`, `a4paper`, `a5paper`, `a6paper`, 
    `b0paper`, `b1paper`, `b2paper`, `b3paper`, `b4paper`, `b5paper`, `b6paper`, 
    `c0paper`, `c1paper`, `c2paper`, `c3paper`, `c4paper`, `c5paper`, `c6paper`, 
    `b0j`, `b1j`, `b2j`, `b3j`, `b4j`, `b5j`, `b6j`, `ansiapaper`, `ansibpaper`,
    `ansicpaper`, `ansidpaper`, `ansiepaper`, `letterpaper`, `executivepaper`, 
    or `legalpaper`.
   
`screen` 

:   a special paper size with (W,H) = (225mm,180mm).
    For presentation with PC and video projector, `screen,centering`
    with `slide` documentclass would be useful.

`paperwidth` 
:  width of the paper: 
    
    `paperwidth=`\meta{length}

`paperheight`
:  height of the paper: 

    `paperheight=`\meta{length}

`papersize` 
:  width and height of the paper: 

    `papersize={`\meta{width},\meta{height}`}` or `papersize=`\meta{length}

`landscape` 
:  switches the paper orientation to landscape mode.

`portrait` 

: switches the paper orientation to portrait mode.
  This is equivalent to `landscape=false`.

 The options for paper names (e.g., `a4paper`) and orientation
 (`portrait` and `landscape`) can be set as document class options. 
 For example, you can set `\documentclass[a4paper,landscape]{article}`, 
 then `a4paper` and `landscape` are processed in *geometry* as well.
 This is also the case for `twoside` and `twocolumn`
 (see also Section \ref{sec:dimension}).

## Layout size

  You can specify the layout area with options described in this
  section regardless of the paper size.
  The options would help to print the specified layout to a different
  sized paper.  For example, with `a4paper` and `layout=a5paper`, the
  package uses A5 layout to calculate margins on A4 paper.
  The layout size defaults to the same as the paper.
  The options for the layout size are available in `\newgeometry`,
  so that you can change the layout size in the middle of the document.
  The paper size itself can't be changed though.
  Figure \ref{fig:layoutandpaper} shows what the difference between
  \emph{layout} and \emph{paper} is.
 
\begin{figure}[H]
{\small
  {\unitlength=.65pt
  \begin{picture}(450,250)(-60,-10)
  \put(20,0){\makebox(168,12)[r]{paper}}
  \put(20,0){\framebox(170,230){}}
  \put(21,40){\dashbox{3}(140,189){}}
  \put(21,28){\makebox(140,12)[r]{layout}}
  \put(40,50){\makebox(100,10){foot}}
  \put(40,50){\line(1,0){100}}
  \put(40,65){\framebox(100,125){body}}
  \put(40,200){\framebox(100,10){head}}
  \put(20,230){\makebox(140,20){layoutwidth}}
  \put(40,240){\vector(-1,0){20}}
  \put(140,240){\vector(1,0){20}}
  \put(10,145){\vector(0,1){85}}
  \put(15,125){\makebox(0,20)[r]{layout-}}
  \put(15,110){\makebox(0,20)[r]{height}}
  \put(10,110){\vector(0,-1){70}}
  \put(280,0){\makebox(168,12)[r]{paper}}
  \put(280,0){\framebox(170,230){}}
  \put(293,35){\dashbox{3}(140,189){}}
  \put(293,23){\makebox(140,12)[r]{layout}}
  \put(312,45){\makebox(100,10){foot}}
  \put(312,45){\line(1,0){100}}
  \put(312,60){\framebox(100,125){body}}
  \put(312,195){\framebox(100,10){head}}
  \put(235,230){\makebox(80,20)[l]{layouthoffset}}
  \put(260,210){\vector(1,0){20}}
  \put(308,210){\vector(-1,0){15}}
  \put(260,210){\line(-1,2){10}}
  \put(355,230){\makebox(100,20){layoutvoffset}}
  \put(350,250){\vector(0,-1){20}}
  \put(350,209){\vector(0,1){15}}
  \end{picture}}}
  \caption{
  The dimensions related to the layout size. Note that the layout size
  defaults to the same size as the paper, so you don't have to specify
  layout-related options explicitly in most cases.
  }
  \label{fig:layoutandpaper}
 \end{figure}
 
`layout`
:   specifies the layout size by paper name: 

    `layout=`\meta{paper-name} 

    All the paper names defined in *geometry* are available. See Section \ref{sec:paper} for details.

`layoutwidth`
:   width of the layout: 

    `layoutwidth=`\meta{length}

`layoutheight`
:   height of the layout: 

    `layoutheight=`\meta{length}

`layoutsize`
:   width and height of the layout:
  
    `layoutsize={`\meta{width}`,`\meta{height}`}` or `layoutsize=`\meta{length}

`layouthoffset`
:   specifies the horizontal offset from the left edge of the paper: 

    `layouthoffset=`\meta{length}

`layoutvoffset`
:   specifies the vertical offset from the top edge of the paper: 

    `layoutvoffset=`\meta{length}

`layoutoffset`
:   specifies both horizontal and vertical offsets: 

    `layoutoffset={`\meta{hoffset}`,`\meta{voffset}`}` or `layoutsize=`\meta{length}
 
## Body size\label{sec:body}

 The options specifying the size of *total body* are described in this
 section.

`hscale`
:   ratio of width of *total body* to `\paperwidth`. 

    `hscale=`\meta{h-scale}, e.g., `hscale=0.8` is equivalent to
    `width=0.8\paperwidth`. ($0.7$ by default)

`vscale`
:   ratio of height of *total body* to `\paperheight`, e.g.,
    `vscale=`\meta{v-scale} ($0.7$ by default). `vscale=0.9` is equivalent
    to `height=0.9\paperheight`.

`scale`
:   ratio of *total body* to the paper:

    `scale={`\meta{h-scale}`,`\meta{v-scale}`}` or `scale=`\meta{scale}.
    ($0.7$ by default)

`width | totalwidth`
:   width of *total body*. 

    `width=`\meta{length} or `totalwidth=`\meta{length}. 

    This dimension defaults to \emph{textwidth},
    but if \emph{includemp} is set to \emph{true}, \emph{width} $\ge$ \emph{textwidth} 
    because \emph{width} includes the width of the marginal notes.
    If \emph{textwidth} and \emph{width} are specified at the same time, 
    \emph{textwidth} takes priority over \emph{width}.

`height | totalheight`
:    height of *total body*, excluding header and footer by default.
     If *includehead* or *includefoot* is set, *height* includes
     the head or foot of the page as well as *textheight*:
    
     `height=`\meta{length} or `totalheight=`\meta{length} 

     If both *textheight* and *height* are specified, *height* will be ignored.

`total`
: width and height of *total body*:

    `total=`\meta{width}`,`\meta{height} or `total=`\meta{length}

`textwidth`
: specifies *textwidth*, the width of *body* 
    (the text area): 

    `textwidth=`\meta{length}

`textheight`
: specifies *textheight*, the height of
    *body* (the text area): 

    `textheight=`\meta{length}

`text | body`
: specifies both *textwidth* and *textheight*
    of the body of page: 

    `body={`\meta{width}`,`\meta{height}`}` or `text=`\meta{length}

`lines`
:   enables users to specify *textheight* by the number
    of lines: 

    `lines`=\meta{integer}

`includehead`
: includes the head of the page, \emph{headheight}
    and \emph{headsep}, into *total body*. It is set to \emph{false} by
    default. It is opposite to `ignorehead`. See
    Figure \ref{fig:includes} and Figure \ref{fig:modes}.

`includefoot`
: includes the foot of the page, \emph{footskip},
    into \emph{total body}. It is opposite to `ignorefoot`.
    It is *false* by default. See Figure \ref{fig:includes} and
    Figure \ref{fig:modes}.

`includeheadfoot` 
:    sets both *includehead* and *includefoot* to *true*, which is opposite
    to `ignoreheadfoot`. See Figure \ref{fig:includes} and
    Figure \ref{fig:modes}.

`includemp`
: includes the margin notes,  *marginparwidth*
    and *marginparsep*, into *body* when calculating horizontal
    calculation.

`includeall`
: sets both *includeheadfoot* and *includemp* to
    *true*. See Figure \ref{fig:modes}.

`ignorehead`
:  disregards the head of the page,
    *headheight* and *headsep*, in determining vertical layout, but does not
    change those lengths. It is equivalent to `includehead=false`. It is set
    to *true* by default. See also `includehead`.

`ignorefoot`
: disregards the foot of page, *footskip*,
    in determining vertical layout, but does not change that length.
    This option defaults to *true*. See also `includefoot`.

`ignoreheadfoot`
:  sets both *ignorehead* and *ignorefoot*
    to *true*. See also `includeheadfoot`.

`ignoremp`
: disregards the marginal notes in determining the
    horizontal margins (defaults to *true*). If marginal notes overrun
    the page, the warning message will be displayed when `verbose=true`.
    See also `includemp` and Figure \ref{fig:modes}.

`ignoreall`
: sets both *ignoreheadfoot* and *ignoremp* to *true*. 
    See also `includeall`.

`heightrounded`
:   This option rounds *textheight* to *n*-times (where *n* is
    an integer) of *baselineskip* plus *topskip* to avoid 
    "underfull vbox" in some cases. For example, if *textheight* is
    486pt with `baselineskip 12pt` and `topskip 10pt`, then
    $$\underbrace{478\textrm{pt}}_{39\times12\textrm{pt}+10\textrm{pt}}\
     < \; 486\textrm{pt} \; < 
    \underbrace{490\textrm{pt}}_{40\times12\textrm{pt}+10\textrm{pt}}$$
    as a result *textheight* is rounded to 490pt. `heightrounded=false`
    by default.

 Figure \ref{fig:modes} illustrates various layouts with different layout
 modes. The dimensions for a header and a footer can be controlled by
 *nohead* or *nofoot* mode, which sets each length to 0pt directly.
 On the other hand, options with the prefix `ignore` do *not*
 change the corresponding native dimensions.

 \begin{figure}
  {\small
  {\unitlength=.65pt
  \begin{picture}(460,525)(-30,0)
  \put( 20,310){\framebox(120,170){}}
  \put( 20,507){\makebox(120,0)[bl]%
  {(a) includeheadfoot}}
  \put( 20,460){\line(1,0){120}}\put( 20,450){\line(1,0){120}}
  \put( 20,330){\line(1,0){120}}
  \put( 20,485){\makebox(120,0)[br]{total body}}
  \put( 20,335){\makebox(120,0)[bc]{textwidth}}
  \put(150,470){\makebox(0,0)[l]{headheight}}
  \put(150,450){\makebox(0,0)[l]{headsep}}
  \put(150,390){\makebox(0,0)[l]{textheight}}
  \put(150,320){\makebox(0,0)[l]{footskip}}
  \put( 10,460){\makebox(120,20)[bc]{head}}
  \put( 10,320){\makebox(120,140)[c]{body}}
  \put( 10,310){\makebox(120,10)[c]{foot}}
  \put(250,310){\framebox(120,170){}}
  \put(250,507){\makebox(120,0)[bl]%
  {(b) includeall}}
  \put(250,460){\line(1,0){95}}\put(250,450){\line(1,0){95}}
  \put(250,330){\line(1,0){95}}\put(345,330){\line(0,1){120}}
  \put(350,330){\line(0,1){120}}\put(350,450){\line(1,0){20}}
  \put(350,330){\line(1,0){20}}
  \put(250,485){\makebox(120,0)[br]{total body}}
  \put(250,460){\makebox(95,20)[bc]{head}}
  \put(250,320){\makebox(95,140)[c]{body}}
  \put(385,390){\makebox(95,0)[cl]%
  {\shortstack[l]{marginal\\note}}}
  \put(250,310){\makebox(95,10)[c]{foot}}
  \put(250,335){\makebox(95,0)[bc]{textwidth}}
  \multiput(360, 390)(4,0){6}{\line(1,0){2}}
  \multiput(348,333)(0,-4){12}{\line(0,1){2}}
  \multiput(360,333)(0,-4){8}{\line(0,1){2}}
  \put(355,292){\makebox(0,0)[bl]{marginparwidth}}
  \put(345,275){\makebox(0,0)[bl]{marginparsep}}
  \put( 20, 40){\framebox(120,170){}}
  \put( 20,237){\makebox(120,0)[bl]%
  {(c) includefoot}}
  \put( 20, 60){\line(1,0){120}}
  \put( 20,215){\makebox(120,0)[br]{total body}}
  \put(150,130){\makebox(0,0)[l]{textheight}}
  \put(150, 50){\makebox(0,0)[l]{footskip}}
  \put( 20, 50){\makebox(120,160)[c]{body}}
  \put( 20, 40){\makebox(120,10)[c]{foot}}
  \put( 20, 65){\makebox(120,10)[c]{textwidth}}
  \put(250, 40){\framebox(120,170){}}
  \put(250,237){\makebox(120,0)[bl]%
  {(d) includefoot,includemp}}
  \put(250, 60){\line(1,0){95}}\put(350, 60){\line(1,0){20}}
  \put(250,215){\makebox(120,0)[br]{total body}}
  \put(250, 50){\makebox(95,160)[c]{body}}
  \put(385,130){\makebox(95,0)[cl]%
  {\shortstack[l]{marginal\\note}}}
  \put(250, 40){\makebox(95,10)[c]{foot}}
  \put(250, 65){\makebox(95,0)[bc]{textwidth}}
  \put(345, 60){\line(0,1){150}}\put(350, 60){\line(0,1){150}}
  \multiput(360, 130)(4,0){6}{\line(1,0){2}}
  \multiput(348, 63)(0,-4){12}{\line(0,1){2}}
  \multiput(360, 63)(0,-4){8}{\line(0,1){2}}
  \put(355,22){\makebox(0,0)[bl]{marginparwidth}}
  \put(345, 5){\makebox(0,0)[bl]{marginparsep}}
  \end{picture}}}
  \caption{Sample layouts for \emph{total body} with different switches:
    (a) \emph{includeheadfoot}, (b) \emph{includeall}, (c) \emph{includefoot}
     and (d) \emph{includefoot,includemp}. 
    If \emph{reversemp} is set to \emph{true}, the location of the
    marginal notes are swapped on every page.
    Option \emph{twoside} swaps both margins and marginal notes on verso pages.
    Note that the marginal note, if any, is printed despite
    \emph{ignoremp} or \emph{includemp} $=$ \emph{false} and overrun the page in some cases.
  }
  \label{fig:modes}
 \end{figure}

 The following options can specify body and margins simultaneously with
 three comma-separated values in braces.

`hdivide`
:   horizontal partitions (*left*,*width*,*right*):

    `hdivide={`\meta{left margin}`,`\meta{width}`,`\meta{right margin}`}` 

    Note that you should not specify all of the three parameters.
    The best way of using this option is to specify two of three and 
    leave the rest with *null* (nothing) or `*`. For example, when you set
    `hdivide={2cm,15cm, }`, the margin from the right-side edge of page
    will be determined calculating *paperwidth* $-$ 2cm $-$ 15cm.

`vdivide`
:   vertical partitions (*top*,*height*,*bottom*):

    `vdivide={`\meta{top margin}`,`\meta{height}`,`\meta{bottom margin}`}`

`divide`
:   `divide={`$A$`,`$B$`,`$C$`}` is interpreted  as 
    `hdivide={`$A$`,`$B$`,`$C$`}` and `vdivide={`$A$`,`$B$`,`$C$`}`.

## Margin size\label{sec:margin}

 The options specifying the size of the margins are listed below.

`left | lmargin | inner`
:    left margin (for oneside) or inner margin (for twoside) of 
    *total body*. In other words, the distance between the left (inner)
    edge of the paper and that of *total body*: 

    `left=`\meta{length}

    `inner` has no special meaning, just an alias of `left` and `lmargin`.

`right | rmargin | outer`
:   right or outer margin of *total body*: 

    `right=`\meta{length}

`top | tmargin`
:   top margin of the page: 

    `top=`\meta{length}

    Note this option has nothing to do with the native dimension
    `\topmargin`.

`bottom | bmargin`
:   bottom margin of the page: 

    `bottom=`\meta{length}

`hmargin`
:   left and right margin:
 
    `hmargin={`\meta{left margin}`,`\meta{right margin}`}` or `hmargin=`\meta{length}.

`vmargin`
:   top and bottom margin:

    `vmargin={`\meta{top margin}`,`\meta{bottom margin}`}` or `vmargin=`\meta{length}

`margin`
:   `margin={`$A$`,`$B$`}` is equivalent to 
    `hmargin={`$A$`,`$B$`}` and `vmargin={`$A$`,`$B$`}`.
    `margin=`$A$ is automatically expanded to `hmargin=`$A$ and `vmargin=`$A$.

`hmarginratio`
:   horizontal margin ratio of *left* (inner) to *right* (outer). 
   The value of \meta{ratio} should be specified with colon-separated 
   two values. Each value should be a positive integer less than 100
   to prevent arithmetic overflow, e.g., `2:3` instead of `1:1.5`.
   The default ratio is `1:1` for *oneside*, `2:3` for *twoside*.

`vmarginratio`
:    vertical margin ratio of *top* to *bottom*. The default ratio is `2:3`.

`marginratio | ratio`
:   horizontal and vertical margin ratios:

    `marginratio={`\meta{horizontal ratio}`,`\meta{vertical ratio}`}` or
    `marginratio=`\meta{ratio}

`hcentering`

: sets auto-centering horizontally and is
   equivalent to `hmarginratio=1:1`. It is set to *true* by default for
   *oneside*. See also `hmarginratio`.

`vcentering`

: sets auto-centering vertically and is
   equivalent to `vmarginratio=1:1`. The default is *false*.
   See also `vmarginratio`.

`centering`

: sets auto-centering and is equivalent to
   `marginratio=1:1`. See also `marginratio`. The default is *false*.
   See also `marginratio`.

`twoside`

: switches on twoside mode with left and right margins swapped
   on verso pages. The option sets `\@twoside` and `\@mparswitch` 
   switches. See also `asymmetric`.

`asymmetric`

: implements a twosided layout in which margins are
   not swapped on alternate pages (by setting *oddsidemargin* to 
   *evensidemargin* $+$ *bindingoffset*) and in which the marginal notes
   stay always on the same side. This option can be used as an alternative
   to the twoside option. See also *twoside*.

`bindingoffset`

:   removes a specified space from the lefthand-side of the page 
    for *oneside* or the inner-side for *twoside*:

    `bindingoffset=`\meta{length} 

    This is useful if pages are bound by a press binding (glued, 
    stitched, stapled \ldots). See Figure \ref{fig:bindingoffset}.

`hdivide`
: See description in Section \ref{sec:body}.

`vdivide`
: See description in Section \ref{sec:body}.

`divide`
: See description in Section \ref{sec:body}.
 
\begin{figure}
  {\small
  {\unitlength=.65pt
  \begin{picture}(500,270)(0,0)
  \put(20,0){\framebox(170,230){}}
  \put(20,255){\makebox(80,20)[l]{a) every page for oneside or}}
  \put(20,240){\makebox(80,20)[l]{\hspace{3ex}odd pages for twoside}}
  \put(110,225){\makebox(80,20)[r]{paper}}
  \put(55,37){\framebox(110,170)[tc]{total body}}
  \multiput(38,0)(0,7){33}{\line(0,1){4}}
  \put(38,100){\vector(1,0){17}}\put(55,100){\vector(-1,0){17}}
  \put(60,95){\makebox(80,10)[l]{left}}
  \put(60,80){\makebox(80,10)[l]{(inner)}}
  \put(165,100){\vector(1,0){25}}\put(190,100){\vector(-1,0){25}}
  \put(195,95){\makebox(80,10)[l]{right}}
  \put(195,80){\makebox(80,10)[l]{(outer)}}
  \put(20,16){\vector(1,0){18}}
  \put(45,10){\makebox(80,10)[bl]{bindingoffset}}
  \put(280,255){\makebox(80,20)[l]{b) even (back) pages for twoside}}
  \put(280,0){\framebox(170,230){}}
  \put(370,225){\makebox(80,20)[r]{paper}}
  \put(305,37){\framebox(110,170)[tc]{total body}}
  \multiput(432,0)(0,7){33}{\line(0,1){4}}
  \put(280,100){\vector(1,0){25}}\put(305,100){\vector(-1,0){25}}
  \put(310,95){\makebox(80,10)[l]{outer}}
  \put(310,80){\makebox(80,10)[l]{(right)}}
  \put(415,100){\vector(1,0){17}}\put(432,100){\vector(-1,0){17}}
  \put(373,95){\makebox(80,10)[l]{inner}}
  \put(373,80){\makebox(80,10)[l]{(left)}}
  \put(450,16){\vector(-1,0){18}}
  \put(330,10){\makebox(80,10)[bl]{bindingoffset}}
  \end{picture}}}
  \caption{
   The option \emph{bindingoffset} adds the specified length to the inner margin.
   Note that \emph{twoside} option swaps the horizontal margins and the
   marginal notes together with \emph{bindingoffset} on even pages (see
   b)), but \emph{asymmetric} option suppresses the swap of the
   margins and marginal notes (but \emph{bindingoffset} is still swapped).
   }
  \label{fig:bindingoffset}
 \end{figure}

## Native dimensions\label{sec:dimension}

The options below overwrite \LaTeX{} native dimensions and switches for page
layout (See the right-hand side in Figure \ref{fig:layout}).

`headheight | head`
:    modifies *headheight*, height of header:

    `headheight=`\meta{length} or `head=`\meta{length}

`headsep`
:   modifies *headsep*, separation between header and text
    (body):

    `headsep=`\meta{length}

`footskip | foot`
: modifies *footskip*, distance separation
    between baseline of last line of text and baseline of footer:

    `footskip=`\meta{length} or `foot=`\meta{length}

`nohead`
: eliminates spaces for the head of the page, which is
    equivalent to both `headheight=0pt` and `headsep=0pt`.

`nofoot`
: eliminates spaces for the foot of the page, which is
    equivalent to `footskip=0pt`.

`noheadfoot`
: equivalent to `nohead` and `nofoot`, which means that
    *headheight*, *headsep* and *footskip* are all set to 0pt.

`footnotesep`
: changes the dimension \emph{skipfootins}, separation
    between the bottom of text body and the top of footnote text.

`marginparwidth | marginpar` 
:   modifies `marginparwidth`, width of the marginal notes:

    `marginparwidth=`\meta{length}

`marginparsep`
:   modifies `marginparsep`, separation between
    body and marginal notes:

    `marginparsep=`\meta{length}

`nomarginpar`
: shrinks spaces for marginal notes to 0pt, which
    is equivalent to `marginparwidth=0pt` and `marginparsep=0pt`.

`columnsep`
: modifies *columnsep*, the separation between two
    columns in *twocolumn* mode.

`hoffset`
:   modifies *hoffset*:

    `hoffset=`\meta{length}

`voffset`
:   modifies *voffset*: 

    `voffset=`\meta{length}

`offset`
:   horizontal and vertical offset:

    `offset={`\meta{hoffset}`,`\meta{voffset}`}` or `offset=`\meta{length}

`twocolumn`
: sets *twocolumn* mode with `@twocolumntrue`.
   `twocolumn=false` denotes *onecolumn* mode with`@twocolumnfalse`.
   Instead of `twocolumn=false`, you can specify `onecolumn` (which
   defaults to *true*)

`onecolumn`
: works as `twocolumn=false`. On the other hand,
   `onecolumn=false` is equivalent to `twocolumn`. 

`twoside`
: sets both `@twosidetrue` and `@mparswitchtrue`.
   See Section \ref{sec:margin}.

`textwidth`
: sets *textwidth* directly. See Section \ref{sec:body}.

`textheight`
: sets *textheight* directly. See Section \ref{sec:body}.

`reversemp | reversemarginpar` 
:  makes the marginal notes appear in the *left* (inner) margin with
   `@reversemargintrue`. The option doesn't change *includemp* mode.
   It's set *false* by default.

## Drivers\label{sec:drivers}
 
The package supports drivers *dvips*, *dvipdfm*, *pdftex*, *luatex*,
*xetex* and *vtex*. You can also set *dvipdfm* for *dvipdfmx* and
*xdvipdfmx* The options *dvipdfmx* and *xdvipdfmx* are also supported
as aliases for the *dvipdfm* option.
*pdftex* for *pdflatex*, and *vtex* for
VTeX environment.

The driver options are exclusive. The driver can be set by either
`driver=`\meta{driver name} or any of the drivers directly like `pdftex`.
By default, *geometry* guesses the driver appropriate to the system
in use. Therefore, you don't have to set a driver in most cases.
However, if you want to use `dvipdfm`, you should specify it explicitly.

`driver`
:   specifies the driver with `driver=`\meta{driver name}.
 
    *dvips*, *dvipdfm*, *pdftex*, *luatex*, *vtex*, *xetex*, *auto* and *none* are
    available as a driver name. The names except for *auto* and *none* can
    be specified directly with the name without `driver=`.

    `driver=auto` makes the auto-detection work whatever the previous setting is. 

    `driver=none` disables the auto-detection and sets no driver, which
    may be useful when you want to let other package work out the driver
    setting. For example, if you want to use `crop` package with *geometry*,
    you should call `\usepackage[driver=none]{geometry}` before
    the `crop` package.

`dvips`
: writes the paper size in dvi output with the `special`
     macro. If you use *dvips* as a DVI-to-PS driver,
     for example, to print a document with `\geometry{a3paper,landscape}`
     on A3 paper in landscape orientation, you don't need options
     `-t a3 -t landscape` to *dvips*. 

`dvipdfm`
: works like *dvips* except for landscape correction.
      You can set this option when using *dvipdfmx* and
      *xdvipdfmx* to process the dvi output.

`pdftex`
: sets *pdfpagewidth* and *pdfpageheight*
      internally.

`luatex`
: sets *pagewidth* and *pageheight* internally.

`xetex`
: is the same as `pdftex` except for ignoring
     `\pdf{h,v}origin` undefined in XeLaTeX. This option is introduced in
     the version 5. Note that `geometry.cfg` in \TeX{} Live, which disables the
     auto-detection routine and sets *pdftex*, is no longer necessary,
     but has no problem even though it's left undeleted.
     Instead of *xetex*, you can specify *dvipdfm* with XeLaTeX
     if you want to use specials of *dvipdfm* XeTeX supports.

`vtex`
: sets dimensions *mediawidth* and *mediaheight*
     for VTeX. When this driver is selected (explicitly or
     automatically), *geometry* will auto-detect which output mode
     (DVI, PDF or PS) is selected in VTeX, and do proper
     settings for it.
 
If explicit driver setting is mismatched with the typesetting program
 in use, the default driver *dvips* would be selected.

## Other options

The other useful options are described here.

`verbose`
: displays the parameter results on the terminal.
   `verbose=false` (default) still puts them into the log file.

`reset`
:   sets back the layout dimensions and switches to the
    settings before *geometry* is loaded. Options given in 
    `geometry.cfg` are also cleared.
    Note that this cannot reset *pass* and *mag* with *truedimen*.
    `reset=false` has no effect and cannot cancel the previous
    `reset`($=$ *true*) if any. For example, when you go
    
    ```
    \documentclass[landscape]{article}
    \usepackage[twoside,reset,left=2cm]{geometry}
    ```

    with `\ExecuteOptions{scale=0.9}` in `geometry.cfg`,
    then as a result, `landscape` and `left=2cm` remain effective,
    and `scale=0.9` and `twoside` are ineffective.

\pagebreak

`mag`
:   sets magnification value (*mag*) and automatically modifies 
    *hoffset* and *voffset* according to the magnification:

    `mag=`\meta{value}

    Note that \meta{value} should be an integer value
    with 1000 as a normal size. For example, `mag=1414` with `a4paper`
    provides an enlarged print fitting in `a3paper`, which is $1.414$
    (=$\sqrt{2}$) times larger than `a4paper`. Font enlargement needs extra
    disk space. Note that setting `mag` should precede any other
    settings with "true" dimensions, such as  `1.5truein`, `2truecm`
    and so on. See also `truedimen` option.

`truedimen`
: changes all internal explicit dimension values into 
   *true* dimensions, e.g., `1in` is changed to `1truein`.
   Typically this option will be used together with *mag* option. Note that
   this is ineffective against externally specified dimensions. For example,
   when you set `mag=1440, margin=10pt, truedimen`, margins are
   not *true* but magnified. If you want to set exact margins, you should
   set like `mag=1440, margin=10truept, truedimen` instead.

`pass`
: disables all of the geometry options and calculations
   except *verbose* and *showframe*. It is order-independent and can be
   used for checking out the page layout of the documentclass, other
   packages and manual settings without *geometry*.

`showframe`
: shows visible frames for the text area and page,
   and the lines for the head and foot on the first page.

`showcrop`
: prints crop marks at each corner of user-specified
  layout area.

# Processing options\label{sec:process}
 
## Order of loading\label{sec:loadorder}

If there's `geometry.cfg` somewhere \TeX{} can find it,*geometry* loads
it first. For example, in `geometry.cfg` you may write
`\ExecuteOptions{a4paper}`, which specifies A4 paper as the default
paper. Basically you can use all the options defined in *geometry* with
`\ExecuteOptions{}`.

The order of loading in the preamble of your document is as follows:

 - `geometry.cfg` if it exists.
 - Options specified with `\documentclass[`\meta{options}`]{...}`.
 - Options specified with `\usepackage[`\meta{options}`]{geometry}`
 - Options specified with `\geometry{`\meta{options}`}`, which
 can be called multiple times. (`reset` option will cancel the
 specified options ever given in  `\usepackage{geometry}` or
 `\geometry`.)

## Order of options\label{sec:optionorder}

The specification of *geometry* options is order-independent,
and overwrites the previous one for the same setting.
For example, 
```
 [left=2cm, right=3cm]
``` 
is equivalent to 
```
 [right=3cm, left=2cm].
```
The options called multiple times overwrite the previous
settings. For example, 
```
 [verbose=true, verbose=false]
```
results in 
```
 verbose=false
```

 The `[hmargin={3cm,2cm}, left=1cm]` is the same as `hmargin={1cm,2cm}`, 
 where the left (or inner) margin is overwritten by `left=1cm`. 

 The *reset* and *mag* are exceptions.
 The *reset* option removes all the geometry options (except *pass*)
 before it. If you set
 
```
 \documentclass[landscape]{article}
 \usepackage[margin=1cm,twoside]{geometry}
 \geometry{a5paper, reset, left=2cm}
```

 then *margin* $=$ 1cm, *twoside* and *a5paper* are removed, and 
 is eventually equivalent to
 
```
\documentclass[landscape]{article}
\usepackage[left=2cm]{geometry}
```

 The *mag* option should be set in advance of any other settings with
 *true* length, such as `left=1.5truecm`, `width=5truein` and so on.
 The `\mag` primitive can be set before this package is called.

## Priority\label{sec:priority}
  
 There are several ways to set dimensions of the *body*:
 `scale`, `total`, `text` and `lines`. The *geometry* package gives higher
 priority to the more concrete specification. Here is the priority
 rule for *body*.
 
$$\begin{array}{c}
 \textrm{priority:}\qquad\textrm{low}\quad
    \longrightarrow\quad\textrm{high}\\[1em]
 \left\{\begin{array}{l}\emph{hscale}\\\emph{vscale}\\\emph{scale}
        \end{array}\right\} <
 \left\{\begin{array}{l}\emph{width}\\\emph{height}\\\emph{total}
        \end{array}\right\} <
 \left\{\begin{array}{l}\emph{textwidth}\\\emph{textheight}\\\emph{text}
        \end{array}\right\} < \emph{lines}
 \end{array}$$

 For example, 
 
```
 \usepackage[hscale=0.8, textwidth=7in, width=18cm]{geometry}
```

 is the same as 

```
 \usepackage[textwidth=7in]{geometry}
```

Another example:

```
 \usepackage[lines=30, scale=0.8, text=7in]{geometry}
```

 results in 

```
[lines=30, textwidth=7in]
```

## Defaults\label{sec:defaults}

This section sums up the default settings for the auto-completion
described later.

The default vertical margin ratio is $2/3$, namely,
 \begin{equation}
  \emph{top} : \emph{bottom} = 2 : 3 \qquad\emph{default}
 \end{equation}
 As for the horizontal margin ratio, the default value depends on
 whether the document is onesided or twosided,
 \begin{equation}
  \emph{left}\;(\textrm{inner}) : \emph{right}\;(\textrm{outer}) 
       = \left\{ \begin{array}{ll}
              1 : 1 \qquad \emph{default for oneside}\\
              2 : 3 \qquad \emph{default for twoside}
         \end{array}\right.
 \end{equation}
Obviously the default horizontal margin ratio for *oneside* is "centering".

The *geometry* package has the following default setting for
*onesided* documents:

 - `scale=0.7` (*body* is $0.7 \times \emph{paper}$)
 - `marginratio={1:1, 2:3}` (`1:1` for horizontal and `2:3` for vertical margins)
 - `ignoreall` (the header, footer, marginal notes are excluded when calculating the size of *body*.)
 
 For *twosided* document with `twoside` option, the default
 setting is the same as *onesided* except that the horizontal
 margin ratio is set to `2:3` as well.

 Additional options overwrite the previous specified dimensions. 


## Auto-completion \label{sec:rules}

 Figure \ref{fig:specrule} shows schematically how many specification
 patterns exist and how to solve the ambiguity of the
 specifications. Each axis shows the numbers of lengths
 explicitly specified for body and margins. `S(`$m$`,`$b$`)` presents the
 specification with a set of numbers $(\emph{margin},\emph{body})=(m,b)$.

 For example, the specification `width=14cm, left=3cm` is categorized
 into `S(1,1)`, which is an adequate specification. If you add
 `right=4cm`, it would be in `S(2,1)` and overspecified. 
 If only `width=14cm` is given, it's in `S(0,1)`, underspecified. 

 The *geometry* package has the auto-completion mechanism, in which
 if the layout parameters are underspecified or overspecified,
 *geometry* works out the ambiguity using the defaults and other
 relations. Here are the specifications and the completion rules.

 \begin{figure}
  {\unitlength=1pt
  \begin{picture}(400,150)(40,0)
  \put(1,49){\makebox(90,49)[r]{\large 0}}
  \put(1,1){\makebox(70,99)[r]{\large body}}
  \put(1,1){\makebox(90,49)[r]{\large 1}}
  \put(100,100){\makebox(99,20){\large 0}}
  \put(100,50){\framebox(99,49){}}
  \put(100,80){\makebox(99,15){\texttt{S(0,0)}}}
  \put(100,50){\makebox(99,49){use scale}}
  {\linethickness{1pt}%
  \put(150,35){\line(0,1){30}}
  \put(150,35){\line(-1,3){4}}
  \put(150,35){\line(1,3){4}}}
  \put(100,0){\framebox(99,49){}}
  \put(100,2){\makebox(99,15){\texttt{S(0,1)}}}
  \put(100,0){\makebox(99,49){use marginratio}}
  \put(200,120){\makebox(99,12){\large margin}}
  \put(200,100){\makebox(99,20){\large 1}}
  \put(200,50){\framebox(99,49){use scale}}
  \put(200,55){\makebox(89,10)[r]{\scriptsize\shortstack[l]{if ratio\\specified}}}
  \put(200,2){\makebox(99,15){\texttt{S(1,1)}}}
  {\linethickness{1pt}%
  \put(250,35){\line(0,1){30}}
  \put(250,35){\line(-1,3){4}}
  \put(250,35){\line(1,3){4}}}
  {\linethickness{1pt}%
  \put(225,25){\line(-1,0){35}}
  \put(225,25){\line(-3,-1){12}}
  \put(225,25){\line(-3,1){12}}}
  \put(200,80){\makebox(99,15){\texttt{S(1,0)}}}
  \put(200,0){\framebox(99,49){\textcolor{red}{solvable}}}
  \put(300,100){\makebox(99,20){\large 2}}
  \put(300,80){\makebox(99,15){\texttt{S(2,0)}}}
  \put(300,50){\framebox(99,49){\textcolor{red}{solvable}}}
  \put(300,0){\framebox(99,49){forget body}}
  \put(300,2){\makebox(99,15){\texttt{S(2,1)}}}
  {\linethickness{1pt}%
  \multiput(290,65)(5,0){6}{\line(1,0){3}}
  \put(320,65){\line(-3,-1){12}}
  \put(320,65){\line(-3,1){12}}}
  {\linethickness{1pt}%
  \put(350,65){\line(0,-1){30}}
  \put(350,65){\line(-1,-3){4}}
  \put(350,65){\line(1,-3){4}}}
  \end{picture}}
  \caption{
  Specifications \texttt{S(0,0)} to \texttt{S(2,1)} and the completion rules
  (arrows). Column and row numbers denote the number of explicitly
  specified lengths for margin and body respectively. \texttt{S(}$m$,$b$\texttt{)} denote a
  specification with a set of the numbers $(\emph{margin},\emph{body})=(m,b)$. 
  }
  \label{fig:specrule}
 \end{figure}

- `S(0,0)`
    Nothing is specified. The *geometry* package sets *body* with the
    default `scale` ($=0.7$). 

    For example, `width` is set to be
    $0.7\times \emph{layoutwidth}$. Note that by default *layoutwidth* 
    and *layoutheight* will be equal to `\paperwidth` and `\paperheight`
    respectively.
    
    Thus `S(0,0)` goes to `S(0,1)`. See `S(0,1)`.

- `S(0,1)`
    Only *body* is specified, such as `width=7in`, `lines=20`,
    `body={20cm,` `24cm}`, `scale=0.9` and so forth.
    Then *geometry* sets margins with the margin ratio.
    If the margin ratio is not specified, the default is used.
    The default vertical margin ratio is defined as

    \begin{equation}
     \emph{top} : \emph{bottom} = 2 : 3 \qquad \emph{default}
    \end{equation}

    As for the horizontal margin ratio, the default value depends on
    whether the document is onesided or twosided,
   
    \begin{equation}
     \emph{left}(\textrm{inner}) : \emph{right}(\textrm{outer}) 
          = \left\{ \begin{array}{ll}
                 1 : 1 \qquad \emph{default for oneside}\\
                 2 : 3 \qquad \emph{default for twoside}
            \end{array}\right. 
    \end{equation}
   
   
    For example, if `height=22cm` is specified on A4 paper, 
    *geometry* calculates `top` margin as follows:
    \begin{equation}
      \begin{array}{ll}
      \emph{top} &= ( \emph{layoutheight} - \emph{height} ) \times 2/5 \\
            &= (29.7-22)\times 2/5 = 3.08\textrm{(cm)}
      \end{array}
    \end{equation}
   
   Thus `top` margin and body `height` have been determined, the
    specification for the vertical goes to `S(1,1)` and
    all the parameters can be solved.

 - `S(1,0)`
   Only one margin is specified, such as `bottom=2cm`, `left=1in`,
   `top=3cm`, and so forth.

 
 - If the margin ratio is *not specified*, *geometry* sets
   *body* with the default `scale` ($=0.7$). 
   For example, if `top=2.4cm` is specified, *geometry* sets
    
   ```
   height= 0.7\layoutheight
         (=0.7\paperheight by default)
   ```
   
   then `S(1,0)` goes to `S(1,1)`, in which *bottom* is calculated
   with $\emph{layoutheight}-(\emph{height}+\emph{top})$ and results in $6.51$cm on A4
   paper if the layout size is equal to the paper size.

- If the margin ratio is specified, such as
  `hmarginratio={1:2}`, `vratio={3:4}` and so forth,
  *geometry* sets the other margin with the specified margin ratio.
  For example, if a set of options `top=2.4cm,vratio={3:4}` is
  specified, *geometry* sets `bottom` to be `3.2cm` calculating
 
  \begin{center}
      $\emph{bottom}= \emph{top}/3\times4 = 3.2\textrm{cm}$
  \end{center}
  Thus `S(1,0)` goes to `S(2,0)`.
  
 
  Note that the version 4 or earlier used to set the other margin
  with the margin ratio. In the version 5, therefore, with the
  same specification, the result will be different from the one in the
  version 4. For example, if only `top=2.4cm` is specified, 
  you got `bottom=2.4cm` in the version 4 or earlier, but you will get
  `bottom=6.51cm` in the version 5.

 - `S(2,1)`
   The *body* and two *margins* are all specified, such as
   `vdivide={1in,8in,1.5in}`, `left=3cm,width=13cm,right=4cm` and
   so forth. Since *geometry* basically gives priority to *margins*
   if dimensions are overspecified, *geometry* forgets and resets
   *body*. For example, if you specify
 
   ```
    \usepackage[a4paper,left=3cm,width=13cm,right=4cm]{geometry}
   ```
  
   *width* is reset to be 14cm because the width of a A4 paper is 21cm long.

# Changing layout mid-document\label{sec:midchange}

The version 5 provides the new commands `\newgeometry{`$\cdots$`}`
and `\restoregeometry`, which allow you to change page dimensions
in the middle of the document. Unlike *geometry* in the preamble,
`\newgeometry` is available only after `\begin{document}`,
resets all the options ever specified except for the
papersize-related options: *landscape*, *portrait*, and paper size
options (such as `papersize`, `paper=a4paper` and so forth), which
can't be changed with `\newgeometry`. 

The command `\restoregeometry` restores the page layout specified
in the preamble (before `\begin{document}`) with the options to
`\usepackage{geometry}` and `\geometry`.

Note that both `\newgeometry` and `\restoregeometry` insert
`\clearpage` where they are called.

\pagebreak

Below is an example of changing layout mid-document. The layout L1
specified with hmargin=3cm *(*left and *right* margins are 3cm
long) is changed to L2 with `left=3cm`, `right=1cm` and
`bottom=0.1cm`. The layout L1 is restored with
`restoregeometry`. 

\verb$\usepackage[hmargin=3cm]{geometry\}$

\verb$\begin{document}$

 \hspace{1cm}\fbox{Layout L1}

\verb$\newgeometry{left=3cm,right=1cm,bottom=0.1cm}$

 \hspace{1cm}\fbox{Layout L2 (new)}

\verb$\restoregeometry$

 \hspace{1cm}\fbox{Layout L1 (restored)}

\verb$\newgeometry{margin=1cm,includefoot}$

 \hspace{1cm}\fbox{Layout L3 (new)}

\verb$\end{document}$

\begin{figure}[H]
\small
{\unitlength=.78pt
\begin{picture}(450,180)(0,0)
\put(0,165){\makebox(95,12){(saved)}}
\put(15,135){\framebox(65,10){head}}
\put(15,60){\framebox(65,70){body}}
\put(15,45){\makebox(65,12){foot}}
\put(15,45){\line(1,0){65}}
\put(0,20){\framebox(95,140){}}
\put(0,0){\makebox(95,20){L1}}
\put(104,90){\circle*{4}}
\put(110,90){\circle*{4}}
\put(116,90){\circle*{4}}
\put(125,165){\makebox(95,12){\texttt{\textbackslash newgeometry}}}
\put(140,135){\framebox(71,10){head}}
\put(140,33){\framebox(71,97){body}}
\put(140,21){\makebox(71,12){foot}}
\put(125,20){\framebox(95,140){}}
\put(125,0){\makebox(95,20){L2 (new)}}
\put(229,90){\circle*{4}}
\put(235,90){\circle*{4}}
\put(241,90){\circle*{4}}
\put(250,165){\makebox(95,12){\texttt{\textbackslash restoregeometry}}}
\put(265,135){\framebox(65,10){head}}
\put(265,60){\framebox(65,70){body}}
\put(265,45){\makebox(65,12){foot}}
\put(265,45){\line(1,0){65}}
\put(250,20){\framebox(95,140){}}
\put(250,0){\makebox(95,20){L1 (restored)}}
\put(354,90){\circle*{4}}
\put(360,90){\circle*{4}}
\put(366,90){\circle*{4}}
\put(375,165){\makebox(95,12){\texttt{\textbackslash newgeometry}}}
\put(383,41){\framebox(80,111){body}}
\put(383,29){\makebox(80,12){foot}}
\put(383,29){\line(1,0){80}}
\put(375,20){\framebox(95,140){}}
\put(375,0){\makebox(95,20){L3 (new)}}
\end{picture}}
\end{figure}

\pagebreak

A set of commands `\savegeometry{`\meta{name}`}` and
`\loadgeometry{`\meta{name}`}` is handy if you want to
reuse more different layouts in your document.
For example, 
```
 \usepackage[hmargin=3cm]{geometry}
 \begin{document}
       L1
 \newgeometry{left=3cm,right=1cm,bottom=0.1cm}
 \savegeometry{L2}
       L2 (new, saved)
 \restoregeometry
       L1 (restored)
 \newgeometry{margin=1cm,includefoot}
       L3 (new)
 \loadgeometry{L2}
       L2 (loaded)
 \end{document}
```

# Examples

 
1. A onesided page layout with the text area centered in the paper.
   The examples below have the same result because the horizontal margin ratio
   is set `1:1` for oneside by default.

   - `centering`
   - `marginratio=1:1`
   - `vcentering`


2. A twosided page layout with the inside offset for binding set to `1cm`.
 
    - `twoside, bindingoffset=1cm`
 
   In this case, `textwidth` is shorter than that of the default twosided
   document by $0.7\times 1$cm ($=0.7$cm) because the default width of
   *body* is set with `scale=0.7`, which means 

   ``` 
    width=0.7\layoutwidth
    (=0.7\paperwidth by default)
   ```

3. A layout with the left, right, and top margin `3cm`, `2cm` and
   `2.5in` respectively, with textheight of 40 lines, and with the head and
   foot of the page included in *total body*.
   The two examples below have the same result.
 
   - `left=3cm, right=2cm, lines=40, top=2.5in, includeheadfoot`
   - `hmargin={3cm,2cm}, tmargin=2.5in, lines=40, includeheadfoot`
 

4. A layout with the height of *total body* `10in`, the bottom
   margin `2cm`, and the default width. The top margin will be calculated
   automatically. Each solution below results in the same page layout.
 
   - `vdivide={*, 10in, 2cm}`
   - `bmargin=2cm, height=10in`
   - `bottom=2cm, textheight=10in` 
 
   Note that dimensions for *head* and *foot* are excluded from
   *height* of *total body*. An additional *includefoot* makes
   *footskip* included in *totalheight*. Therefore, in the two cases below,
   *textheight* in the former layout is shorter than the latter
   (with 10in exactly) by *footskip*. In other words, 
   *height* $=$ *textheight* $+$ *footskip* when *includefoot* $=$ *true* in this case.
 
   - `bmargin=2cm, height=10in, includefoot`
   - `bottom=2cm, textheight=10in, includefoot`
 
5. A layout with `textwidth` and `textheight` 90\% of the
   paper and with *body* centered.
   Each solution below results in the same page layout as long as
   *layoutwidth* and *layoutheight* are not modified from the default.

   - `scale=0.9, centering`
   - `text={.9\paperwidth,.9\paperheight}, ratio=1:1`
   - `width=.9\paperwidth, vmargin=.05\paperheight, marginratio=1:1`
   - `hdivide={*,0.9\paperwidth,*}, vdivide={*,0.9\paperheight,*}`
     (as for onesided documents)
   - `margin={0.05\paperwidth,0.05\paperheight}`

   You can add `heightrounded` to avoid an "underfull vbox warning" like

   ```
    Underfull \vbox (badness 10000) has occurred 
    while \output is active.
   ```

   See Section \ref{sec:body} for the detailed description about *heightrounded*.

\pagebreak

6. A layout with the width of marginal notes set to 3cm and included
   in the width of *total body*. The following examples are the same.

   - `marginparwidth=3cm, includemp`
   - `marginpar=3cm, ignoremp=false`


7. A layout where *body* occupies the whole paper with A5 paper in
   landscape. The following examples are the same.

   - `a5paper, landscape, scale=1.0`
   - `landscape=TRUE, paper=a5paper, margin=0pt`


8. A screen size layout appropriate for presentation with PC and video
   projector.
   ```
    \documentclass{slide}
    \usepackage[screen,margin=0.8in]{geometry}
    ...
    \begin{slide}
    ...
    \end{slide}
   ```
9. A layout with fonts and spaces both enlarged from A4 to A3.
   In the case below, the resulting paper size is A3:
 
   - `a4paper, mag=1414`
 
   If you want to have a layout with two times bigger fonts, but without
   changing paper size, you can type:
 
   - `letterpaper, mag=2000, truedimen`
 
   You can add *dvips* option, that is useful to preview it with proper
   paper size by *dviout* or *xdvi*.

\pagebreak

10. Changing the layout of the first page and leaving the others
    as default before loading *geometry*. Use *pass* option, `\newgeometry`
    and `\restoregeometry`.

    ```
     \documentclass{book}
     \usepackage[pass]{geometry}
       % 'pass' disregards the package layout,
       %  so the original 'book' layout is memorized here.
     \begin{document}
     \newgeometry{margin=1cm}% changes the first page dimensions.
       Page 1
     \restoregeometry % restores the original 'book' layout.
       Page 2 and more
     \end{document}
    ```

10. A complex page layout.

    ```
     \usepackage[
      a5paper, landscape, twocolumn, twoside,
      left=2cm, hmarginratio=2:1, includemp, marginparwidth=43pt, 
      bottom=1cm, foot=.7cm, includefoot, textheight=11cm, 
      heightrounded, columnsep=1cm, dvips, verbose]{geometry}
    ```

