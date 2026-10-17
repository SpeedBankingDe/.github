<div align="center">

# SpeedBanking

Fast, allocation-free, zero-dependency Java tooling for IBAN, BIC and German bank account validation.

<a href="https://central.sonatype.com/artifact/de.speedbanking/iban-commons"><img src="https://img.shields.io/maven-central/v/de.speedbanking/iban-commons?label=Maven%20Central&style=flat-square" alt="Maven Central"></a>
<a href="https://github.com/SpeedBankingDe/iban-commons/actions/workflows/ci.yml"><img src="https://img.shields.io/github/actions/workflow/status/SpeedBankingDe/iban-commons/ci.yml?label=Build&style=flat-square" alt="Build"></a>
<a href="https://javadoc.io/doc/de.speedbanking/iban-commons"><img src="https://javadoc.io/badge2/de.speedbanking/iban-commons/javadoc.svg?style=flat-square" alt="Javadoc"></a>
<a href="https://github.com/SpeedBankingDe/iban-commons/stargazers"><img src="https://img.shields.io/github/stars/SpeedBankingDe/iban-commons?style=flat-square&label=Stars" alt="GitHub Stars"></a>
<img src="https://img.shields.io/badge/Java-8%2B-blue?style=flat-square" alt="Java 8+">
<img src="https://img.shields.io/badge/Android-API%2021%2B-3DDC84?style=flat-square" alt="Android API 21+">
<img src="https://img.shields.io/badge/License-Apache%202.0-blue?style=flat-square" alt="Apache 2.0">

[Website](https://www.speedbanking.de/) · [Getting started](https://github.com/SpeedBankingDe/iban-commons#-quick-start) · [Benchmarks](https://github.com/SpeedBankingDe/iban-commons-benchmarks) · [Discussions](https://github.com/SpeedBankingDe/iban-commons/discussions)

</div>

---

We build [iban-commons](https://github.com/SpeedBankingDe/iban-commons), a Java library for parsing, validating and formatting IBANs (ISO 13616) and BICs (ISO 9362). It covers 127 countries, runs on Java 8 and Android, and the core has no dependencies outside the JDK. Validation does not allocate, which makes it a good fit for batch processing, payment pipelines and anything else that checks a lot of account numbers.

Add it with Maven (use the current version from the Maven Central badge in place of X.Y.Z):

```xml
<dependency>
    <groupId>de.speedbanking</groupId>
    <artifactId>iban-commons</artifactId>
    <version>X.Y.Z</version>
</dependency>
```

```java
Iban iban = Iban.of("DE91100000000123456789");   // throws InvalidIbanException
Optional<Iban> maybe = Iban.tryParse(input);      // no exception
boolean valid = Bic.isValid("DEUTDEFFXXX");

iban.getBankCode();        // "10000000"
iban.toFormattedString();  // "DE91 1000 0000 0123 4567 89"
```

### Modules

| Artifact | What it does |
|----------|--------------|
| [`iban-commons`](https://github.com/SpeedBankingDe/iban-commons) | IBAN and BIC models, validation, formatting, builder with national check digits, country and currency metadata |
| [`iban-commons-bankdata`](https://github.com/SpeedBankingDe/iban-commons/tree/master/iban-commons-bankdata) | BIC and bank name by IBAN or bank code (DE, AT, CH, CZ, BE, PL, NL, ES, FR), bundled offline data with background refresh |
| [`iban-commons-de-checkdigit`](https://github.com/SpeedBankingDe/iban-commons/tree/master/iban-commons-de-checkdigit) | German account number (Kontonummer) check digit methods per Bankleitzahl, standalone |
| [`iban-commons-validation`](https://github.com/SpeedBankingDe/iban-commons/tree/master/iban-commons-validation) | Jakarta Bean Validation constraints `@ValidIban` and `@ValidBic` |
| [`iban-commons-junit`](https://github.com/SpeedBankingDe/iban-commons/tree/master/iban-commons-junit) | JUnit 5 sources for parameterized tests over countries and random IBANs |

### How fast?

Measured with JMH against the other Java IBAN libraries, rejecting invalid IBANs on a single core. Setup, raw numbers and the accept path are in [iban-commons-benchmarks](https://github.com/SpeedBankingDe/iban-commons-benchmarks).

| Library | ops/s | B/op |
|---------|------:|-----:|
| **iban-commons** | **10,740,280** | **0** |
| jbanking | 7,880,633 | 154 |
| Apache Commons Validator | 6,531,841 | 247 |
| garvelink iban | 2,250,043 | 647 |
| iban4j | 1,801,759 | 1,156 |

### Get involved

Questions and ideas are welcome in [Discussions](https://github.com/SpeedBankingDe/iban-commons/discussions), bugs go to the [issue tracker](https://github.com/SpeedBankingDe/iban-commons/issues). If iban-commons is useful to you, a star helps others find it.
