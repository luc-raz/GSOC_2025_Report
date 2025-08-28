# GSoC 2025 Final Report: Optimizing the Pharo Compiler with bytecode-level Inlining

**Name:** Andry RAZAFINDRAINIBE Radoniaina Lucio  
**Organization:** Pharo Consortium  
**Mentor(s):** [Nahuel Palumbo](https://github.com/PalumboN)
**Keywords:** Compiler, Optimization, DRUID, Pharo, Block Closure, Inlining

---

## Context

Pharo is a dynamic, purely object-oriented programming language, widely used both in research and in industry. Its compilation infrastructure currently provides limited optimizations, which motivates the development of **DRUID**, an optimizing compiler for Pharo.  

The original motivation behind DRUID is to enable advanced optimizations on Pharo programs, with a particular focus on **bytecode-level inlining**. This optimization is especially relevant in Pharo, where message sending is pervasive and has a strong impact on runtime efficiency.  

However, in order to implement inlining and other advanced optimizations, DRUID first needs to support all major language constructs.   A key missing feature was the **support for blocks**, which are a fundamental part of Pharo’s syntax and semantics. Blocks are used to implement control structures: loop and conditions, and without them DRUID could not handle a significant portion of real-world Pharo code.  

During this GSoC, my work focused on **extending DRUID with block support**.  
This contribution lays the foundation for further optimizations — including inlining — by making DRUID capable of compiling realistic Pharo programs while preserving their semantics.  


---

## Contributions

### Implemented Features
- Extend DRUID’s **Intermediate Representation (IR)** to better model blocks.
- Handle correctly **local and non-local returns** inside blocks
- Support for **capturing lexical environments**, including nested blocks.
- Added a dedicated **test suite** to validate block compilation and execution.
- **Ensure integration** of blocks into DRUID’s existing optimization passes.

### Pull Requests

| PR Number | Description                                   | Issue Fixed |
|-----------|-----------------------------------------------|-------------|
| [#192](https://github.com/Alamvic/druid/pull/192) | - Handle local and non-local return <br>- Using TempVector to share variables      | [#183 Compile simple methods using one TempVector always](https://github.com/Alamvic/druid/issues/183) <br> [#186 Compile Blocks using Druid](https://github.com/Alamvic/druid/issues/186)|
| [#194](https://github.com/Alamvic/druid/pull/194) | Support nested blocks (by creating a scope) | [#193 Add scopes to the CFG](https://github.com/Alamvic/druid/issues/193) |
| [#201](https://github.com/Alamvic/druid/pull/201) | Make optimisations(inlining) work with block compilation| [#199 Errors with DRBytecodeGenerator](https://github.com/Alamvic/druid/issues/199) <br> [#200 Variable not in scope when inlining method](https://github.com/Alamvic/druid/issues/200) |



### Other Contributions
- [PR #176:](https://github.com/Alamvic/druid/pull/176): Improve testing on some optimisations: DRDeadCodeElimination, DRCopyPropagation, DRFrameInfoCleaner
- [PR #178:](https://github.com/Alamvic/druid/pull/178) Optimization InstVar
  Related to [Issue #174](https://github.com/Alamvic/druid/issues/174).
- [PR #178:](https://github.com/Alamvic/druid/pull/207) Add Support for Literal Variables (Not Merged)
  Related to: 
  - [Issue #201](https://github.com/Alamvic/druid/issues/201) Support Class Variables.
  - [Issue #202](https://github.com/Alamvic/druid/issues/202) Support Literal Nodes.



---

## Future Work

- Implement optimizations to **select which variables should be stored in the TempVector** and passed to blocks.
- Extend DRUID with **more language features** to support the full Pharo language, moving closer to the original long-term goal of a complete optimizing compiler.  


---

## Links

- [Landed PRs](https://github.com/Alamvic/druid/pulls?q=is%3Apr+author%3Aluc-raz)
- [DRUID repository](https://github.com/Alamvic/druid)  
- [GSoC project](https://summerofcode.withgoogle.com/programs/2025/projects/ZAqo1UGN)  
- [Pharo website](https://pharo.org/) 

---

Thanks to the Pharo community and my mentors for their guidance and support throughout GSoC 2025!

