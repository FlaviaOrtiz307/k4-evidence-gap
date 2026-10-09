# Kryptos K4 — Reproducible Negative Results

**Independent Research:** Flavia Ortiz
**Date:** October 9, 2026
**Version:** 1.0 — First Publication

## 1. Introduction

This document presents seven negative tests conducted as part of an independent investigation into the fourth encrypted section of Kryptos (K4), the cryptographic sculpture created by Jim Sanborn.

The purpose is to document specific mathematical incompatibilities using explicit data, calculations, and reproducible procedures.

The seven tests are organized into three categories:

* Direct periodic Vigenère encryption.
* Direct monoalphabetic substitution.
* Alphabet-size restrictions in classical 5×5 cipher systems.

**This research does not present a cryptographic solution to K4.**

The conclusions apply only to the specific models and assumptions tested. They do not eliminate entire cipher families, modified implementations, or combinations of multiple cryptographic operations.

## 2. Data and Conventions

K4 consists of 97 ciphertext characters:

```
OBKRUOXOGHULBSOLIFBBWFLRVQQPRNGKSSOTWTQSJQSSEKZZWATJKLUDIAWINFBNYPVTTMZFPKWGDKZXTJCDIGKUHUAUEKCAR
```

Four publicly confirmed plaintext fragments are used:

| Positions (1-based) | Ciphertext | Plaintext |
| ------------------- | ---------- | --------- |
| 22–25               | FLRV       | EAST      |
| 26–34               | QQPRNGKSS  | NORTHEAST |
| 64–69               | NYPVTT     | BERLIN    |
| 70–74               | MZFPK      | CLOCK     |

These produce two contiguous known-plaintext sequences:

* Positions 22–34: EASTNORTHEAST.
* Positions 64–74: BERLINCLOCK.

### Conventions

* Positions are numbered starting from 1.
* The English alphabet A–Z is used.
* A = 0 and Z = 25.
* Arithmetic is performed modulo 26.
* The Vigenère tests assume a single continuously repeating key applied directly to the original ciphertext alignment.
* No preliminary transposition, key reset, or additional transformation is assumed.

No speculative complete plaintext reconstruction is used in these tests.

## 3. Test 1 — Direct Vigenère, Period 19

### Hypothesis

K4 was encrypted using standard Vigenère encryption with a key repeating every 19 characters.

### Method

For standard Vigenère encryption, the required key shift at a known position is:

K(i) = (C(i) − P(i)) mod 26

Positions separated by an integer multiple of the key period must require identical key shifts.

### Result

Positions 26 and 64 are separated by 38 characters:

38 = 2 × 19.

However, the required shifts are:

* Position 26: shift 3.
* Position 64: shift 12.

**Contradiction: 3 ≠ 12.**

The complete comparison produces seven conflicting position pairs.

### Conclusion

Standard direct Vigenère encryption with a continuously repeating key of period 19 is incompatible with the publicly known plaintext fragments.

This test does not exclude additional transformations, altered key alignment, or other cryptographic systems.

## 4. Test 2 — Direct Vigenère, Period 20

### Hypothesis

K4 uses standard Vigenère encryption with a key repeating every 20 positions.

### Method

Known positions separated by multiples of 20 are compared to determine whether they require identical key shifts.

### Result

Positions 24 and 64 are separated by 40 characters:

40 = 2 × 20.

The required shifts are:

* Position 24: shift 25.
* Position 64: shift 12.

**Contradiction: 25 ≠ 12.**

Eleven conflicting position pairs were identified.

### Conclusion

Direct standard Vigenère encryption with a continuously repeating key of period 20 is incompatible with the known plaintext under the tested conditions.

## 5. Test 3 — Direct Vigenère, Period 21

### Hypothesis

K4 uses a single standard Vigenère key repeating every 21 characters.

### Method

Required key shifts at known positions separated by multiples of 21 are compared.

### Result

Positions 22 and 64 are separated by 42 characters:

42 = 2 × 21.

Their required shifts are:

* Position 22: shift 1.
* Position 64: shift 12.

**Contradiction: 1 ≠ 12.**

All eleven comparable position pairs require different shifts.

### Conclusion

Standard direct Vigenère encryption with period 21 and continuous key alignment is incompatible with the publicly known plaintext.

This finding does not establish that the number 21 is irrelevant to every possible cryptographic construction.

## 6. Test 4 — Direct Vigenère, Period 24

### Hypothesis

