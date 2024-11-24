## Implementação de estruturas e predicados para formação e operação com listas em Prolog.

#### L é uma lista.
```prolog
    list([]).
    list([_ | _]).
```

#### X é um elemento da lista L.
```prolog
    member(X, [X | _]) :- !
    member(X, [_ | R]) :-
        member(X, R).
```

#### X não é um elemento da lista L.
```prolog
    not_member(_, []) :- !.
    not_member(X, [H | T]) :-
        X \= H, 
        not_member(X, T).
```

#### Prefix é um prefixo de List.
```prolog
    prefix([], _).
    prefix([H | T1], [H | T2]) :-
        prefix(T1, T2).
```

#### Sufix é um sufixo de List.
```prolog
    sufix(L, L).
    sufix(Lista, [_ | T]) :-
        sufix(Lista, T).
```

#### Sub é uma sublista de List.
```prolog
    sublist([], _).
    sublist([H | T], Lista) :-
        member(H, Lista), sublist(T, Lista).
```

#### List é o resultado da concatenação de L1 e L2.
```prolog
    append([], L, L).
    append([H | T1], L, [H | T2]) :-
        append(T1, L, T2).
```

#### Rev é o resultado de reverter List.
```prolog
    reverse([], []).
    reverse([H | T], Result) :-
        reverse(T, RevT), append(RevT, [H], Result).
```

#### X e Y são elementos adjacentes em List.
```prolog
    adjacent(X, Y, [X, Y | _]).
    adjacent(X, Y, [_ | R]) :-
            adjacent(X, Y, R).
```

#### N é o número de elementos de List.
```prolog
    tamain([], 0).
    tamain([_ | T], N) :-
        tamain(T, N1), N1 is N + 1.
```

#### X é o primeir elemento de List.
```prolog
    first([X | _], X).
```

#### X é o último elemento de List.
```prolog
    last([X], X) :- !.
    last([_ | T], X) :-
        last(T, X).
```

#### X é o N-ésimo elemento de List.
```prolog
    nth(X, 0, [X | _]).
    nth(X, N, [_ | T]) :-
        N > 0, N1 is N - 1, nth(X, N1, T).
```

#### Cada elemento de L aparece em LL em duplicado.
```prolog
    double([], []).
    double([H | T], [H, H | R]) :-
        double(T, R).
```

#### Sum é a soma dos elementos de Xs.
```prolog
    sum([], 0).
    sum([H | T], Ac) :-
        sum(T, X1), Ac is H + X1.
```

#### L2 resulta da elminação de todos os X de L1.
```prolog
    delete([], _, []).
    delete([X | T], X, L2) :-
        delete(T, X, L2).
    delete([H | T], X, [H | L2]) :-
        X \= H, delete(T, X, L2).
```

#### L2 resulta da elminação de um X de L1.
```prolog
    select(X, [X | T], T).
    select(X, [H | T], [H | R]) :- 
        X \= H, select(X, T, R).
```

#### L2 resulta da inserção de X em L1.
```prolog
    insert(X, L1, [X | L1]).
```

#### L2 é uma lista com todos os átomos de L1.
```prolog
    flatten([], []).
    flatten([H | T], [H | R]) :-
        atom(H),
        flatten(T, R).
    flatten([H | T], R) :-
        \+ atom(H),
        flatten(T, R).
```