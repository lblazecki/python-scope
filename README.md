# python-scope
Objasniti sto je scope u programiranju i kako funkcionira u Pythonu te cemu sluzi global keyword


Scope je najjednostavnije objasniti pomocu primjera, pa krenimo.

### 1. zad  
```python
opseg = 12
print(opseg)
```

Ispisuje `12`. To smo i ocekivali, ajmo dalje.

### 2. zad
```python
def ispisi():
  opseg = 20
  print(opseg)
  return

ispisi()
```

Ispisuje `20`.  
Definiriali smo variajblu `noviOpseg` u funkciji `ispisi` te ispisali vrijednost.  
Sada nesto malo teze!

### 3. zad
```python
def ispisi():
  opseg = 20
  print(opseg)
  return

ispisi()
print(opseg)
```

Ispisuje  
`20`  
`NameError: name 'opseg' is not defined`  
Ocekivali smo da ce se ispisati `20` dva puta. Sto se dogodilo?  
`print(opseg)` unutar funkcije `ispisi` ispise varijablu `opseg`, ali   
`print(opseg)` izvan funkcije `ispisi` "ne vidi" varijablu `opseg` i baci error. Zasto?

Zato sto varijabla unutar funckije nije vidljiva izvan funkcije.  
Scope je doseg vidljivost varijable. U nasem slucaju doseg(scope) varijable `opseg` je unutar funkcije `ispisi`.

Kako rijesiti sljedeci problem. Tako da funkcija vrati vrijednost.

### 4. zad
```python
def ispisi():
  noviOpseg = 20
  print(noviOpseg)
  return noviOpseg

vraceniOpseg = ispisi()
print(vraceniOpseg)
```

Sada se ispisuje  
`20`  
`20`  
kako smo i ocekivali.

Sto kada iz funkcije pristupamo varijablama izvan funkcije. Hajd'mo vidjeti :)

### 5. zad
```python
opseg = 20

def ispisi():
  print(opseg)
  return

ispisi()
```

Ispisuje `20`.   
Kada ispisujemo unutar funkcije varijablu koja je definira vani nema problema :) Zasto?  
Zato sto je doseg varijable `opseg` kroz cijeli program i u svim funkcijama koje su definirane u programu.

Sada malo tezi dio!
Sto ce ispisati sljedeci komad koda?

### 6. zad
```python
opseg = 20

def ispisi():
  opseg = 30
  print(opseg)
  return

ispisi()
print(opseg)
```

Ispisuje:   
`30`  
`20`  

Kada bismo htjeli da ispisuje dva puta po 30 trebat cemo koristiti kljucnu rijec `global`.

### 7. zad
```python
opseg = 20

def ispisi():
  global opseg
  opseg = 30
  print(opseg)
  return

ispisi()
print(opseg)
```

Ispisuje:   
`30`  
`30`  

S kljucnom rijecju global omogucujemo koristenje varijabli koje nisu definirane u funkciji nego su definirane izvan nje. Ako ne definiramo kljucnu rijec global funkcija ce napraviti novu varijablu koja se isto zove i nju koristiti ne mjenjajuci varijablu koja se nalazi izvan funkcije.  
Ovo pravilo vrijedi kod mjenjanja varijabli.  
Kod ispisa ili pridruzivanja, funkcija prvo pokusa iskoristiti varijablu koja je definirana unutar funkcija, a ako ne postoji onda trazi izvan.

I jos jedno pravilo (koje proizlazi iz prijasnjih). Jedna funkcija ne moze citati varijable druge funkcije (osim ako nisu jedna unutar druge).  

Primjeri:

### 8. zad
```python
def prva():
  opseg = 30
  print(opseg)
  return

def druga():
  print(opseg)

prva()
druga()
```

Ispisuje:  
`30`  
`NameError: global name 'opseg' is not defined`

ALI:

### 9. zad
```python
def prva():
  opseg = 30
  print(opseg)

  def druga():
    print(opseg)
    return

  druga()
  return

prva()
```

Ispisuje:  
`30`    
`30`  
kao i 

### 10. zad
```python
opseg = 30

def prva():
  print(opseg)

  def druga():
    print(opseg)
    return

  druga()
  return

prva()
```

Scope je doseg/vidljivost varijabli. Postoji globalni (koja ima doseg cijelog programa) i lokalni (koja ima doseg unutar jedne funckije). U lokalnom scope se mogu vidjeti varijable u globalnom, ali obrnuto ne ide.  
Posebno za Python je da ako se iz lokalnog scope zeli promijeniti varijabla u globalnom, mora se koristiti kljucna rijec `global` da se definira da cemo mjenjati varijablu koja nije u trenutnom lokalnom scopeu.


