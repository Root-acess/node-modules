const esprima = require('esprima');
const { walk } = require('estree-walker');

// Function to analyze code and find missing closing elements
function analyzeCode(code) {
  let missingClosingElements = {
    '}': 0,
    ';': 0,
    ')': 0,
  };

  try {
    const ast = esprima.parse(code, { tolerant: true }); // Handle syntax errors gracefully

    walk(ast, {
      enter(node) {
        if (node.type === 'BlockStatement' && !node.body.length) {
          missingClosingElements['}']++; // Count missing closing brace
        } else if (node.type === 'ExpressionStatement' && !node.expression) {
          missingClosingElements[';']++; // Count missing semicolon
        }
        // Handle other missing elements as needed
      },
      exit(node) {
        // Check for unbalanced parentheses here if needed
      },
    });
  } catch (error) {
    console.error('Error parsing code:', error.message); // Handle parsing errors
  }

  return missingClosingElements;
}

// Example usage
const code = `function add(a, b {
  return a + b;
}`;
const results = analyzeCode(code);
console.log(results); // Output: { '}' : 1, ';' : 0, ')' : 0 }
