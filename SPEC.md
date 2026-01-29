# caseshift Specification

**Version:** 0.1.0  
**Status:** Draft

## Overview

`caseshift` is a library for converting strings between common programming case conventions. It transforms identifiers like "hello_world" to "helloWorld", "HelloWorld", "HELLO_WORLD", and more.

All functions are pure—no side effects, no I/O, no system state. The same input always produces the same output.

## Design Principles

1. **Pure functions only.** No side effects, no environment access.
2. **Strings are UTF-8.** All inputs and outputs are UTF-8 encoded.
3. **Word boundary detection.** Intelligently split on existing delimiters, case transitions, and numbers.
4. **Acronym-aware.** Handle common patterns like "XMLParser" and "getHTTPResponse" sensibly.
5. **Roundtrip-friendly.** Conversions should be reversible where possible.

---

## Case Conventions

| Name | Pattern | Example |
|------|---------|---------|
| `camel` | lowerCamelCase | `helloWorld` |
| `pascal` | UpperCamelCase / PascalCase | `HelloWorld` |
| `snake` | lower_snake_case | `hello_world` |
| `screaming` | SCREAMING_SNAKE_CASE | `HELLO_WORLD` |
| `kebab` | kebab-case / dash-case | `hello-world` |
| `train` | Train-Case | `Hello-World` |
| `title` | Title Case (spaces) | `Hello World` |
| `sentence` | Sentence case | `Hello world` |
| `flat` | flatcase | `helloworld` |
| `upper_flat` | UPPERFLATCASE | `HELLOWORLD` |

---

## Functions

### to_camel

Converts text to lowerCamelCase.

```
to_camel(text) → string
```

**Parameters:**

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `text` | string | yes | The text to convert |

**Returns:** String in lowerCamelCase format.

**Behavior:**

1. Split input into words (see Word Splitting)
2. Lowercase the first word entirely
3. Capitalize the first letter of each subsequent word, lowercase the rest
4. Join all words with no separator

**Examples:**

```
to_camel("hello_world")       → "helloWorld"
to_camel("HelloWorld")        → "helloWorld"
to_camel("hello-world")       → "helloWorld"
to_camel("HELLO_WORLD")       → "helloWorld"
to_camel("Hello World")       → "helloWorld"
to_camel("hello")             → "hello"
to_camel("HTTP_REQUEST")      → "httpRequest"
to_camel("getHTTPResponse")   → "getHttpResponse"
to_camel("XMLParser")         → "xmlParser"
to_camel("iPhone")            → "iphone"
to_camel("already camelCase") → "alreadyCamelcase"
```

---

### to_pascal

Converts text to PascalCase (UpperCamelCase).

```
to_pascal(text) → string
```

**Parameters:**

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `text` | string | yes | The text to convert |

**Returns:** String in PascalCase format.

**Behavior:**

1. Split input into words (see Word Splitting)
2. Capitalize the first letter of each word, lowercase the rest
3. Join all words with no separator

**Examples:**

```
to_pascal("hello_world")      → "HelloWorld"
to_pascal("helloWorld")       → "HelloWorld"
to_pascal("hello-world")      → "HelloWorld"
to_pascal("HELLO_WORLD")      → "HelloWorld"
to_pascal("Hello World")      → "HelloWorld"
to_pascal("HTTP_REQUEST")     → "HttpRequest"
to_pascal("getHTTPResponse")  → "GetHttpResponse"
to_pascal("XMLParser")        → "XmlParser"
to_pascal("iPhone")           → "Iphone"
```

---

### to_snake

Converts text to lower_snake_case.

```
to_snake(text) → string
```

**Parameters:**

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `text` | string | yes | The text to convert |

**Returns:** String in lower_snake_case format.

**Behavior:**

1. Split input into words (see Word Splitting)
2. Lowercase all words
3. Join with underscore `_`

**Examples:**

```
to_snake("helloWorld")        → "hello_world"
to_snake("HelloWorld")        → "hello_world"
to_snake("hello-world")       → "hello_world"
to_snake("HELLO_WORLD")       → "hello_world"
to_snake("Hello World")       → "hello_world"
to_snake("HTTP_REQUEST")      → "http_request"
to_snake("getHTTPResponse")   → "get_http_response"
to_snake("XMLParser")         → "xml_parser"
to_snake("version2Release")   → "version2_release"
to_snake("v2API")             → "v2_api"
```

