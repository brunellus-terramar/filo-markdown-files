# Code Examples in Markdown

This document demonstrates how code blocks and inline code are displayed.

## Inline Code

To install a package, run `npm install package-name` in your terminal.

The `print()` function is used to output text in Python.

## Code Blocks

Here's a simple Python function:

```python
def greet(name):
    """Return a greeting message."""
    return f"Hello, {name}! Welcome to Markdown Reader."

# Example usage
message = greet("World")
print(message)
```

And here's some JavaScript:

```javascript
function calculateSum(numbers) {
    return numbers.reduce((acc, num) => acc + num, 0);
}

const result = calculateSum([1, 2, 3, 4, 5]);
console.log(`The sum is: ${result}`);
```

## Swift Example

Since this is a macOS app, here's some Swift code:

```swift
import SwiftUI

struct ContentView: View {
    @State private var message = "Hello, World!"
    
    var body: some View {
        VStack {
            Text(message)
                .font(.largeTitle)
            
            Button("Change Message") {
                message = "You clicked the button!"
            }
        }
        .padding()
    }
}
```

## Shell Commands

Common terminal commands:

```bash
# List files in current directory
ls -la

# Change directory
cd ~/Documents

# Create a new directory
mkdir my_project

# View file contents
cat README.md
```

---

Code blocks help make technical documentation clear and readable.
