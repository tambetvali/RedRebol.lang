# Implementing Laegna Numbers: Syntax, Semantics, and Dialect Design  
### A coherent article describing how Laegna numbers work, how syntax is defined, and how operations integrate into a dialect-native language (Red/Rebol)

Laegna numbers are symbolic–semantic numeric entities with structural meaning.  
They encode:
- **Type** (standard vs wave),
- **Sign** (uppercase = unsigned, lowercase = signed),
- **Base** (Laegna, binary, hex),
- **Digit sequence** (A, E, O, I),
- **Digit length R** (mathematically essential),
- **Octave** (structural property of R).

This article explains how to implement them in a dialect-native language such as Red or Rebol, how syntax is parsed, how operations behave, and how iteration works.

---

## 1. Laegna Number Syntax

Laegna numbers begin with a **prefix**, followed by **digits**.

### 1.1 Prefix structure

| Prefix | Meaning |
|-------|---------|
| **0L...** | Laegna standard, unsigned |
| **0l...** | Laegna standard, signed |
| **0W...** | Laegna wave, unsigned |
| **0w...** | Laegna wave, signed |
| **0Lb...** | Laegna standard binary |
| **0Lb...** | Laegna standard binary (unsigned) |
| **0Lx...** | Laegna standard hex |
| **0Wx...** | Laegna wave hex |
| **0Wb...** | Laegna wave binary |

Uppercase = **unsigned**, lowercase = **signed**.

Digits are drawn from the Laegna alphabet:
- **A** = positive truth  
- **E** = positive posetion  
- **O** = negative negation  
- **I** = negative negotion  

---

## 2. Truth Semantics in Conditionals

When a Laegna number is used in an `if` condition:

- Numbers starting with **A** or **E** → **true**
- Numbers starting with **O** or **I** → **false**

This is structural truth, not boolean coercion.

Example (escaped fence):

```text
if 0LAA [ ...true branch... ]
if 0LOI [ ...false branch... ]
```

---

## 3. Iteration Semantics

### 3.1 Iterating wave numbers

Wave numbers have a natural ordering:
- **0WII** → lowest  
- **0WEE** → highest  

Example (escaped fence):

```text
for a in 0WII to 0WEE [
    ...do something...
]
```

### 3.2 Iterating by digit length R

Digit length is essential in Laegna math.

- **0r2** → all 2‑digit Laegna numbers  
- **0r3** → all 3‑digit Laegna numbers  
- **0r2 to 0r4** → iterate lengths 2, 3, 4

Example (escaped fence):

```text
for a in 0r2 [
    ...all 2-digit numbers...
]

for a in 0r2 to 0r4 [
    ...2-digit, 3-digit, 4-digit numbers...
]
```

This is a structural iteration over the combinatorial universe of digit sequences.

---

## 4. Basic Math Operations

