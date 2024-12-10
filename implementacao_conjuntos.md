## Implementação de estruturas e predicados para operação com conjuntos em Prolog.

### L3 resulta da união de L1 com L2.
```prolog
    union([], L2, L2).
    union([X|L1], L2, [X|L3]) :-
        \+ member(X, L2),  % X nao esta em L2
        union(L1, L2, L3).  % Continua unindo o restante de L1 e L2
    union([X|L1], L2, L3) :-
        member(X, L2),  % X esta em L2
        union(L1, L2, L3).  % Ignora X e continua
```

### L3 resulta da intersecção de L1 com L2.
```prolog
    intersection([], _, []).
    intersection([X | L1], L2, [X | L3]) :-
        member(X, L2),  % X esta em L2
        intersection(L1, L2, L3).  % Continua lendo o restante de L1 e L2
    intersection([_ | L1], L2, L3) :-
        \+ member(X, L2),  % X nao esta em L2
        intersection(L1, L2, L3).  % Ignora X e continua
```

### L3 resulta da diferença de L1 com L2.
```prolog
    diference([], _, []).
    diference([X | L1], L2, L3) :-
        member(X, L2),  % X esta em L2
        diference(L1, L2, L3).  % Ignora X e continua
    diference([X | L1], L2, [X | L3]) :-
        \+ member(X, L2),  % X nao esta em L2
        diference(L1, L2, L3).  % Continua lendo o restante de L1 e L2
```

### L1 é um subconjunto de L2.
```prolog
    subset([], _).
    subset([X|L1], L2) :-
        member(X, L2),  % Verifica se X está em L2
        subset(L1, L2).  % Continue verificando o restante
```

### L1 é um conjunto equivalente a L2.
<mark>Obs: Essa questão reaproveita o predicado de "subset" da questão anterior.</mark> 
```prolog
    equivalence(L1, L2) :-
        subset(L1, L2),
        subset(L2, L1).
```
