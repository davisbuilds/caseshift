# caseshift: A Ghost Library for Case Conversion

A library for converting between programming case conventions—with no code.

`caseshift` provides twelve functions that convert identifiers between camelCase, PascalCase, snake_case, kebab-case, and more. It handles acronyms, numbers, and edge cases intelligently.

There are *many* libraries that perform similar functions. But none of them are language agnostic.

`caseshift` supports Python, Ruby, JavaScript, Go, Rust, PHP, Elixir, Java, C#, and more. It works in any language your AI coding assistant can write.

## What It Does

```
to_camel("hello_world")       → "helloWorld"
to_pascal("hello_world")      → "HelloWorld"
to_snake("helloWorld")        → "hello_world"
to_screaming("helloWorld")    → "HELLO_WORLD"
to_kebab("helloWorld")        → "hello-world"
to_train("helloWorld")        → "Hello-World"
to_title("helloWorld")        → "Hello World"
to_sentence("helloWorld")     → "Hello world"
to_flat("helloWorld")         → "helloworld"
to_upper_flat("helloWorld")   → "HELLOWORLD"

detect("helloWorld")          → "camel"
split_words("helloWorld")     → ["hello", "world"]
```

### Acronym-Aware

```
to_snake("XMLParser")         → "xml_parser"
to_snake("getHTTPResponse")   → "get_http_response"
to_pascal("xml_parser")       → "XmlParser"
to_camel("HTTP_REQUEST")      → "httpRequest"
```

### Number-Aware

```
to_snake("version2Release")   → "version2_release"
to_camel("v2_api")            → "v2Api"
split_words("test123abc")     → ["test", "123", "abc"]
```

## No Code?

This repository contains no implementation code. Instead, it contains:

| File | Purpose |
|------|---------|
| `SPEC.md` | Detailed behavior specification |
| `tests.yaml` | 156 language-agnostic test cases |
| `INSTALL.md` | Instructions for generating your implementation |

## Installation

Copy this into Claude, Codex, Cursor, or any AI coding assistant:

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

That's it. Pick your language, pick your location, and go.

## Supported Case Styles

| Style | Pattern | Example | Common Usage |
|-------|---------|---------|--------------|
| camel | lowerCamelCase | `helloWorld` | JavaScript, Java variables |
| pascal | PascalCase | `HelloWorld` | C#, Java classes |
| snake | snake_case | `hello_world` | Python, Ruby, Rust |
| screaming | SCREAMING_SNAKE | `HELLO_WORLD` | Constants, env vars |
| kebab | kebab-case | `hello-world` | CSS, URLs, CLI flags |
| train | Train-Case | `Hello-World` | HTTP headers |
| title | Title Case | `Hello World` | UI labels, headings |
| sentence | Sentence case | `Hello world` | Error messages |
| flat | flatcase | `helloworld` | Identifiers, hashtags |
| upper_flat | UPPERFLATCASE | `HELLOWORLD` | Legacy systems |

## Functions

### Conversion Functions

All conversion functions take a string and return the converted string:

```python
to_camel(text)      # → "helloWorld"
to_pascal(text)     # → "HelloWorld"
to_snake(text)      # → "hello_world"
to_screaming(text)  # → "HELLO_WORLD"
to_kebab(text)      # → "hello-world"
to_train(text)      # → "Hello-World"
to_title(text)      # → "Hello World"
to_sentence(text)   # → "Hello world"
to_flat(text)       # → "helloworld"
to_upper_flat(text) # → "HELLOWORLD"
```

### Detection

```python
detect(text)  # → "camel" | "pascal" | "snake" | ... | null
```

Returns the detected case style, or `null`/`None`/`nil` if the format is mixed or undetectable.

### Word Splitting

```python
split_words(text)  # → ["hello", "world"]
```

Returns an array of lowercase words. This is the core utility used by all conversion functions.

## Why Ghost Libraries?

> "What does software engineering look like when coding is free?"

Traditional libraries ship code. Ghost libraries ship specifications.

**Pros:**
- Works in any language
- No dependencies to manage
- Customizable to your conventions
- Consistent behavior across your polyglot stack
- Generated fresh for each project

**Cons:**
- Requires AI coding assistant
- No community-maintained patches
- Implementation varies between generations

For simple utilities like case conversion, the tradeoffs favor specs over code. You get identical behavior whether you're writing Python, JavaScript, or Rust.

## Test Coverage

156 test cases covering:
- All 10 conversion functions (100+ tests)
- Detection for all case styles (24 tests)
- Word splitting edge cases (28 tests)
- Acronym handling (XMLParser, getHTTPResponse)
- Number boundaries (version2Release, v2API)
- Empty strings, single characters
- Mixed and consecutive delimiters

## Real-World Examples

### API Response Transformation

```python
# JavaScript API (camelCase) → Python (snake_case)
response = {"firstName": "John", "lastName": "Doe", "emailAddress": "john@example.com"}
pythonic = {to_snake(k): v for k, v in response.items()}
# {"first_name": "John", "last_name": "Doe", "email_address": "john@example.com"}
```

### Code Generation

```javascript
// Database table → TypeScript interface
const tableName = "user_accounts";
const interfaceName = toPascal(tableName);  // "UserAccounts"
const fileName = toKebab(tableName) + ".ts"; // "user-accounts.ts"
```

### Environment Variable Mapping

```python
# Config → Environment Variable
config = {"databaseUrl": "...", "apiKey": "...", "maxRetries": 3}
env_vars = {to_screaming(k): v for k, v in config.items()}
# {"DATABASE_URL": "...", "API_KEY": "...", "MAX_RETRIES": 3}
```

### CSS-in-JS

```javascript
// JavaScript styles → CSS properties
const styles = { backgroundColor: "red", fontSize: "14px", marginTop: "10px" };
const cssProps = Object.entries(styles).map(([k, v]) => `${toKebab(k)}: ${v}`);
// ["background-color: red", "font-size: 14px", "margin-top: 10px"]
```

## License

MIT

## Contributing

Found a bug in the spec? Edge case not covered? Open an issue or PR.

When contributing:
1. Add behavior description to `SPEC.md`
2. Add corresponding test cases to `tests.yaml`
3. Verify the spec is implementable (test with your AI tool)

## See Also

- [whenwords](https://github.com/dbreunig/whenwords) — The original ghost library for relative time formatting
- [slugify](https://github.com/davisbuilds/slugify) — Ghost library for URL-safe string conversion
- [A Software Library with No Code](https://www.dbreunig.com/2026/01/08/a-software-library-with-no-code.html) — Blog post explaining the concept
