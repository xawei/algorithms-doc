# Trie (Prefix Tree)

A **Trie**, also known as a **Prefix Tree**, is a specialized tree data structure that excels at storing and searching for **strings** with shared prefixes. Each node in a Trie represents a single character, and paths from the root to leaves represent complete words. This structure makes Trie incredibly efficient for **prefix-based operations**, **autocomplete features**, and **word validation**.

## When to Use Trie

Trie is ideal for problems where you need to:

- **Prefix matching**: Finding all words that start with a given prefix.
- **Autocomplete**: Implementing search suggestions or word predictions.
- **Word validation**: Checking if a word exists in a dictionary.
- **Pattern matching**: Searching for words with wildcards or patterns.
- **IP routing**: Network routing tables use Trie-like structures.

## Why Use Trie?

- **Efficient prefix operations**: O(m) for search/insert where m is word length.
- **Space optimization**: Shared prefixes are stored only once.
- **Fast word enumeration**: Easy to find all words with a common prefix.
- **No hash collisions**: Unlike hash tables, Trie has predictable performance.
- **Ordered traversal**: Can retrieve words in lexicographical order.

## Key Concepts

### Trie Node Structure
- **Character storage**: Each node represents one character
- **Children mapping**: Usually an array/map of child nodes
- **End marker**: Flag indicating if this node ends a valid word
- **Optional data**: Additional information like word count or definitions

### Common Operations
- **Insert**: Add a word to the Trie (O(m))
- **Search**: Check if word exists (O(m))
- **StartsWith**: Check if any word has given prefix (O(m))
- **Delete**: Remove a word from Trie (O(m))
- **Traverse**: Visit all words with given prefix

## Common Use Cases

1. **Autocomplete Systems**: Search engines, IDE code completion.
2. **Spell Checkers**: Validating words against dictionaries.
3. **IP Routing**: Network routing tables for longest prefix matching.
4. **Word Games**: Boggle, Scrabble word validation.
5. **Search Suggestions**: Real-time search recommendations. 