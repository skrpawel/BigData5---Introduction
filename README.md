# BigData5 - Introduction

# Zadanie 1  

### 1. Przygotuj mały plik tekstowy do policzenia słów.  

### 2. Wykonaj następujący skrypt:  
-- odczytaj plik linijka po linijce  
-- kazda linijke wczytujesz jako rekord o nazwie linijka  
```
plik = load '/user/cloudera/plik_avg1.txt' as (linijka);
```

-- podziel kazda linijke na tokeny - kazdy znich teraz jest rekordem o nazwie wyraz
```
wyrazy = foreach plik generate flatten(TOKENIZE(linijka)) as wyraz; 
```

-- pogrupuj razem wyrazy po poszczegolnym wyrazie  grupa = group wyrazy by wyraz;  
-- policz wyrazy  
```
policz = foreach grupa generate group, COUNT(wyrazy);  
```

-- wykonaj zadanie na platformie Hadoop i wypisz rezultaty  dump policz;  

### 3. Zmień plik na jeden z większych oraz przeprowadź zapis do pliku zastępując polecenie DUMP … poleceniem 
```
STORE policz INTO '/user/cloudera/wynik_pig_licznik';     
```

# Zadanie 2

Możesz korzystać z pomocy na stronie: [Apache](https://pig.apache.org/docs/r0.15.0/index.html)

### 1. Skopiuj do HDFS plik o nazwie movies_data.csv.

### 2. Wczytaj plik i wypisz na standardowe urządzenia wyjścia.

### 3. Zmodyfikuj wczytywanie pliku dodając klauzulę:
```
USING PigStorage(',') as (identyfikator,tytul,rok,ocena,czas_trwania)
```

Dzięki niej będziesz mógł odwoływać się do odpowiednich kolumn w pliku.

Uwaga: Funkcja PigStorage przetwarza pliki tekstowe – chcąc operować później na kolumnach numerycznych, będziesz musiał przeprowadzić rzutowanie.

### 4. Wybierz filmy tylko z roku 1949 i zapisz do pliku.

Podpowiedzi:

Przeprowadź rzutowanie roku na typ float.
Użyj funkcji FILTER … BY …
Operator porównania to ==.
### 5. Przeprowadź ponowne filtrowanie wybierając filmy z lat 1949 – 1961.

Podpowiedź: 
```
FILTER … BY … AND …  
```
### 6. Zapisz do pliku rezultatów tylko kolumny z tytułem i czasem trwania w minutach (w pliku wejściowym czas jest podany w sekundach).

Podpowiedź: FOREACH … GENERATE …

7. Uporządkuj filmy malejąco po roku.

Podpowiedź: 
```
ORDER … BY …
```

# Zadanie 3

Korzystając z jednego z wcześniej wykonanych zadań oraz interpretera GRUNT, sprawdź działanie poleceń Pig:
```
1. DESCRIBE,
2. EXPLAIN,
3. LIMIT … DUMP.
```

# Zadanie 4

Przetestuj na wybranych zbiorach operatory złączenia:
```
1. JOIN,
2. UNION.
```

# Zadanie 5

Przetestuj na wybranych zbiorach operatory grupowania:

```
1. GROUP,
2. COGROUP.
```

#Zadanie 6

Przetestuj na wybranym zbiorze numerycznym funkcje agregujące:
```
1. COUNT_STAR,
2. COUNT,
3. MIN,
4. MAX,
5. SUM,
6. AVG.
```


# Zadanie 7

Na podstawie składni języka Pig Latin sprawdź, czy wiesz:

1. Czy za pomocą operatów złączenia można połączyć więcej niż dwa zbiory?

2. Czy za pomocą operatora SPLIT można podzielić zbiór na więcej niż dwa podzbiory?

3. Jak powinien być zbudowany plik wejściowy, żeby przynajmniej jeden z jego elementów można było wczytać jako:
4. a) krotka/tuple składającą się z elementów atomowych? 
5. zbiór/bag składający się z krotek?

