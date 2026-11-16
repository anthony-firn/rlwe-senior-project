# Quantum-secure encryption hardware: ring learning with errors

My computer engineering senior project at Cal Poly, San Luis Obispo (2019), with Lahiru Perera and Vasanth
Sadhasivan, advised by Andrew Danowitz and Paul Hummel. The report lists me under my former name, Anthony Fortner.

**[Read the report (PDF)](rLWE_Report.pdf)** · 8 pages, final revision August 2019

## What it covers

Public-key encryption such as RSA relies on problems that a large quantum computer could solve with Shor's
algorithm. Lattice-based schemes built on *learning with errors* (LWE) are believed to resist that attack. We
set out to build encryption hardware for the ring variant, ring-LWE, which uses much smaller keys and turns
the core work into polynomial multiplication.

- **The math:** private and public key generation, encryption and decryption under LWE, and why we chose
  ring-LWE over matrix LWE (speed, key size and multi-bit messages).
- **Validation first:** we implemented the scheme in Python with NumPy to confirm our understanding before
  designing hardware.
- **The hardware design:** a Gaussian sampler using rejection sampling, a number-theoretic transform (NTT) for
  fast polynomial multiplication, and a control unit sequencing them. A UART interface accepts an operation
  code, message and key, and returns the result; it doubled as our debugging port.
- **What changed along the way:** generating Gaussian samples in real time was too slow, so sampling moved to
  run independently and fill reserved memory when the control unit signals it; the control unit itself went
  through several revisions.

At the time of writing we had designed each component and begun assembling and testing the full system. The
report lists the remaining work: integration debugging, then measuring power and speed and optimizing.

## Files

| File | |
| --- | --- |
| [`rLWE_Report.pdf`](rLWE_Report.pdf), [`rLWE_Report.tex`](rLWE_Report.tex) | Final report and its LaTeX source |
| [`Senior_Project.pdf`](Senior_Project.pdf), [`Senior_Project.tex`](Senior_Project.tex) | Earlier draft (June 2019) |
| [`test.bib`](test.bib) | References |

The PDFs are the versions we submitted; the LaTeX source is kept as it was written.

## Key references

- O. Regev, "On lattices, learning with errors, random linear codes, and cryptography," STOC 2005.
- V. Lyubashevsky, C. Peikert and O. Regev, "On ideal lattices and learning with errors over rings,"
  [ePrint 2012/230](https://eprint.iacr.org/2012/230).
- R. de Clercq, S. S. Roy, F. Vercauteren and I. Verbauwhede, "Efficient software implementation of ring-LWE
  encryption," [ePrint 2014/725](https://eprint.iacr.org/2014/725).