K4 uses standard Vigenère encryption with a key repeating every 24 positions.

### Method

Known plaintext positions sharing the same residue modulo 24 are compared.

### Result

Positions 22 and 70 are separated by 48 characters:

48 = 2 × 24.

Their required shifts are:

* Position 22: shift 1.
* Position 70: shift 10.

**Contradiction: 1 ≠ 10.**

Five conflicting position pairs were identified.

### Conclusion

Standard direct Vigenère encryption with period 24 and continuous key alignment is incompatible with the known plaintext fragments.

This result does not exclude other cryptographic systems involving groups of 24 characters.

## 7. Test 5 — Direct Vigenère, Period 42

### Hypothesis

K4 uses a single standard Vigenère key repeating every 42 positions.

### Method

Known plaintext positions separated by 42 characters are compared.

### Result

Positions 22 and 64 require:

* Position 22: shift 1.
* Position 64: shift 12.

**Contradiction: 1 ≠ 12.**

Eleven conflicting position pairs were identified.

These are the same eleven pairs used in the period-21 comparison. They do not represent eleven additional independent observations.

### Conclusion

Standard direct Vigenère encryption with period 42 and continuous key alignment is incompatible with the known plaintext fragments.

Key resets, transpositions, and compound encryption systems are outside the scope of this test.

## 8. Test 6 — Direct Monoalphabetic Substitution

### Hypothesis

Every ciphertext letter consistently represents the same plaintext letter through one fixed substitution table.

### Method

Under direct monoalphabetic substitution, a given ciphertext symbol must always map to the same plaintext symbol.

Occurrences of identical ciphertext letters within the known plaintext regions are compared.

### Result

The ciphertext letter F occurs in two confirmed positions:

* Position 22: F corresponds to E.
* Position 72: F corresponds to O.

A single fixed substitution table would therefore need to assign two different plaintext letters to the same ciphertext letter.

**Contradiction: E ≠ O.**

### Conclusion

Direct monoalphabetic substitution using one fixed mapping, without additional operations, is incompatible with the confirmed plaintext fragments.

This result does not exclude polyalphabetic substitution or composite encryption systems.

## 9. Test 7 — Alphabet-Size Restriction in Classical 5×5 Systems

### Hypothesis

K4 is the direct output of a classical Bifid or Four-square implementation strictly limited to a 25-symbol alphabet, without subsequent symbol-expanding conversions.

### Method

A classical 5×5 alphabet grid contains 25 positions.

The number of distinct ciphertext symbols in K4 is counted and compared with the maximum alphabet capacity.

### Result

The K4 ciphertext contains all 26 letters of the English alphabet.

Therefore:

* Available symbols in the tested 5×5 alphabet: 25.
* Distinct symbols observed in K4: 26.

**Contradiction: 26 observed symbols exceed the available 25-symbol alphabet.**

A subsequent transposition alone cannot increase the number of distinct symbols.

### Conclusion

Strictly 25-symbol implementations of classical Bifid and Four-square cannot directly produce the complete K4 ciphertext.

This restriction does not exclude modified implementations, expanded alphabets, special character handling, or additional substitution stages.

## 10. Reproducibility — Python Code

The following script reproduces all seven tests using the Python standard library.

No external dependencies or internet connection are required.

```python
C = (
    "OBKRUOXOGHULBSOLIFBBWFLR"
    "VQQPRNGKSSOTWTQSJQSSEKZZ"
    "WATJKLUDIAWINFBNYPVTTMZF"
    "PKWGDKZXTJCDIGKUHUAUEKCA"
    "R"
)

assert len(C) == 97

# Publicly confirmed plaintext positions.
# Position numbering starts at 1.

known = {
    **dict(zip(range(22, 35), "EASTNORTHEAST")),
    **dict(zip(range(64, 75), "BERLINCLOCK")),
}

assert len(known) == 24

# Verify ciphertext alignment.

assert C[21:34] == "FLRVQQPRNGKSS"
assert C[63:74] == "NYPVTTMZFPK"

# Calculate standard Vigenere key shifts.

shifts = {
    i: (ord(C[i - 1]) - ord(p)) % 26
    for i, p in known.items()
}

expected = {
    19: 7,
    20: 11,
    21: 11,
    24: 5,
    42: 11,
}

witnesses = {
    19: (26, 64, 3, 12),
    20: (24, 64, 25, 12),
    21: (22, 64, 1, 12),
    24: (22, 70, 1, 10),
    42: (22, 64, 1, 12),
}

for period, count in expected.items():

    conflicts = [
        (i, j, shifts[i], shifts[j])
        for i in known
        for j in known
        if i < j
        and (j - i) % period == 0
        and shifts[i] != shifts[j]
    ]

    assert len(conflicts) == count
    assert witnesses[period] in conflicts

    print(
        f"Period {period}: "
        f"{len(conflicts)} contradictions"
    )

# Direct monoalphabetic substitution.

assert C[21] == C[71] == "F"
assert known[22] == "E"
assert known[72] == "O"

print("Direct monoalphabetic substitution: incompatible")

# Classical 25-symbol alphabet restriction.

assert len(set(C)) == 26

print("Distinct ciphertext letters:", len(set(C)))

print("All checks passed")
```

