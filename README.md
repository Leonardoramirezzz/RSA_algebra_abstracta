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
    //genera primos aleatorios
    unsigned long long p = RANDOMGEN_PRIMOS(k / 2);
    unsigned long long q = RANDOMGEN_PRIMOS(k / 2);
    //por si son iguales se vuelve a generar q
    while (p == q) {
        q = RANDOMGEN_PRIMOS(k / 2);
    }
    //se calcula n 
    unsigned long long n = p * q;
    //calculamos  φ(n)= φ(p)*φ(q)=(p-1)*(q-1)
    unsigned long long φn = (p - 1) * (q - 1);
    int x, y;
    //hallamos Generar aleatoriamente e ∈ [2, n − 1], tal que gcd(e, φ(n)) = 1 (con euclides de (e,φn)
    e = 2 + rand() % φn - 1;
    while (EuclidesExtendido(e, φn, x, y) != 1) {
        e = 2 + rand() % φn - 1;
    }
    //hallamos d q es el inverso de (e, φn)
    d = inverso(e, φn);
    return n;

}
```
```bash
Numeros primos de 3 digitos:
101--103--107--109--113--127--131--137--139--149--151--157--163--167--173--179--181--191--193--197--199--211--223--227--229--233--239--241--251--257--263--269--271--277--281--283--293--307--311--313--317--331--337--347--349--353--359--367--373--379--383--389--397--401--409--419--421--431--...--997
Numeros primos de 4 digitos:
1009--1013--1019--1021--1031--1033--1039--1049--1051--1061--1063--1069--1087--1091--1093--1097--1103--1109--1117--1123--1129--1151--1153--1163--1171--1181--1187--1193--1201--1213--1217--1223--1229--1231--1237--1249--1259--1277--1279--1283--1289--1291--1297--1301--1303--1307--1319--1321--...--9973
Numeros primos de 5 digitos:
10007--10009--10037--10039--10061--10067--10069--10079--10091--10093--10099--10103--10111--10133--10139--10141--10151--10159--10163--10169--10177--10181--10193--10211--10223--10243--10247--10253--10259--10267--10271--10273--10289--10301--10303--10313--10321--10331--10333--10337--10343--...--99991
```

### Ejercicio 2
*Implementar un programa que genere de manera aleatoria al menos 10 primos distintos de 16, 32 y 64 bits.*

any content here

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