---

### to_screaming

Converts text to SCREAMING_SNAKE_CASE (also called CONSTANT_CASE).

```
to_screaming(text) → string
```

**Parameters:**

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `text` | string | yes | The text to convert |

**Returns:** String in SCREAMING_SNAKE_CASE format.

**Behavior:**

1. Split input into words (see Word Splitting)
2. Uppercase all words
3. Join with underscore `_`

**Examples:**

```
to_screaming("helloWorld")       → "HELLO_WORLD"
to_screaming("HelloWorld")       → "HELLO_WORLD"
to_screaming("hello_world")      → "HELLO_WORLD"
to_screaming("hello-world")      → "HELLO_WORLD"
to_screaming("HTTP_REQUEST")     → "HTTP_REQUEST"
to_screaming("getHTTPResponse")  → "GET_HTTP_RESPONSE"
to_screaming("maxRetries")       → "MAX_RETRIES"
```

---

### to_kebab

Converts text to kebab-case (also called dash-case, lisp-case).

```
to_kebab(text) → string
```

**Parameters:**

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `text` | string | yes | The text to convert |

**Returns:** String in kebab-case format.

**Behavior:**

1. Split input into words (see Word Splitting)
2. Lowercase all words
3. Join with hyphen `-`

**Examples:**

```
to_kebab("helloWorld")        → "hello-world"
to_kebab("HelloWorld")        → "hello-world"
to_kebab("hello_world")       → "hello-world"
to_kebab("HELLO_WORLD")       → "hello-world"
to_kebab("Hello World")       → "hello-world"
to_kebab("getHTTPResponse")   → "get-http-response"
to_kebab("backgroundColor")   → "background-color"
```

---

### to_train

Converts text to Train-Case (also called HTTP-Header-Case).

```
to_train(text) → string
```

**Parameters:**

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `text` | string | yes | The text to convert |

**Returns:** String in Train-Case format.

**Behavior:**

1. Split input into words (see Word Splitting)
2. Capitalize the first letter of each word, lowercase the rest
3. Join with hyphen `-`

**Examples:**

```
to_train("helloWorld")        → "Hello-World"
to_train("hello_world")       → "Hello-World"
to_train("content-type")      → "Content-Type"
to_train("CONTENT_TYPE")      → "Content-Type"
to_train("x_custom_header")   → "X-Custom-Header"
to_train("getHTTPResponse")   → "Get-Http-Response"
```

---

### to_title

Converts text to Title Case with spaces.

```
to_title(text) → string
```

**Parameters:**

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `text` | string | yes | The text to convert |

**Returns:** String in Title Case format.

**Behavior:**

1. Split input into words (see Word Splitting)
2. Capitalize the first letter of each word, lowercase the rest
3. Join with space ` `

**Examples:**

```
to_title("helloWorld")        → "Hello World"
to_title("hello_world")       → "Hello World"
to_title("hello-world")       → "Hello World"
to_title("HELLO_WORLD")       → "Hello World"
to_title("getHTTPResponse")   → "Get Http Response"
to_title("user_id")           → "User Id"
```

---

### to_sentence

Converts text to Sentence case.

```
to_sentence(text) → string
```

**Parameters:**

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `text` | string | yes | The text to convert |

**Returns:** String in Sentence case format.

**Behavior:**

1. Split input into words (see Word Splitting)
2. Capitalize only the first letter of the first word
3. Lowercase all other letters
4. Join with space ` `

**Examples:**

```
to_sentence("helloWorld")        → "Hello world"
to_sentence("hello_world")       → "Hello world"
to_sentence("HELLO_WORLD")       → "Hello world"
to_sentence("getHTTPResponse")   → "Get http response"
to_sentence("userProfilePage")   → "User profile page"
```

---

### to_flat

Converts text to flatcase (all lowercase, no separators).

```
to_flat(text) → string
```

**Parameters:**

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `text` | string | yes | The text to convert |

**Returns:** String in flatcase format.

**Behavior:**

1. Split input into words (see Word Splitting)
2. Lowercase all words
3. Join with no separator

**Examples:**

```
to_flat("helloWorld")       → "helloworld"
to_flat("Hello_World")      → "helloworld"
to_flat("HELLO-WORLD")      → "helloworld"
to_flat("Hello World")      → "helloworld"
```

