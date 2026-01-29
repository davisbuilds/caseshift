# Installing caseshift

`caseshift` is a ghost library—it contains no code, only specifications. You generate the implementation yourself using an AI coding assistant.

## Quick Start

Copy this prompt into Claude, Codex, Cursor, or your preferred AI coding tool:

```
Implement the caseshift library in [LANGUAGE].

1. Read SPEC.md for complete behavior specification
2. Parse tests.yaml and generate a test file
3. Implement all twelve functions: to_camel, to_pascal, to_snake, 
   to_screaming, to_kebab, to_train, to_title, to_sentence, 
   to_flat, to_upper_flat, detect, split_words
4. Run tests until all pass
5. Place implementation in [LOCATION]

All tests.yaml test cases must pass. See SPEC.md "Testing" section 
for test generation examples.
```

Replace `[LANGUAGE]` with your target language (Python, Ruby, JavaScript, Go, Rust, etc.) and `[LOCATION]` with your desired file path.

## What You Get

Twelve pure functions for case conversion:

| Function | Output | Example |
|----------|--------|---------|
| `to_camel` | lowerCamelCase | `hello_world` → `helloWorld` |
| `to_pascal` | PascalCase | `hello_world` → `HelloWorld` |
| `to_snake` | snake_case | `helloWorld` → `hello_world` |
| `to_screaming` | SCREAMING_SNAKE | `helloWorld` → `HELLO_WORLD` |
| `to_kebab` | kebab-case | `helloWorld` → `hello-world` |
| `to_train` | Train-Case | `helloWorld` → `Hello-World` |
| `to_title` | Title Case | `helloWorld` → `Hello World` |
| `to_sentence` | Sentence case | `helloWorld` → `Hello world` |
| `to_flat` | flatcase | `helloWorld` → `helloworld` |
| `to_upper_flat` | UPPERFLATCASE | `helloWorld` → `HELLOWORLD` |
| `detect` | Detect case style | `helloWorld` → `"camel"` |
| `split_words` | Word array | `helloWorld` → `["hello", "world"]` |

## Files in This Repository

| File | Purpose |
|------|---------|
| `SPEC.md` | Complete behavior specification (~600 lines) |
| `tests.yaml` | Language-agnostic test cases (156 tests) |
| `INSTALL.md` | This file |

## How It Works

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  SPEC.md    │     │ tests.yaml  │     │   Your AI   │
│  (behavior) │ ──▶ │  (tests)    │ ──▶ │   (impl)    │
└─────────────┘     └─────────────┘     └─────────────┘
                                               │
                                               ▼
                                        ┌─────────────┐
                                        │  Working    │
                                        │   Library   │
                                        └─────────────┘
```

1. **Read**: AI reads the specification to understand behavior
2. **Generate**: AI creates test file from `tests.yaml`
3. **Implement**: AI writes code to pass all tests
4. **Verify**: All 156 tests pass

## Example Implementations

### Python

```
Implement the caseshift library in Python.

1. Read SPEC.md for complete behavior specification
2. Parse tests.yaml and generate pytest tests
3. Implement all twelve functions: to_camel, to_pascal, to_snake, 
   to_screaming, to_kebab, to_train, to_title, to_sentence, 
   to_flat, to_upper_flat, detect, split_words
4. Run tests until all pass
5. Place implementation in ./caseshift.py with tests in ./test_caseshift.py

Use snake_case for function names. Return None for detect() when undetectable.
```

### JavaScript/TypeScript

```
Implement the caseshift library in TypeScript.

1. Read SPEC.md for complete behavior specification
2. Parse tests.yaml and generate Jest tests
3. Implement all twelve functions with camelCase names: toCamel, toPascal, 
   toSnake, toScreaming, toKebab, toTrain, toTitle, toSentence, 
   toFlat, toUpperFlat, detect, splitWords
4. Run tests until all pass
5. Place implementation in ./src/caseshift.ts with tests in ./src/caseshift.test.ts

Include TypeScript type definitions. Return null for detect() when undetectable.
```

### Ruby

```
Implement the caseshift library in Ruby.

1. Read SPEC.md for complete behavior specification
2. Parse tests.yaml and generate RSpec tests
3. Implement all twelve functions: to_camel, to_pascal, to_snake, 
   to_screaming, to_kebab, to_train, to_title, to_sentence, 
   to_flat, to_upper_flat, detect, split_words
4. Run tests until all pass
5. Create a gem structure in ./lib/caseshift.rb with tests in ./spec/

Return nil for detect() when undetectable.
```

### Go

```
Implement the caseshift library in Go.

1. Read SPEC.md for complete behavior specification
2. Parse tests.yaml and generate table-driven tests
3. Implement all twelve functions with PascalCase names: ToCamel, ToPascal, 
   ToSnake, ToScreaming, ToKebab, ToTrain, ToTitle, ToSentence, 
   ToFlat, ToUpperFlat, Detect, SplitWords
4. Run tests until all pass
5. Place implementation in ./caseshift.go with tests in ./caseshift_test.go

Detect() should return (string, bool) tuple where bool indicates success.
SplitWords() returns []string.
```

### Rust

```
Implement the caseshift library in Rust.

1. Read SPEC.md for complete behavior specification
2. Parse tests.yaml and generate unit tests
3. Implement all twelve functions: to_camel, to_pascal, to_snake, 
   to_screaming, to_kebab, to_train, to_title, to_sentence, 
   to_flat, to_upper_flat, detect, split_words
4. Run tests until all pass
5. Create a library crate in ./src/lib.rs

Use Option<String> for detect() return type. Use Vec<String> for split_words().
Consider implementing a Case enum for type-safe case representation.
```

### PHP

```
Implement the caseshift library in PHP 8+.

