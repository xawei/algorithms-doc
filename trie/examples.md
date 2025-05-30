# Examples

## Implement Trie (Prefix Tree)
?> LeetCode: [208. Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/description/) `Medium`

- **Simplified Problem**: Implement a trie with insert, search, and startsWith operations.

- **Solution Approach**: Create a Trie node structure with children mapping and end-of-word flag. Implement the three required operations using tree traversal.

```pseudocode
TrieNode:
    children = map/array of TrieNode
    isEndOfWord = false

insert(word):
    node = root
    for char in word:
        if char not in node.children:
            node.children[char] = new TrieNode()
        node = node.children[char]
    node.isEndOfWord = true

search(word):
    node = root
    for char in word:
        if char not in node.children:
            return false
        node = node.children[char]
    return node.isEndOfWord
```

<!-- tabs:start -->
### **Go**
```go
type TrieNode struct {
    children    [26]*TrieNode
    isEndOfWord bool
}

type Trie struct {
    root *TrieNode
}

func Constructor() Trie {
    return Trie{
        root: &TrieNode{},
    }
}

func (this *Trie) Insert(word string) {
    node := this.root
    
    for _, char := range word {
        index := char - 'a'
        if node.children[index] == nil {
            node.children[index] = &TrieNode{}
        }
        node = node.children[index]
    }
    
    node.isEndOfWord = true
}

func (this *Trie) Search(word string) bool {
    node := this.root
    
    for _, char := range word {
        index := char - 'a'
        if node.children[index] == nil {
            return false
        }
        node = node.children[index]
    }
    
    return node.isEndOfWord
}

func (this *Trie) StartsWith(prefix string) bool {
    node := this.root
    
    for _, char := range prefix {
        index := char - 'a'
        if node.children[index] == nil {
            return false
        }
        node = node.children[index]
    }
    
    return true
}
```

### **Python**
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end_of_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        node = self.root
        
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        
        node.is_end_of_word = True

    def search(self, word: str) -> bool:
        node = self.root
        
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        
        return node.is_end_of_word

    def startsWith(self, prefix: str) -> bool:
        node = self.root
        
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
        
        return True
```
<!-- tabs:end -->

---

## Word Search II
?> LeetCode: [212. Word Search II](https://leetcode.com/problems/word-search-ii/description/) `Hard`

- **Simplified Problem**: Given an m x n board of characters and a list of strings words, return all words on the board.

- **Solution Approach**: Build a Trie from all words, then use DFS with backtracking to explore the board while following Trie paths.

<!-- tabs:start -->
### **Go**
```go
type TrieNode struct {
    children [26]*TrieNode
    word     string
}

func findWords(board [][]byte, words []string) []string {
    // Build Trie
    root := &TrieNode{}
    for _, word := range words {
        node := root
        for _, char := range word {
            index := char - 'a'
            if node.children[index] == nil {
                node.children[index] = &TrieNode{}
            }
            node = node.children[index]
        }
        node.word = word
    }
    
    result := []string{}
    rows, cols := len(board), len(board[0])
    
    var dfs func(int, int, *TrieNode)
    dfs = func(row, col int, node *TrieNode) {
        if row < 0 || row >= rows || col < 0 || col >= cols {
            return
        }
        
        char := board[row][col]
        if char == '#' {
            return
        }
        
        index := char - 'a'
        if node.children[index] == nil {
            return
        }
        
        node = node.children[index]
        if node.word != "" {
            result = append(result, node.word)
            node.word = "" // Avoid duplicates
        }
        
        // Mark as visited
        board[row][col] = '#'
        
        // Explore neighbors
        dfs(row+1, col, node)
        dfs(row-1, col, node)
        dfs(row, col+1, node)
        dfs(row, col-1, node)
        
        // Backtrack
        board[row][col] = char
    }
    
    for i := 0; i < rows; i++ {
        for j := 0; j < cols; j++ {
            dfs(i, j, root)
        }
    }
    
    return result
}
```

### **Python**
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.word = None

def findWords(board, words):
    # Build Trie
    root = TrieNode()
    for word in words:
        node = root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.word = word
    
    result = []
    rows, cols = len(board), len(board[0])
    
    def dfs(row, col, node):
        if row < 0 or row >= rows or col < 0 or col >= cols:
            return
        
        char = board[row][col]
        if char == '#' or char not in node.children:
            return
        
        node = node.children[char]
        if node.word:
            result.append(node.word)
            node.word = None  # Avoid duplicates
        
        # Mark as visited
        board[row][col] = '#'
        
        # Explore neighbors
        dfs(row + 1, col, node)
        dfs(row - 1, col, node)
        dfs(row, col + 1, node)
        dfs(row, col - 1, node)
        
        # Backtrack
        board[row][col] = char
    
    for i in range(rows):
        for j in range(cols):
            dfs(i, j, root)
    
    return result
```
<!-- tabs:end -->

