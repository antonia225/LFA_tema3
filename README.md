Structura 

1. Configurarea Gramaticii libere de context (GLC)
2. Generarea Aleatorie de Șiruri
3. Afișarea Derivării
4. Verificarea Aparținerii

1. Configurarea GLC 
Definirea componentelor gramaticii în Python:

  V = {'S'}                   # Mulțimea simbolurilor neterminale
  E = {'a', 'b'}              # Mulțimea simbolurilor terminale
  R = {
      'S': ['aSb', '']        # Regulile de producție ('' înseamnă e)
  }
  S = 'S'                     # Simbolul de start

2. Generarea Aleatorie de Șiruri
Funcția `generate_string(max_strings=10, max_length=10)`:
  - `max_strings` : numărul maxim de șiruri distincte generate.
  - `max_length`  : lungimea maximă permisă pentru oricare șir.

Algoritmul:
  - Pornim de la neterminalul de start ("S") și expandăm recursiv  
    primul neterminal din stânga, aplicând toate producțiile sale (în ordine aleatorie).
  - Dacă șirul curent conține doar terminale ('a' și 'b') și nu depășește `max_length`,  
    îl adăugăm în setul de rezultate.
  - Oprim recursia când:
      • Am adăugat `max_strings` șiruri.
      • Orice expansiune generează un șir mai lung decât `max_length`.

3. Afișarea Derivării
Funcția `derivation(string)`:
  - Verifică dacă `string` conține doar caractere din `E` (dacă nu, raportează eroare).
  - Pentru șirul vid, afișează direct `S => e`.
  - Construiește recursiv o listă de pași de derivare, folosind:
      derive(k) = [ 'S', 'aSb', 'aaSbb', … ] până la numărul de pași `k = len(string)//2`.
  - Înlocuiește '' cu `e` pentru a arăta simbolul vid.

4. Verificarea Aparținerii
Funcția `verification(string)`:
  1. Dacă `string == ""`, returnează True (șir vid acceptat).
  2. Dacă lungimea șirului e impară → False.
  3. Dacă primul caracter e 'a' și ultimul e 'b', se apelează recursiv pe `string[1:-1]`.
  4. În orice alt caz → False.
Astfel, validăm corect limbajul { a^n b^n | n ≥ 0 }.

Exemplu de Rulare

Generated strings: {'', 'aaaabbbb', 'ab', 'aaabbb', 'aabb'}
Derivation of '': S => e
Derivation of 'aaaabbbb': S => aSb => aaSbb => aaaSbbb => aaaaSbbbb => aaaabbbb
Derivation of 'ab': S => aSb => ab
Derivation of 'aaabbb': S => aSb => aaSbb => aaaSbbb => aaabbb
Derivation of 'aabb': S => aSb => aaSbb => aabb
'': Yes
'aaaabbbb': Yes
'ab': Yes
'aaabbb': Yes
'aabb': Yes
'aab': No
'abb': No
'aacbb': No
'abab': No
'aaabb': No
'aaabbbb': No
