---
layout: left-menu
title: Commands
tagline: user documentation for KIX-CC using GitHub Pages
description: KIX-CC Commands
order: 100
category: KIX-CC
---

Any single command or stack of commands is specified in the command line panel and executed by pressing either the \rightclick{Ctrl} and \rightclick{Enter} keys together or the "green arrow" button in the upper left corner of that panel.
Please note that the plug-in is not developed to check the sensibility of your computations. To yield sensible results the chain-linked indices to be aggregated or disaggregated have to have the same reference period. In this sense, the reference period is defined as the period for which the series is based to an average of 100.

Each command described in this section is essentially a sequence of mandatory and optional arguments. To distinguish the two types of arguments, the latter are displayed in brackets. Comments can be added as entire lines by using the **#** symbol as the first character in the respective lines. However, please note that comments cannot be added after commands.

## Chain linking: the 'CLI.CC' command

The 'CLI.CC' command is used to aggregate and/or disaggregate two or more continuously chained indices. To this end, the following steps are carried out under the assumption that all continuously chained indices involved in the calculation have the same base and reference periods:

1. Each index is unchained.
2. A weighted sum/difference of the unchained time series is calculated, where the weight of each unchained series in period $t$ is given by the last value of the respective weighting series in period $t-1$. If a weighting series does not cover the period $t = 0$, then its last value in this period is approximated by the last value in period $t = 1$. However, the user can decide whether or not (default) the values of the continuously chained aggregate are displayed for period $t = 1$, see section \ref{sec:opt} for further details.
3. The resulting series is chained: To obtain a time series showing the long term growth compared to the first observation, the aggregated growth factor are continuously multiplied. for the first period a starting value of 100 is set.
4. The aggregate is normalised to the desired reference period, so that the reference period equals 100.

The specification of the command is given by
\begin{center}
\tt [Name=]CLI.CC,index1,[weight1,]+/-,index2,[weight2,]...,refperiod
\end{center}
with the following arguments:
\begin{tabular_new}
{\tt Name} & Name of the continuously chained aggregate to be displayed in the \window{Results} panel. If not specified, it is set to {\it Formula} $n$, where $n$ is the line of the command in the command line panel of the \window{MyKIX} document. \\
{\tt index1} & First index from the \window{Index Data} panel to be used in the aggregation/disaggregation. \\
{\tt weight1} & Weighting series from the \window{Weight Data} panel which corresponds to the first index ({\tt index1}). If not specified, the weighting series with the same running number as the first index is taken automatically. \\
{\tt +/-} & Operator used to indicate aggregation (+) or disaggregation (-). All operations are executed ``from left to right''. \\
{\tt index2} & Second index from the \window{Index Data} panel to be used in the aggregation/disaggregation. \\
{\tt weight2} & Weighting series from the \window{Weight Data} panel which corresponds to the second index ({\tt index2}). If not specified, the weighting series with the same running number as the second index is taken automatically. \\
{\tt ...} & Additional indices, corresponding weighting series and operators to be included in the aggregation/disaggregation. \\
{\tt refperiod} & Depend on the period unit (monthly, quarterly, semi-annual or annual) the user has to choice the correct reference period of the continuously chained index (for example: the notation $IV-2012$ means the April of $2012$ for monthly time series, for quarterly time series it means the fourth quarter of $2012$).
\end{tabular_new}

\begin{exam}[{\tt CLI.CC} command]
Suppose we have loaded five quarterly indices and seven quarterly weighting series to the \window{Index Data} and \window{Weight Data} panels, respectively, and the command line panel reads:
\begin{verbatim}
    CLI.CC,i1,+,i2,IV-2012
    CLI.CC,i5,w5,-,i4,w4,IV-2012
    MyCLi1=CLI.CC,i1,w6,+,i2,w7,-,i4,w4,I-2015
