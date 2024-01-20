---
layout: post
title: The Art of Readable Code
description: A not so deep dive into the nuances of code readability and maintainability, examining the subjective nature of what makes code readable, weird programming languages and personal preferences

date: 2023-06-01 15:00:00 +0100
image: '/images/posts/coded-maze.png'
tags: [op-ed, blog, writing, tech, software]
featured: true
---

{:refdef: style="text-align: center;"}
![Disclaimer Title](/images/brand/content/disclaimer-top.png)
{: refdef}

{:refdef: style="text-align: center;"}
The opinions expressed here are my own, do not reflect the views of my organization, and should not be be attributed to or associated with my organization in any manner.
{: refdef}

{:refdef: style="text-align: center;"}
![Disclaimer Footer](/images/brand/content/disclaimer-bottom.png)
{: refdef}

## Maintainability

Code, files, and other source artifacts are often labeled as either _maintainable_ or _not maintainable_; but maintainability usually refers to the entire project – including sources, project structure, modules, integrations, tooling, and so forth. My understanding of maintainability boils down to answering this question:

### How easily can I <font color="#FAA">fix issues</font> and <font color="#FAA">add features</font> to this codebase?

While most projects are made up of fully functional code that effectively fulfills its intended purpose, having functional code does not directly result in a maintainable project.

