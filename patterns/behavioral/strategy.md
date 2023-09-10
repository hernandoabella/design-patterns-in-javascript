### Strategy

Allows selecting one of the algorithms in certain situations.

The strategy pattern is a behavioral software design pattern that allows selecting an algorithm at runtime. Instead of implementing a single algorithm directly, the code receives instructions at runtime on which one to use from a family of algorithms.

**Example:**

Let's take an example where we have a text processor that will display data based on the chosen strategy (HTML or Markdown).

The strategy design pattern allows selecting an algorithm at runtime. Here's the example step by step:

**1. Definition of Output Formats:** An OutputFormat object is defined that lists the available output formats, in this case, Markdown and HTML.

**2. Abstract Strategy Class `ListStrategy`:** An abstract class called `ListStrategy` is created, which defines abstract methods `start`, `end`, and `addListItem`. These methods will be implemented by specific strategies.

```
class ListStrategy {
  start(buffer) {}
  end(buffer) {}
  addListItem(buffer, item) {}
}
```

**3. Specific List Strategies:** Two classes are created that inherit from ListStrategy to implement specific strategies: MarkdownListStrategy and HTMLListStrategy. Each one implements the abstract methods of the base strategy according to its specific format.

```
class MarkdownListStrategy extends ListStrategy {
  addListItem(buffer, item) {
    buffer.push(` * ${item}`);
  }
}

class HTMLListStrategy extends ListStrategy {
  start(buffer) {
    buffer.push("<ul>");
  }

  end(buffer) {
    buffer.push("</ul>");
  }

  addListItem(buffer, item) {
    buffer.push(` <li>${item}</li>`);
  }
}

```

**4. TextProcessor Class:** A TextProcessor class is created that accepts an output format and uses a specific list strategy based on the selected format.

```
class TextProcessor {
  constructor(outputFormat) {
    this.buffer = [];
    this.setFormat(outputFormat);
  }

  setFormat(format) {
    switch (format) {
      case OutputFormat.markdown:
        this.listStrategy = new MarkdownListStrategy();
        break;
      case OutputFormat.html:
        this.listStrategy = new HTMLListStrategy();
        break;
    }
  }

  appendList(items) {
    this.listStrategy.start(this.buffer);
    for (let item of items) {
      this.listStrategy.addListItem(this.buffer, item);
    }
    this.listStrategy.end(this.buffer);
  }

  clear() {
    this.buffer = [];
  }

  toString() {
    return this.buffer.join("\n");
  }
}
```

**5. Using the Text Processor:** An instance of TextProcessor is created, the output format is set, and a list is added. Then, the result is displayed.

```
let textProcessor = new TextProcessor();

textProcessor.setFormat(OutputFormat.markdown);
textProcessor.appendList(["one", "two", "three"]);
console.log(textProcessor.toString());

textProcessor.clear();
textProcessor.setFormat(OutputFormat.html);
textProcessor.appendList(["one", "two", "three"]);
console.log(textProcessor.toString());
```

**Final Code:**

```
// Enumeration of output formats
let OutputFormat = Object.freeze({
  markdown: 0,
  html: 1,
});

// Abstract class ListStrategy
class ListStrategy {
  start(buffer) {}
  end(buffer) {}
  addListItem(buffer, item) {}
}

// Specific strategy for Markdown format
class MarkdownListStrategy extends ListStrategy {
  addListItem(buffer, item) {
    buffer.push(` * ${item}`);
  }
}

// Specific strategy for HTML format
class HTMLListStrategy extends ListStrategy {
  start(buffer) {
    buffer.push("<ul>");
  }

  end(buffer) {
    buffer.push("</ul>");
  }

  addListItem(buffer, item) {
    buffer.push(` <li>${item}</li>`);
  }
}

// TextProcessor class
class TextProcessor {
  constructor(outputFormat) {
    this.buffer = [];
    this.setFormat(outputFormat);
  }

  setFormat(format) {
    switch (format) {
      case OutputFormat.markdown:
        this.listStrategy = new MarkdownListStrategy();
        break;
      case OutputFormat.html:
        this.listStrategy = new HTMLListStrategy();
        break;
    }
  }

  appendList(items) {
    this.listStrategy.start(this.buffer);
    for (let item of items) {
      this.listStrategy.addListItem(this.buffer, item);
    }
    this.listStrategy.end(this.buffer);
  }

  clear() {
    this.buffer = [];
  }

  toString() {
    return this.buffer.join("\n");
  }
}

// Create an instance of the text processor
let textProcessor = new TextProcessor();

// Set the output format to Markdown
textProcessor.setFormat(OutputFormat.markdown);

// Append a list of items
textProcessor.appendList(["one", "two", "three"]);

// Display the output in Markdown format
console.log("Markdown Format Output:");
console.log(textProcessor.toString());

// Clear the text processor
textProcessor.clear();

// Set the output format to HTML
textProcessor.setFormat(OutputFormat.html);

// Append a list of items
textProcessor.appendList(["one", "two", "three"]);

// Display the output in HTML format
console.log("\nHTML Format Output:");
console.log(textProcessor.toString());
```

**Salida esperada en formato HTML:**

```
<ul>
 <li>one</li>
 <li>two</li>
 <li>three</li>
</ul>
```

This code demonstrates how different output format strategies (Markdown and HTML) can be easily switched at runtime using the strategy design pattern.