---

### to_upper_flat

Converts text to UPPERFLATCASE (all uppercase, no separators).

```
to_upper_flat(text) → string
```

**Parameters:**

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `text` | string | yes | The text to convert |

**Returns:** String in UPPERFLATCASE format.

**Behavior:**

1. Split input into words (see Word Splitting)
2. Uppercase all words
3. Join with no separator

**Examples:**

```
to_upper_flat("helloWorld")    → "HELLOWORLD"
to_upper_flat("Hello_World")   → "HELLOWORLD"
to_upper_flat("hello-world")   → "HELLOWORLD"
```

---

### detect

Detects the case convention of a string.

```
detect(text) → string | null
```

**Parameters:**

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `text` | string | yes | The text to analyze |

**Returns:** One of: `"camel"`, `"pascal"`, `"snake"`, `"screaming"`, `"kebab"`, `"train"`, `"title"`, `"sentence"`, `"flat"`, `"upper_flat"`, or `null` if undetectable.

**Detection Rules (in priority order):**

1. **screaming**: All uppercase, contains underscore → `"screaming"`
2. **snake**: All lowercase, contains underscore → `"snake"`
3. **train**: Contains hyphen, each segment starts with uppercase → `"train"`
4. **kebab**: All lowercase, contains hyphen → `"kebab"`
5. **title**: Contains space, each word starts with uppercase → `"title"`
6. **sentence**: Contains space, only first word starts with uppercase → `"sentence"`
7. **pascal**: No separators, starts with uppercase, has internal uppercase → `"pascal"`
8. **camel**: No separators, starts with lowercase, has internal uppercase → `"camel"`
9. **upper_flat**: All uppercase, no separators → `"upper_flat"`
10. **flat**: All lowercase, no separators → `"flat"`
11. Otherwise → `null`

**Examples:**

```
detect("helloWorld")       → "camel"
detect("HelloWorld")       → "pascal"
detect("hello_world")      → "snake"
detect("HELLO_WORLD")      → "screaming"
detect("hello-world")      → "kebab"
detect("Hello-World")      → "train"
detect("Hello World")      → "title"
detect("Hello world")      → "sentence"
detect("helloworld")       → "flat"
detect("HELLOWORLD")       → "upper_flat"
detect("hello")            → "flat"
detect("Hello")            → "pascal"
detect("HELLO")            → "upper_flat"
detect("hello World")      → null
detect("Hello_World")      → null
detect("")                 → null
detect("123")              → null
```

---

### split_words

Splits text into component words. This is the core utility used by all conversion functions.

```
split_words(text) → array of strings
```

**Parameters:**

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `text` | string | yes | The text to split |

**Returns:** Array of lowercase word strings.

**Examples:**

```
split_words("helloWorld")       → ["hello", "world"]
split_words("HelloWorld")       → ["hello", "world"]
split_words("hello_world")      → ["hello", "world"]
split_words("HELLO_WORLD")      → ["hello", "world"]
split_words("hello-world")      → ["hello", "world"]
split_words("Hello World")      → ["hello", "world"]
split_words("XMLParser")        → ["xml", "parser"]
split_words("getHTTPResponse")  → ["get", "http", "response"]
split_words("version2Release")  → ["version", "2", "release"]
split_words("iPhone")           → ["i", "phone"]
split_words("iOS")              → ["i", "os"]
split_words("")                 → []
```

---

## Word Splitting Algorithm

Word splitting is the core of case conversion. The algorithm must handle:
- Explicit delimiters (underscore, hyphen, space)
- Case transitions (lowercase→uppercase)
- Acronyms (consecutive uppercase)
- Numbers (digit sequences)

### Rules

**1. Split on explicit delimiters:**
- Underscore `_`
- Hyphen `-`
- Space ` `
- Multiple consecutive delimiters treated as single split

**2. Split on case transitions:**
- lowercase → UPPERCASE: split before the uppercase
  - `helloWorld` → `[hello, World]`
- UPPERCASE → lowercase (when preceded by uppercase): split before the last uppercase
  - `XMLParser` → `[XML, Parser]` → but normalized to `[xml, parser]`
  - `getHTTPResponse` → `[get, HTTP, Response]` → `[get, http, response]`