1. Read SPEC.md for complete behavior specification
2. Parse tests.yaml and generate PHPUnit tests
3. Implement all twelve functions: toCamel, toPascal, toSnake, 
   toScreaming, toKebab, toTrain, toTitle, toSentence, 
   toFlat, toUpperFlat, detect, splitWords
4. Run tests until all pass
5. Place implementation in ./src/CaseShift.php with tests in ./tests/

Use a class with static methods. Return null for detect() when undetectable.
```

### Elixir

```
Implement the caseshift library in Elixir.

1. Read SPEC.md for complete behavior specification
2. Parse tests.yaml and generate ExUnit tests
3. Implement all twelve functions: to_camel, to_pascal, to_snake, 
   to_screaming, to_kebab, to_train, to_title, to_sentence, 
   to_flat, to_upper_flat, detect, split_words
4. Run tests until all pass
5. Create a Mix project structure

Return nil for detect() when undetectable. Return list for split_words().
```

### Java

```
Implement the caseshift library in Java 17+.

1. Read SPEC.md for complete behavior specification
2. Parse tests.yaml and generate JUnit 5 tests
3. Implement all twelve functions in a CaseShift class: toCamel, toPascal, 
   toSnake, toScreaming, toKebab, toTrain, toTitle, toSentence, 
   toFlat, toUpperFlat, detect, splitWords
4. Run tests until all pass
5. Place implementation in ./src/main/java/CaseShift.java

Use Optional<String> for detect(). Use List<String> for splitWords().
```

### C#

```
Implement the caseshift library in C# 11+.

1. Read SPEC.md for complete behavior specification
2. Parse tests.yaml and generate xUnit tests
3. Implement all twelve functions in a CaseShift class: ToCamel, ToPascal, 
   ToSnake, ToScreaming, ToKebab, ToTrain, ToTitle, ToSentence, 
   ToFlat, ToUpperFlat, Detect, SplitWords
4. Run tests until all pass
5. Create a class library project

Use string? (nullable) for Detect(). Use string[] for SplitWords().
```

## Testing Your Implementation

After generation, run your language's test suite:

```bash
# Python
pytest test_caseshift.py -v

# JavaScript/TypeScript
npm test

# Ruby
rspec spec/

# Go
go test -v

# Rust
cargo test

# PHP
./vendor/bin/phpunit tests/

# Elixir
mix test

# Java
mvn test

# C#
dotnet test
```

Expected output: **156 tests passing**

## Why Ghost Libraries?

Traditional libraries ship code. Ghost libraries ship specifications.

**Benefits:**
- Works in any language
- No dependencies to manage  
- Customizable to your conventions
- Generated fresh for each project
- Consistent behavior across your polyglot stack

**Trade-offs:**
- Requires AI coding assistant
- No community-maintained patches
- Implementation varies between generations

## Common Use Cases

### API Integration
```python
# Convert between JavaScript API (camelCase) and Python (snake_case)
api_response = {"firstName": "John", "lastName": "Doe"}
python_dict = {to_snake(k): v for k, v in api_response.items()}
# {"first_name": "John", "last_name": "Doe"}
```

### Code Generation
```javascript
// Generate class name from table name
const tableName = "user_profiles";
const className = toPascal(tableName);  // "UserProfiles"
```

### CSS Property Conversion
```javascript
// JavaScript style object to CSS
const jsStyle = { backgroundColor: "red", fontSize: "14px" };
const cssProps = Object.fromEntries(
  Object.entries(jsStyle).map(([k, v]) => [toKebab(k), v])
);
// { "background-color": "red", "font-size": "14px" }
```

### Environment Variables
```python
# Config key to environment variable
config_key = "databaseUrl"
env_var = to_screaming(config_key)  # "DATABASE_URL"
```

## Extending the Spec

Want to add functionality? Fork this repository and:

1. Add behavior description to `SPEC.md`
2. Add test cases to `tests.yaml`
3. Regenerate your implementation

Common extensions:
- Custom acronym handling (preserve "HTTP" instead of "Http")
- Locale-aware title case (articles: "the", "a", "of")
- Additional case styles (dot.case, path/case, cobol-case)
- Preserve specific words (brand names, technical terms)

## License

MIT License. Use freely, modify freely, distribute freely.

---

## Troubleshooting

### Acronyms not handled correctly?

The spec normalizes acronyms: `XMLParser` → `xml_parser` → `XmlParser`. If you want to preserve acronyms (`XMLParser` → `xml_parser` → `XMLParser`), you'll need to extend the spec with an acronym preservation option.

### Unicode characters causing issues?

The spec preserves Unicode letters and applies Unicode case mapping. Ensure your implementation uses Unicode-aware case conversion functions:

- Python: `str.lower()`, `str.upper()` (Unicode-aware by default)
- JavaScript: `toLowerCase()`, `toUpperCase()` (Unicode-aware)
- Go: `strings.ToLower()`, `strings.ToUpper()` (Unicode-aware)
- Rust: `.to_lowercase()`, `.to_uppercase()` (Unicode-aware)

### Detection returning wrong result?

Detection has strict rules. Mixed formats return `null`:
- `hello_World` → `null` (mixed snake and camel)
- `Hello-world` → `null` (mixed train and kebab)

If you need fuzzy detection, extend the spec with a `detect_fuzzy()` function.

### Some tests failing?

Re-read the `SPEC.md` Word Splitting Algorithm section. Common issues:
- Acronym boundary detection (`XMLParser` → `[xml, parser]`, not `[x, m, l, parser]`)
- Number boundary handling (`v2API` → `[v, 2, api]`)
- Consecutive delimiters (`hello__world` → `[hello, world]`)

If a test seems wrong, open an issue! The spec may have bugs too.
