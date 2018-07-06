---
layout: left-menu
title: Introduction
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Introduction to KIX-CC
order: 0
category: KIX-CC
---

As opposed to fixed-base indices, aggregating chain-linked index series is anything but trivial. Yet, some of the most prominent macroeconomic indicators, such as national accounts or harmonised indices of consumer prices (HICP), are constructed as chain-linked Laspeyres indices. Furthermore, the currently developed 'indices of exchange rate effects in the international investment position (IIE)' are part of this index family.

The necessary computational work for chain-linked indices can be facilitated by use of programs of the KIX family. The abbreviation KIX of KettenIndeX is the German word for chain index. The software JDemetra+ (JD+) provides the implementation of KIX plug-ins.

The program KIX-CC offers chain-linking procedures for continuously chain-linked indices, like the IIE. That means the aggregation or disaggregation of two ore more chain-linked indices, as well as the calculation of growth contributions.

For all operations the plug-in requires the indices of interest and the corresponding weights. Indices and weights may be of any periodicity (e.g. monthly, quarterly or annual). The contribution of a subindex's growth to the overall growth can be calculated for the change to the previous periods (i.e. changes to previous month, quarter, half year or year). In contrast to to fixed-base indices the outcome of the growth contribution depends on the method used. The KIX-CC plug-in uses the formula of \cite{Arz/Rentzsch:2017} which was developed in accordance to the approach of \cite{Ribe:1999} for chain-linked price indices of one-period overlap type.

Currently, the software does not apply any tests concerning the usefulness or appropriateness of the investigated time series. In this sense, no test is implemented to check whether or not input series are chained or unchained. Furthermore, the software does not check the reference year of the input series. In the end, the user is solely responsible for the meaningfulness of any operation.

## Overview

The KIX-CC plug-in allows the user to carry out aggregation and disaggregation of continuously chained indices as well as calculation of their growth contributions in JD+. The following table provides an overview of the operations, commands, functions, and methods available for monthly and quarterly time series:


{: .table .table-bordered}
| Operation | Function | Command | Method |
| --------- | -------- | ------- | ------ |
| Chain-linking | Aggregation and disaggregation of continuously chained indices | *CLI.CC* | Arz 2018|
| Growth contribution | Calculation of growth contribution of a component series to an aggregate serie's growth rate | *CTG.CC* | Rentzsch 2018|

## Installation

Download the installation file from the plug-in's GitHub repository and save it to your local folder of choice. Choose
\begin{center}
text
\end{center}
from the JD+ drop down menu, open the **Downloaded** sheet and press the \rightclick{Add Plugins} button. Select the local copy of the installation file, click the \rightclick{Install} button and accept the terms in the licence agreements. Once the installation is finished, KIX documents and a global option menu are available. Note that the plug-in is automatically activated and, therefore, a restart of JD+ is not necessary.

The remainder of this manual is organised as follows:

  * \ref{sec:wind} describes the basic structure of the KIX document as well as data input and storage.
  * \ref{sec:kix} explains how the available computations can be carried out in the command line panel of the KIX document.
  * \ref{sec:opt} addresses the global options available for customising the plug-in according to the user's preferences.