**3. Split on number boundaries:**
- letter → digit: split between
- digit → letter: split between
- `version2Release` → `[version, 2, release]`
- `v2API` → `[v, 2, API]` → `[v, 2, api]`
- Consecutive digits stay together: `test123abc` → `[test, 123, abc]`

**4. Normalize:**
- All words lowercase in the returned array
- Empty strings filtered out

### Acronym Handling

Acronyms (consecutive uppercase letters) require special handling:

| Input | Split Result | Rationale |
|-------|--------------|-----------|
| `XMLParser` | `[xml, parser]` | XML is acronym, Parser is word |
| `getHTTPResponse` | `[get, http, response]` | HTTP is acronym between words |
| `HTTPSConnection` | `[https, connection]` | HTTPS is acronym at start |
| `parseJSON` | `[parse, json]` | JSON is acronym at end |
| `IOError` | `[io, error]` | IO is short acronym |
| `USA` | `[usa]` | All-caps single word |

The rule: When uppercase letters are followed by a lowercase letter, split *before* the last uppercase.

```
XMLParser
^^^      ← consecutive uppercase
   ^     ← lowercase follows
  ^      ← split here: [XM][LParser] → no, that's wrong

Better: [XML][Parser] — split between acronym and following word
```

### Implementation Pseudocode

```
function split_words(text):
    if text is empty:
        return []
    
    words = []
    current_word = ""
    
    for each character c at index i:
        prev = character at i-1 (or null if i=0)
        next = character at i+1 (or null if at end)
        
        # Check if we should split before this character
        should_split = false
        
        if c is delimiter (space, underscore, hyphen):
            # End current word, don't include delimiter
            if current_word is not empty:
                words.append(current_word.lower())
                current_word = ""
            continue
        
        if prev exists:
            # lowercase → uppercase: split before
            if prev is lowercase and c is uppercase:
                should_split = true
            
            # uppercase → lowercase (with preceding uppercase): split before prev
            # This handles: XMLParser → [XML, Parser]
            if prev is uppercase and c is lowercase and len(current_word) > 1:
                # Move last char of current_word to new word
                last_char = current_word[-1]
                current_word = current_word[:-1]
                if current_word is not empty:
                    words.append(current_word.lower())
                current_word = last_char
                should_split = false  # already handled
            
            # letter ↔ digit transitions
            if (prev is letter and c is digit) or (prev is digit and c is letter):
                should_split = true
        
        if should_split and current_word is not empty:
            words.append(current_word.lower())
            current_word = ""
        
        current_word += c
    
    # Don't forget the last word
    if current_word is not empty:
        words.append(current_word.lower())
    
    return words
```

---

## Edge Cases

### Empty and Whitespace Input

```
to_camel("")           → ""
to_snake("   ")        → ""
to_kebab("\t\n")       → ""
split_words("")        → []
detect("")             → null
```

### Single Word

```
to_camel("hello")      → "hello"
to_pascal("hello")     → "Hello"
to_snake("hello")      → "hello"
to_kebab("HELLO")      → "hello"
detect("hello")        → "flat"
detect("Hello")        → "pascal"
detect("HELLO")        → "upper_flat"
```

### Numbers Only

```
to_camel("123")        → "123"
to_snake("123")        → "123"
detect("123")          → null
split_words("123")     → ["123"]
```

### Mixed Numbers and Letters

```
to_snake("test123")         → "test123"
to_snake("test123abc")      → "test_123_abc"
to_camel("user_id_1")       → "userId1"
to_pascal("v2_api")         → "V2Api"
split_words("abc123def456") → ["abc", "123", "def", "456"]
```

### Consecutive Delimiters

```
to_camel("hello__world")    → "helloWorld"
to_snake("hello--world")    → "hello_world"
to_kebab("hello  world")    → "hello-world"
split_words("a__b--c  d")   → ["a", "b", "c", "d"]
```

### Leading/Trailing Delimiters

```
to_camel("_hello_world_")   → "helloWorld"
to_snake("-hello-world-")   → "hello_world"
to_kebab(" hello world ")   → "hello-world"
```

### Single Letters

```
to_snake("a")               → "a"
to_camel("aB")              → "aB"
to_snake("aB")              → "a_b"
split_words("aBcD")         → ["a", "b", "c", "d"]
```

### Acronyms at Boundaries