\end{verbatim}
Executing these commands, the \window{Results} panel will display three continuously chained indices:
(1) a continuously chained aggregate of the index series $i1$ and $i2$, where $w1$ and $w2$ are used as respective weighting series from the \window{Weight Data} panel and with reference period fourth quarter of 2012, with the name Formula $1$,
(2) a disaggregated continuously chained index with the name Formula $2$ derived by subtracting the continuously chained index $i4$ from the continuously chained aggregate $i5$, using the weighting series $w4$ for index series $i4$ and $w5$ for the aggregate $i5$ and with reference period fourth quarter of 2012,
(3) a continuously chained aggregate with the name Formula 3, where the index series $i1$ and $i2$ are aggregated with the aid of the weighting series $w6$ and $w7$, and subtracting the component index series i4 with using $w4$ as weighting series from the \window{Weight Data} panel, with reference period first quarter of 2015 and renamed by user's choice.
\end{exam}

\section{Contribution to growth: the {\tt CTG.CC} command}

The {\tt CTG.CC} command is used to compute the growth contribution of a continuously chained component to a continuously chained aggregate with the method of \cite{Rau:2017}. To this end, the following steps are carried out:
\begin{enumerate}
\item The continuously chained component and the continuously chained aggregate are unchained.
\item The growth contribution is calculated directly from the unchained component and aggregate according to formulas derived by \cite{Rau:2017}.
\end{enumerate}
The specification of the command is given by
\begin{center}
\tt [Name=]CTG.CC,iContr,[wContr,]iTotal,[wTotal,]lags
\end{center}
with the following arguments:
\begin{tabular_new}
{\tt Name} & Name of the growth contribution to be displayed in the \window{Results} panel. If not specified, it is set to {\it Formula} $n$, where $n$ is the line of the command in the command line panel of the \window{MyKIX} document. \\
{\tt iContr} & Continuously chained index from the \window{Index Data} panel, the growth contribution of which is to be computed. \\
{\tt wContr} & Weighting series from the \window{Weight Data} panel which corresponds to the chain-linked index ({\tt iContr}). If not specified, the weighting series with the same running number as the continuously chained index is taken automatically. \\
{\tt iTotal} & Continuously chained aggregate from the \window{Index Data} panel. \\
{\tt wTotal} & Weighting series from the \window{Weight Data} panel which corresponds to the continuously chained aggregate ({\tt iTotal}). If not specified, the weighting series with the same running number as the continuously chained aggregate is taken automatically. \\
{\tt lags} & Horizon of the growth contribution, which must be in the set depend on period unit (for example: $\{1, 3, 12\}$ for monthly data, $\{1, 2, 4\}$ for quarterly data. Using the notation $\{-1, -2\}$ the horizon is one respective two years.
\end{tabular_new}
Note that the {\tt CTG.CC} command always assumes an additive aggregation of the continuously chained components to the continuously chained aggregate.
\begin{exam}[{\tt CTG.CC} command]
Suppose we have loaded five quarterly continuously chained indices and seven quarterly weighting series to the \window{Index Data} and \window{Weight Data} panels, respectively, and the command line panel reads:
\begin{verbatim}
    CTG.CC,i1,i3,1
    CTG.CC,i3,w3,i5,w5,4
    MyUCi1=CTG.CC,i2,w7,i3,w3,1
\end{verbatim}
Executing these commands, the \window{Results} panel will display three growth contributions:
(1) the contribution of the continuously chained component $i1$ to the growth rate of the continuously chained aggregate $i3$, compared to the previous quarter and named Formula $1$, where $w1$ and $w3$ are used as respective weighting series from the \window{Weight Data} panel,
(2) the contribution of the continuously chained component $i3$ to the growth rate of the continuously chained aggregate $i5$, compared to the previous year (four periods) and named Formula $2$, where $w3$ and $w5$ are used as weighting series from the \window{Weight Data} panel,
(3) the contribution of the continuously chained component $i2$ to the growth rate of the continuously chained aggregate $i3$, compared to the previous quarter and named Formula $3$, where $w7$ and $w3$ are used as weighting series from the \window{Weight Data} panel and the result is renamed by user's choice.
\end{exam}