### Expected output

```
Period 19: 7 contradictions
Period 20: 11 contradictions
Period 21: 11 contradictions
Period 24: 5 contradictions
Period 42: 11 contradictions
Direct monoalphabetic substitution: incompatible
Distinct ciphertext letters: 26
All checks passed
```

The contradiction counts include all ordered position pairs satisfying i < j among the 24 confirmed plaintext positions that share a residue class modulo the tested period but require different Vigenère shifts.

Each test also includes an explicit witness that can be checked independently.

## 11. Scope and Limitations

These results refute only the specific implementations examined.

They do not establish that:

* K4 never uses Vigenère encryption.
* K4 contains no transposition.
* K4 cannot employ multiple alphabets.
* K4 cannot involve combined cryptographic operations.
* The original encryption mechanism has been identified.

The five periodicity tests examine five specific hypotheses about direct Vigenère encryption. They do not constitute a general rejection of Vigenère-based methods.

The period-21 and period-42 tests share the same eleven compared position pairs. They must not be interpreted as independent sets of observations.

The monoalphabetic substitution test addresses only direct substitution through one fixed mapping.

The 25-symbol alphabet test applies only to implementations whose ciphertext output is restricted to a 25-character alphabet.

The conclusions are independent of any unauthenticated reconstruction of K4's complete plaintext.

This document presents bounded, reproducible negative results rather than a definitive explanation of the Kryptos K4 encryption process.

## 12. References

The following publicly accessible sources document the Kryptos sculpture, the ciphertext, and the confirmed plaintext clues used in these tests.

**1. Central Intelligence Agency (CIA).**

*"Kryptos" Sculpture.*

Official information about the artwork, its history, and the encrypted inscription.

https://www.cia.gov/legacy/headquarters/kryptos-sculpture/

**2. WIRED (2014).**

*Finally, a New Clue to Solve the CIA's Mysterious Kryptos Sculpture.*

Documents the disclosure of CLOCK following BERLIN at K4 positions 64–74.

https://www.wired.com/2014/11/second-kryptos-clue/

**3. Smithsonian Magazine (2020).**

*New Clue May Be the Key to Cracking CIA Sculpture's Final Puzzling Passage.*

Reports Jim Sanborn's disclosure of the NORTHEAST plaintext clue.

https://www.smithsonianmag.com/smart-news/third-and-final-clue-released-ci-sculptures-last-puzzling-passage-180974102/

**4. Klaus Schmeh, Cipherbrain (2020).**

*Jim Sanborn publishes another Kryptos clue.*

Documents the confirmation of EAST at positions 22–25, immediately preceding NORTHEAST.

https://scienceblogs.de/klausis-krypto-kolumne/2020/08/24/jim-sanborn-publishes-another-new-kryptos-clue/

**5. Steven Levy, WIRED (2025).**

*Inside the Messy, Accidental Kryptos Reveal.*

Reports the archival recovery of K4's plaintext and distinguishes that discovery from cryptographically deriving the plaintext.

https://www.wired.com/story/kryptos-code-reveal/

## 13. Research Status

In 2025, researchers recovered the original K4 plaintext from archival documents associated with Jim Sanborn. Sanborn confirmed its authenticity. This discovery did not constitute a cryptographic derivation of the plaintext from the ciphertext.

The present research does not claim to have recovered the original encryption algorithm or independently solved K4.

It also does not claim that every negative result reported here is previously unpublished.

The purpose is to document clearly defined incompatibilities examined through independent research, together with procedures that allow others to reproduce and challenge the findings.

The tests presented here do not establish the original cryptographic mechanism.

---

**Flavia Ortiz**
Independent Kryptos K4 Research
October 9, 2026

**Version 1.0 — First Publication**
