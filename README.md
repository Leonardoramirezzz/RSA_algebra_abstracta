# algebra abstracta - RSA

**Integrantes**

| Leonardo Alonso Ramirez Quiroz |
| Diego Enrique Zegarra Zenteno |
| Rodrigo del Piero Melendez Flores |


<br>

### 1:
*Implementar RSA_KEY_GENERATOR.*

Utilizamos algoritmos implementados en anteriores sesiones como: Inversa de un número, Euclides extendido, exponenciación modular y miller rabin.

El algoritmo del RSA recibe un int k, long long e y long long d.

Empieza generando dos números primos (p y q) al azar y asegurándose que sean distintos.

Calcula n como el producto de p y q, y phi de n.

Hallamos Generar aleatoriamente e ∈ [2, n − 1], tal que gcd(e, φ(n)) = 1 (con euclides de (e,φ(n)).

Hallamos d, que es el inverso de (e, φ(n)).

```c++
unsigned long long RSA_KEY_GENERATOR(int k, unsigned long long& e, unsigned long long& d) {
    unsigned long long p = RANDOMGEN_PRIMOS(k / 2);
    unsigned long long q = RANDOMGEN_PRIMOS(k / 2);
    while (p == q) q = RANDOMGEN_PRIMOS(k / 2);

    unsigned long long n = p * q;
    unsigned long long φn = (p - 1) * (q - 1);
    int x, y;
    
    e = 2 + rand() % φn - 1;
    while (EuclidesExtendido(e, φn, x, y) != 1) e = 2 + rand() % φn - 1;
    d = inverso(e, φn);
    return n;
}

unsigned long long cifrar(unsigned long long m, unsigned long long e, unsigned long long n) {
    unsigned long long c = EXPMOD(m, e, n);
    return c;
}

unsigned long long descifrar(unsigned long long c, unsigned long long d, unsigned long long n) {
    unsigned long long m = EXPMOD(c, d, n);
    return m;
}
```

### 2:
*Crear un sistema RSA-64 y mostrar los valores para e, d y n.

Generar una tabla con tres columnas m, c = P(m) y m' = S(c). Para las filas usar 10 valores números aleatorios distintos para m.*


```python
def randomPrimeNumber():
    source = [ 
        16, 16, 16, 16, 16, 16, 16, 16, 16, 16,
        32, 32, 32, 32, 32, 32, 32, 32, 32, 32,
        64, 64, 64, 64, 64, 64, 64, 64, 64, 64
    ]

    for i in source:
        prime = RANDOMGEN_PRIMOS(i)
        print("{0}bits -> {1}".format(i, prime))
```
```bash
randomPrimeNumber:

16bits -> 33647
16bits -> 39499
16bits -> 59333
16bits -> 35797
16bits -> 46439
16bits -> 37633
16bits -> 47563
16bits -> 54709
16bits -> 36919
16bits -> 55171
32bits -> 2479449331
32bits -> 3943072037
32bits -> 3392485429
32bits -> 2668402537
32bits -> 4221862063
32bits -> 3054322699
32bits -> 3263909771
32bits -> 4293211151
32bits -> 3885413933
32bits -> 2329364221
64bits -> 12702557818905538561
64bits -> 17605323725312372737
64bits -> 9319588526910369793
64bits -> 11188507237998315521
64bits -> 13344054781187880961
64bits -> 10122845002879154177
64bits -> 13921347531788193793
64bits -> 12495984492930224129
64bits -> 13523977963399149569
64bits -> 9622235937478082561
```