Laegna numbers support:
- **+** addition  
- **-** subtraction  
- **\*** multiplication  
- **/** division  
- **^** or **\*\*** exponentiation  

Operations preserve:
- Type (L/W),
- Sign (uppercase/lowercase),
- Digit length R,
- Structural truth.

Example (escaped fence):

```text
0LAA + 0LOE
0wAI * 0WEE
0LxA2 ^ 0Lb01
```

---

## 5. Sign, Absolute Value, and Structural Queries

### 5.1 Sign

- Uppercase prefix → unsigned  
- Lowercase prefix → signed  

Example (escaped fence):

```text
sign? 0LAA   ; unsigned
sign? 0lAA   ; signed
```

### 5.2 Absolute value

Absolute value removes sign but preserves type:

```text
abs 0lOI  → 0LOI
abs 0wAE  → 0WAE
```

### 5.3 Octave

Octave is a structural property of digit length R.

You can access it via:
- **Oct(n)**  
- **n.oct**  
- **n/oct**  

Example (escaped fence):

```text
Oct(0LAA)   → octave of R
0LAA.oct    → same
```

---

## 6. Clean Syntax Specification

Below is a clean syntax definition for Laegna numbers.

### 6.1 Prefix grammar

```text
prefix = "0" type base
type   = ("L" | "W" | "l" | "w")
base   = ("" | "b" | "x")
```

### 6.2 Digit grammar

```text
digit = ("A" | "E" | "O" | "I")
digits = digit+
```

### 6.3 Full number

```text
laegna-number = prefix digits
```

### 6.4 Length R

```text
R = length of digits
```

### 6.5 Octave

```text
octave = f(R)
```

---

## 7. How Pieces Fit Together (Coherent Explanation)

### 7.1 Dialect-native parsing

Red/Rebol dialects allow Laegna numbers to be parsed as:
- Structured values,
- With type metadata,
- With digit arrays,
- With truth semantics,
- With octave metadata.

### 7.2 Conditionals

Conditionals use the **first digit** to determine truth:
- A/E → true  
- O/I → false  

This allows Laegna numbers to behave like logical entities.

### 7.3 Iteration

Iteration uses:
- Digit length R,
- Wave ordering,
- Structural combinatorics.

Thus:
- `0r2` iterates all 2-digit numbers,
- `0r2 to 0r4` iterates lengths 2–4,
- `0WII to 0WEE` iterates wave numbers.

### 7.4 Math operations

Operations preserve:
- Type,
- Sign,
- Digit length,
- Structural truth.

This ensures Laegna numbers behave consistently across:
- Arithmetic,
- Logic,
- Combinatorics.

### 7.5 Octave

Octave is derived from R and used in:
- Growth models,
- Lane projections,
- Laegna physics,
- Spireason reasoning.

It is accessible via:
- `Oct(n)`
- `n.oct`

---

## 8. Example: Full Scenario

Below is a complete scenario showing how Laegna numbers behave.

### 8.1 Define numbers

```text
a = 0LAA
b = 0WIO
c = 0r3
```

### 8.2 Conditional truth

```text
if a [ ...true... ]
if b [ ...false... ]
```

### 8.3 Iteration

```text
for x in 0r2 to 0r4 [
    ...iterate lengths 2, 3, 4...
]
```

### 8.4 Math

```text
d = a + b
e = a ^ 0LxA2
f = abs 0lOI
```

### 8.5 Octave

```text
o = a.oct
```

---

## 9. Summary

Laegna numbers are:
- Typed,
- Signed/unsigned,
- Digit-structured,
- Truth-bearing,
- Iteration-aware,
- Octave-linked.

Dialect-native languages like Red/Rebol allow:
- Clean syntax,
- Structural semantics,
- Custom iteration,
- Truth integration,
- Math operations,
- Octave access.

This article shows how all pieces fit together into a coherent, mathematically meaningful system.

```rebol
;---------------------------
; REBOL: “0l” as a custom numeric-like type
;---------------------------

; define a constructor: 0l value is stored as a tagged block [0l <number>]
make-0l: func [n [integer! decimal!]] [
    reduce ['0l n]
]

; extractor: get the numeric payload
get-0l: func [v [block!]] [
    second v
]

; arithmetic “operators” implemented as functions
add-0l: func [a [block!] b [block!]] [
    make-0l get-0l a + get-0l b
]

sub-0l: func [a [block!] b [block!]] [
    make-0l get-0l a - get-0l b
]

mul-0l: func [a [block!] b [block!]] [
    make-0l get-0l a * get-0l b
]

div-0l: func [a [block!] b [block!]] [
    make-0l get-0l a / get-0l b
]

; truthiness: non‑zero is TRUE, zero is FALSE
truth-0l?: func [v [block!]] [
    get-0l v <> 0
]

; iterable: walk a series of plain numbers, wrap each as 0l
foreach-0l: func [series [block!] body [block!]] [
    foreach n series [
        do bind body 'n
    ]
]

;---------------------------
; usage
;---------------------------

a: make-0l 2
b: make-0l 3

c: add-0l a b
print ["2 + 3 as 0l =" get-0l c]

if truth-0l? c [
    print "c is non-zero in 0l logic"
]

foreach-0l [0 1 2 3] [
    x: make-0l n
    if truth-0l? x [
        print ["non-zero 0l:" get-0l x]
    ]
]
```

```red
;---------------------------
; Red: “0l” as an object-based numeric-like type
;---------------------------

; define a module-like context for the 0l “type”
0l!: context [

    ; constructor: make a 0l object
    make: func [n [integer! float!]] [
        context [
            type:  '0l
            value: n
        ]
    ]

    ; arithmetic “operators”
    add: func [a b] [
        make a/value + b/value
    ]

    sub: func [a b] [
        make a/value - b/value
    ]

    mul: func [a b] [
        make a/value * b/value
    ]

    div: func [a b] [
        make a/value / b/value
    ]

    ; truthiness: non‑zero is TRUE
    truth?: func [x] [
        x/value <> 0
    ]
]

;---------------------------
; usage
;---------------------------

a: 0l!/make 2
b: 0l!/make 3

c: 0l!/add a b
print ["2 + 3 as 0l =" c/value]

if 0l!/truth? c [
    print "c is non-zero in 0l logic"
]

nums: [0 1 2 3]

foreach n nums [
    x: 0l!/make n
    if 0l!/truth? x [
        print ["non-zero 0l:" x/value]
    ]
]
```