---

## Design Add and Search Words Data Structure
?> LeetCode: [211. Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/description/) `Medium`

- **Simplified Problem**: Design a data structure that supports adding new words and finding if a string matches any previously added string. The search can include '.' which matches any letter.

- **Solution Approach**: Use Trie with DFS for wildcard search. When encountering '.', explore all possible children.

<!-- tabs:start -->
### **Go**
```go
type TrieNode struct {
    children    [26]*TrieNode
    isEndOfWord bool
}

type WordDictionary struct {
    root *TrieNode
}

func Constructor() WordDictionary {
    return WordDictionary{
        root: &TrieNode{},
    }
}

func (this *WordDictionary) AddWord(word string) {
    node := this.root
    
    for _, char := range word {
        index := char - 'a'
        if node.children[index] == nil {
            node.children[index] = &TrieNode{}
        }
        node = node.children[index]
    }
    
    node.isEndOfWord = true
}

func (this *WordDictionary) Search(word string) bool {
    return this.searchHelper(word, 0, this.root)
}

func (this *WordDictionary) searchHelper(word string, index int, node *TrieNode) bool {
    if index == len(word) {
        return node.isEndOfWord
    }
    
    char := word[index]
    
    if char == '.' {
        // Try all possible children
        for i := 0; i < 26; i++ {
            if node.children[i] != nil {
                if this.searchHelper(word, index+1, node.children[i]) {
                    return true
                }
            }
        }
        return false
    } else {
        // Normal character
        charIndex := char - 'a'
        if node.children[charIndex] == nil {
            return false
        }
        return this.searchHelper(word, index+1, node.children[charIndex])
    }
}
```

### **Python**
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end_of_word = False

class WordDictionary:
    def __init__(self):
        self.root = TrieNode()

    def addWord(self, word: str) -> None:
        node = self.root
        
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        
        node.is_end_of_word = True

    def search(self, word: str) -> bool:
        return self._search_helper(word, 0, self.root)
    
    def _search_helper(self, word: str, index: int, node: TrieNode) -> bool:
        if index == len(word):
            return node.is_end_of_word
        
        char = word[index]
        
        if char == '.':
            # Try all possible children
            for child in node.children.values():
                if self._search_helper(word, index + 1, child):
                    return True
            return False
        else:
            # Normal character
            if char not in node.children:
                return False
            return self._search_helper(word, index + 1, node.children[char])
```
<!-- tabs:end -->

---

## Word Break
?> LeetCode: [139. Word Break](https://leetcode.com/problems/word-break/description/) `Medium`

- **Simplified Problem**: Given a string s and a dictionary of strings wordDict, return true if s can be segmented into a space-separated sequence of one or more dictionary words.

- **Solution Approach**: Build a Trie from dictionary words, then use DP with Trie to check all possible word breaks efficiently.

<!-- tabs:start -->
### **Go**
```go
type TrieNode struct {
    children    [26]*TrieNode
    isEndOfWord bool
}

func wordBreak(s string, wordDict []string) bool {
    // Build Trie
    root := &TrieNode{}
    for _, word := range wordDict {
        node := root
        for _, char := range word {
            index := char - 'a'
            if node.children[index] == nil {
                node.children[index] = &TrieNode{}
            }
            node = node.children[index]
        }
        node.isEndOfWord = true
    }
    
    n := len(s)
    dp := make([]bool, n+1)
    dp[0] = true
    
    for i := 1; i <= n; i++ {
        node := root
        for j := i - 1; j >= 0; j-- {
            index := s[j] - 'a'
            if node.children[index] == nil {
                break
            }
            node = node.children[index]
            
            if node.isEndOfWord && dp[j] {
                dp[i] = true
                break
            }
        }
    }
    
    return dp[n]
}
```

### **Python**
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end_of_word = False

def wordBreak(s, wordDict):
    # Build Trie
    root = TrieNode()
    for word in wordDict:
        node = root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end_of_word = True
    
    n = len(s)
    dp = [False] * (n + 1)
    dp[0] = True
    
    for i in range(1, n + 1):
        node = root
        for j in range(i - 1, -1, -1):
            char = s[j]
            if char not in node.children:
                break
            node = node.children[char]
            
            if node.is_end_of_word and dp[j]:
                dp[i] = True
                break
    
    return dp[n]
```
<!-- tabs:end --> 