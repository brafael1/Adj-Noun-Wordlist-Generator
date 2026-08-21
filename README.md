# Adj Noun Wordlist Generator

Gerador de wordlists que combina adjetivos + substantivos + dígitos com suporte a leet speak e variações mistas.

## Compilar

**Linux:**
```bash
g++ adj.cpp -oadj -std=c++11
```

**Windows:**
```bash
cl /EHsc adj.cpp
```

## Parâmetros

### Controle de dígitos
| Param | Descrição | Exemplo |
|-------|-----------|---------|
| `-0` | só adj+sub | `fluffydog` |
| `-1` | +1 dígito | `fluffydog0` |
| `-2` | +2 dígitos | `fluffydog00` |
| `-3` | +3 dígitos | `fluffydog000` |

### Palavras customizadas
| Param | Descrição | Exemplo |
|-------|-----------|---------|
| `-a palavra` | define a palavra 1 | `-a fluffy` |
| `-s palavra` | define a palavra 2 | `-s dog` |

### Modificadores
| Param | Descrição | Exemplo |
|-------|-----------|---------|
| `-at` | adiciona `@` entre elas | `fluffy@dog` |
| `-leet` | leet speak completo | `flu77yd09` |
| `-mix` | variações mistas (leet + maiúsculas) | `Flu77yDo9` |
| `-full` | usa lista completa (968 adj + 1844 nouns) | todas as combinações |

### Separador personalizado

O separador padrão é `@`. Para mudar, edite a **linha 85** do `adj.cpp`:

```cpp
std::string sep = use_at ? "@" : "";
```

Altere `"@"` para o caractere que preferir, como `"#"`, `"-"`, `"_"`, etc.

### Salvar em .txt
```bash
./adj -a fluffy -s dog -0 -at -leet -mix > wordlist.txt
```

## Exemplos de uso

### Combinar palavras customizadas
```bash
./adj -a fluffy -s dog -0 -at -leet -mix
```
Resultado:
```
fluffy@dog
flu77yd09
Flu77yDo9
flu77y@D0g
...
```

### Com 3 dígitos
```bash
./adj -a fluffy -s dog -3 -at -leet -mix > wordlist.txt
```

### Usar listas internas
```bash
./adj -0 -at -leet
```

### Lista completa
```bash
./adj -0 -full -at -leet > wordlist_full.txt
```

## Tabela leet speak

| Caractere | Número |
|-----------|--------|
| a | 4 |
| e | 3 |
| i | 1 |
| o | 0 |
| s | 5 |
| t | 7 |
| g | 9 |
| b | 8 |

## Uso com ferramentas

```bash
# hashcat
./adj -a fluffy -s dog -0 -at -leet -mix | hashcat -m 2500 CAP.hccap

# aircrack-ng
./adj -a fluffy -s dog -0 -at -leet -mix | aircrack-ng -w - CAP.cap -e SSID

# pyrit
./adj -a fluffy -s dog -0 -at -leet -mix | pyrit -r CAP.cap -i- attack_passthrough
```

## Exemplos de variações geradas

### Com `-0` (sem dígitos)
```bash
./adj -a fluffy -s dog -0 -at -mix
```
| Tipo | Exemplo |
|------|---------|
| Original | `fluffy@dog` |
| Leet | `flu77yd09` |
| Mix | `Flu77yDo9` |
| Invertido | `dog@fluffy` |

### Com `-1` (+1 dígito)
```bash
./adj -a fluffy -s dog -1 -at -mix
```
| Tipo | Exemplo |
|------|---------|
| Original | `fluffy@dog0` |
| Leet | `flu77yd090` |
| Mix | `Flu77yDo90` |

### Com `-3` (+3 dígitos)
```bash
./adj -a fluffy -s dog -3 -at -mix
```
| Tipo | Exemplo |
|------|---------|
| Original | `fluffy@dog000` |
| Leet | `flu77yd09000` |
| Mix | `Flu77yDo9000` |
