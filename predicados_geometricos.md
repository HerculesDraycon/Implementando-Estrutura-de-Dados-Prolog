### Implementação de um conjunto de predicados em Prolog para representar pontos, retas e circunferências. Além disso, predicados para calcular a distância entre dois pontos e a área de uma circunferência.

### Definições de ponto, reta e circunferência.
```prolog
    point(X, Y).
    line(ponto1, ponto2).
    circle(Center, Radius).
```

### Distância entre dois pontos.
```prolog
    distance(ponto(X1, Y1), ponto(X2, Y2), D) :-
        Dx is X2 - X1,  % Diferença de coordenadas X
        Dy is Y2 - Y1,  % Diferença de coordenadas Y
        D is sqrt(Dx * Dx + Dy * Dy).  % Formula da distancia
```

### Calcula a área de uma circunferência.
<mark>Obs: Essa questão reaproveita o predicado de "distance" da questão anterior.</mark> 
```prolog
    area(ponto(Xc, Yc), ponto(Xp, Yp), Area) :-
        distance(ponto(Xc, Yc), ponto(Xp, Yp), Raio),  % Calcula o raio
        Area is pi * Raio * Raio.  % Calcula a área
```