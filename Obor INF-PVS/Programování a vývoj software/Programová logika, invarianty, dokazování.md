## Hoareova trojice
$$
\begin{gather}
\{x = 0\} \\
x = x + 1 \\
\{x = 1\}
\end{gather}
$$
- obecně $\{something\}$ je výrok o stavu programu a uprostřed je program *P*
- **prekondice** ... výrok o stavu programu před jeho začátkem $\{ϕ\}$
- **postkondice** ... výrok o stavu programu po jeho konci $\{ψ\}$

>[!info]
>**Pravdivost trojice** je dána tak, že program je ve stavu spňujícím $\{ \phi \}$, poté se program $P$ vykoná a výsledný stav splňuje $\{ \psi \}$.

#### (Axiom) přiřazení
$$
\begin{gather}
\{\phi(v/e)\} \\
v = e \\
\{\psi\}
\end{gather}
$$
- $v$ ... proměnná
- $e$ ... výraz
- $ϕ$ ... tvrzení
- $ϕ(v/e)$ ... nahrazení $v$ za $e$ ve $ϕ$
- **Např.**
$$ 
\begin{gather}
\{ x + 1 = 2 \} \\
x \leftarrow x + 1 \\
\{ x = 2 \}
\end{gather}
$$
	- *A to dále můžeme zjednodušit jako*
$$ 
\begin{gather}
\{ x = 1 \} \\
x \leftarrow x + 1 \\
\{ x = 2 \}
\end{gather}
$$
- Můžeme zesílit prekondici a oslabit postkondici
#### Nenarušení tvrzení
- $P$ ... akce
- $ϕ$ ... prekondice $P$
- $ψ$ ... tvrzení
- $ψ$ není narušeno (neinterferuje s) $P$ jestliže:
$$\begin{gather}
\{ψ∧ϕ\}\\
P\\
\{ψ\}
\end{gather}
$$
>[!info]
>Náčrtky důkazů se nemohou narušit pokud mají **disjunktní proměnné**.

- **invariant programu** ... tvrzení, které platí v každém stavu jeho historie (neboli platí na počátku a nikde v průběhu není narušeno)