```
to_snake("ID")              → "id"
to_snake("getID")           → "get_id"
to_snake("IDNumber")        → "id_number"
to_camel("html_parser")     → "htmlParser"
to_pascal("html_parser")    → "HtmlParser"
```

### Unicode Letters

```
to_snake("héllo_wörld")     → "héllo_wörld"
to_camel("café_latté")      → "caféLatté"
to_kebab("naïveMethod")     → "naïve-method"
```

Note: Case conversion respects Unicode case mappings where available.

---

## Error Handling

### Invalid Input Types

If `text` is not a string, implementations SHOULD either:
1. Convert to string (e.g., `123` → `"123"`)
2. Raise/throw a type error

The recommended approach is option 1 for maximum flexibility.

### Non-ASCII Characters

Non-ASCII letters should be preserved and case-converted using Unicode rules:
- `é` → `É` when uppercasing
- `Ñ` → `ñ` when lowercasing

Characters that don't have case variants are preserved as-is.

---

## Implementation Notes

### Language-Specific Conventions

Implementations should follow language conventions for:
- **Function naming:** `to_snake` vs `toSnake` vs `ToSnake`
- **Return types:** String, or optional/nullable for `detect`
- **Error handling:** Exceptions, Result types, or graceful defaults

### Recommended Function Names by Language

| Language | Style | Example |
|----------|-------|---------|
| Python | snake_case | `to_snake()`, `to_camel()` |
| Ruby | snake_case | `to_snake`, `to_camel` |
| JavaScript | camelCase | `toSnake()`, `toCamel()` |
| TypeScript | camelCase | `toSnake()`, `toCamel()` |
| Go | PascalCase | `ToSnake()`, `ToCamel()` |
| Rust | snake_case | `to_snake()`, `to_camel()` |
| PHP | camelCase or snake_case | `toSnake()` or `to_snake()` |
| Elixir | snake_case | `to_snake/1`, `to_camel/1` |
| Java | camelCase | `toSnake()`, `toCamel()` |
| C# | PascalCase | `ToSnake()`, `ToCamel()` |

### Performance Considerations

- Build regex patterns once, not per call
- For repeated conversions, consider caching word splits
- The algorithm is O(n) where n is string length

---

## Testing

All tests are defined in `tests.yaml`. The test file format:

```yaml
function_name:
  - description: "Human-readable description"
    input:
      text: "input string"
    expected: "expected-output"
```

For `split_words`, expected is an array:

```yaml
split_words:
  - description: "camelCase splitting"
    input:
      text: "helloWorld"
    expected: ["hello", "world"]
```

For `detect`, expected can be a string or null:

```yaml
detect:
  - description: "detects camelCase"
    input:
      text: "helloWorld"
    expected: "camel"
  
  - description: "undetectable mixed"
    input:
      text: "Hello_world"
    expected: null
```

### Test Generation Example (Python)

```python
import yaml

with open('tests.yaml') as f:
    tests = yaml.safe_load(f)

for func_name, cases in tests.items():
    for case in cases:
        test_name = case['description'].lower().replace(' ', '_')
        text = case['input']['text']
        expected = case['expected']
        
        if isinstance(expected, list):
            print(f'''
def test_{func_name}_{test_name}():
    assert {func_name}("{text}") == {expected}
''')
        elif expected is None:
            print(f'''
def test_{func_name}_{test_name}():
    assert {func_name}("{text}") is None
''')
        else:
            print(f'''
def test_{func_name}_{test_name}():
    assert {func_name}("{text}") == "{expected}"
''')
```

---

## Versioning

This specification follows semantic versioning:
- **MAJOR:** Breaking changes to function signatures or core behavior
- **MINOR:** New functions, new case types
- **PATCH:** Clarifications, typo fixes, additional test cases

---

## Changelog

### v0.1.0 (Initial Release)
- Ten conversion functions: to_camel, to_pascal, to_snake, to_screaming, to_kebab, to_train, to_title, to_sentence, to_flat, to_upper_flat
- Detection function: detect
- Utility function: split_words
- Acronym-aware word splitting
- Number boundary handling

---

## Future Considerations (Out of Scope for v0.1)

- Custom acronym preservation (keep "HTTP" as "HTTP" instead of "Http")
- Locale-aware titlecase (handling articles: "the", "a", "of")
- Additional case styles (dot.case, path/case)
- Bidirectional conversion hints
- Streaming/chunked processing for very long strings