> "Functional" means working, or being able to work (especially in reference to a machine, an organization, or a system).
>
> <cite>[Oxford Dictionary](https://www.oxfordlearnersdictionaries.com/definition/english/functional)</cite>

This can also be interpreted as _"meeting the minimum requirements"_. Experience shows us that even fully functional code can negatively impact an organization if it's poorly written. Making a project maintainable involves the proper application of established coding principles (such as [SOLID](https://en.wikipedia.org/wiki/SOLID), [DRY](https://en.wikipedia.org/wiki/Don't_repeat_yourself), [KISS](https://en.wikipedia.org/wiki/KISS_principle), [YAGNI](https://martinfowler.com/bliki/Yagni.html)), the skill to identify and improve poorly written code, and deeply focusing on aspects such as code readability, error handling, effective tooling, and (in some cases) embracing a test-driven development methodology.

Documentation helps, but often doesn't cover the complexity of maintaining large codebases. Improving a codebase through various quality metrics is key to having a maintainable project – not because these arbitrary metrics universally lead to great codebases, but because valuing codebase quality creates an engineering culture where everyone produces easily maintainable artifacts. In large codebases, engineers usually agree on whether the project is easily maintainable or not. Having a consensus makes the answer to the question posed above **more objective**. Not only that, but we know that a module/project is not in a good shape when we delay diving into issues for too long (without a real reason). 🙃

Thus, I am proposing that **maintainability** is a broader, more objective concept than **readability** – the two should not be confused.

{:refdef: style="text-align: center;"}
![Teamwork](/images/posts/team-work.png)
{: refdef}

-----

## Readability

We've explored maintainability as a distinct concept, to which readability contributes, though it's not the only factor. Now, let's address the following question:

### How easily can I <font color="#FAA">read</font> and <font color="#FAA">understand</font> this code?

To answer this, we dive into what makes code readable and what doesn't.

#### 🌎 &nbsp; Does readability depend on the programming language?

Consider this example:

```javascript
/**
 * Finds the middle item of an array.
 * 
 * @param {Array} arr - Where to look
 * @return {any} The middle item of the array; could be undefined
 */
function findMiddle(arr) {
  if (arr.length === 0) return undefined;

  let middle = Math.floor(arr.length / 2);
  if (arr.length % 2 === 0) {
    return arr[middle];
  } else {
    return arr[middle - 1];
  }
}
```

Regardless of your technical background, this code is generally considered readable. It's [JavaScript](https://jsfiddle.net/opet12q3), and if you find an issue, you're proving my point _(the linked snippet includes a fix)_. Now, compare it with this code, accomplishing a similar task:

```brainfuck
++++++++++[>+++++++>++++++++++>+++>+<<<<-]>++.>+.+++++++..+++.>>++++[-<--------<-------->>]<<[>[>+>+<<-]>>[<<+>>-]<<<-]>>.
```

This is [Brainfuck](https://esolangs.org/wiki/Brainfuck), a ~~weird~~ esoteric and Turing-complete language often used in puzzles. This example illustrates that readability is indeed influenced by the programming language used (for humans, at least).

#### 📊 &nbsp; Does readability depend on the artifact type?

Imagine you're building data stubs for testing. Consider this [CSV](https://en.wikipedia.org/wiki/Comma-separated_values) data:

```csv
id, name, address, hobbies, work_experience
1, Alice, "Berlin, Main St, Apt 101; Hamburg, Second St, Apt 202", "Skiing, Painting, Reading, Photography, Traveling", "Software Engineer at TechCorp (2015-2019), Senior Developer at DevInc (2019-2022)"
2, Bob, "Munich, Third St, House 5; Dresden, Fourth St, House 10", "Cycling, Cooking, Guitar, Hiking, Gaming", "Network Specialist at NetSolutions (2013-2018), IT Consultant at GlobalTech (2018-present)"
```

Now, view the same data in [YAML](https://yaml.org):

```yaml
- id: 1
  name: Alice
  addresses: 
    - Berlin, Main St, Apt 101
    - Hamburg, Second St, Apt 202
  hobbies: 
    - Skiing
    - Painting
    - Reading
    - Photography
    - Traveling
  work_experience:
    - position: Software Engineer
      company: TechCorp
      years: 2015-2019
    - position: Senior Developer
      company: DevInc
      years: 2019-2022

# And the same for Bob (trying to keep it vertically short)
```

The choice of format for your program or parsing library is yours. However, when it comes to **human** readability, it's clear that this significantly depends on our ability to read and visualize structured data.

#### **<font color="#F88">{ }</font>** &nbsp; Does readability depend on indentation, variable naming, or code structure?

Absolutely. Here's a [C++](https://cplusplus.com) example emphasizing these factors. First, the less organized version:

```cpp
int a(int b[]) {
int c;
if(sizeof(b)/sizeof(b[0]) % 2 == 0)
c=b[sizeof(b)/sizeof(b[0])/2 - 1];
else c = b[sizeof(b)/sizeof(b[0])/2];
return c;}
```

And now, the same function, written more clearly:

```cpp
int findMiddle(int arr[]) {
  int size = sizeof(arr) / sizeof(arr[0]);
  int middleIndex = size / 2;

  if (size % 2 == 0) {
    return arr[middleIndex - 1];
  } else {
    return arr[middleIndex];
  }
}
```

### The spectrum of readability

Numerous factors contribute to readability, and I've provided examples for some of them. You'll find many more in the recommended reading below, including meaningful and concise naming, proper formatting, commenting, self-documenting code, explainer comments, de-duplication, avoiding magic constants, removing unused code, and creating single-purpose functions. All these elements (and others) undoubtedly enhance readability.

Unlike maintainability, readability feels much more **<font color="#F88">subjective</font>**. It falls on the engineer's shoulders to _(attempt to)_ produce readable code, influenced by their experiences and personal coding style. It's a common experience to struggle with reading your own code after a few months… or to find difficulty in understanding a new code block, especially if it's in an unfamiliar language or formatted differently than what you're used to.

Thus, I am proposing that readability is largely **contingent upon the reader** – it is **not** an inherent, objective property of the code.

{:refdef: style="text-align: center;"}
![Sore Eye](/images/posts/sore-eye.png)
{: refdef}

-----

## The Balancing Act

While readability and maintainability share similarities – primarily in their **<font color="#F88">reliance on human capability</font>** to code and maintain – readability seems to be inherently more subjective. It leans more on the individual engineer's skills, choice of language, and many personal experiences. Even in ideal conditions, being able to fully comprehend code in large codebases poses a challenge. As a project expands and new members join, developers' familiarity with the codebase diminishes over time, highlighting the importance of **maintainability** for future contributions.

With this in mind, I currently view maintainability as a **<font color="#F88">reflection of a team's culture</font>**, while readability strikes me **<font color="#F88">more as an art than a skill</font>**. This perspective helps guide my decisions on which software development rules to implement or discard, and which ones should transition from the space of creative engineering to process management (or vice versa).

#### 🧐 &nbsp; Reality check

The subjective nature of readability makes discussions about it uncomfortable within teams, as it feels more personal. Often, if your code is seen as unreadable by your peers, it might signal a need for personal growth and skill enhancement in programming. On the other hand, if your code is consistently praised for its clarity and readability, there's a risk of over-emphasizing formatting and linting rules to the point where they hinder creativity and free thinking in the team. This isn't just limited to code; it can apply to team processes as well. We should try to **<font color="#F88">find a balance</font>**.

Here's one interesting observation from my experience. In the past I worked on a really large project that was mostly **readable** and also **maintainable**, yet incredibly difficult to fully comprehend. Understanding each function and class, reading the code, and building new features were easily manageable tasks – but the cognitive load was constantly intense. Trying to work around established maintenance frameworks often led to confusion, primarily due to the system's complexity.

Was this an enjoyable experience? Certainly not, but it was a worthwhile one. Food for thought. 🍎

Recommended resources:

  - 📜 &nbsp; [Code as Documentation](https://martinfowler.com/bliki/CodeAsDocumentation.html)
  - 📜 &nbsp; [Maintainable and Readable Code](https://medium.com/@thomassentre/how-to-write-maintainable-and-readable-code-d9876747c224)
  - 📜 &nbsp; [Why Readability is Important](https://thehosk.medium.com/why-code-readability-is-important-e0c228a238a)
  - 📜 &nbsp; [The Best Engineering Interview](https://quuxplusone.github.io/blog/2022/01/06/memcached-interview)
  - 👀 &nbsp; [On Readability and Maintainability](https://www.youtube.com/watch?v=qugPoGBEJeE)
  - 🎧📱📚 &nbsp; [Clean Code](https://a.co/d/gMkZZR8)

> The Art of Readable Code

{:refdef: style="text-align: center;"}
![Engineering](/images/posts/engineering.png)
{: refdef}
