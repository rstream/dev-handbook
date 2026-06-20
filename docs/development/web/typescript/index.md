# TypeScript development

[← back](../../../index.md)

TypeScript is JavaScript with static types. This section skips JavaScript basics and focuses on TypeScript-specific syntax, config, and common project behavior.

## Project setup

[tsconfig basics](config/tsconfig-basics.md) - purpose of `tsconfig.json`, `tsc`, `noEmit`, `include`, `exclude`  
[Config file scope](config/tsconfig-files-scope.md) - which files belong to a project and how TypeScript finds configs  
[Extends and merging](config/tsconfig-extends-merge.md) - how `extends` works, what is replaced, what is inherited  
[Compiler options](config/tsconfig-compiler-options.md) - common options and their practical effect  
[Modules](config/tsconfig-modules.md) - `module`, `moduleResolution`, ESM, CommonJS, bundler mode  
[JSX](config/tsconfig-jsx.md) - JSX settings for React/Preact-style projects  
[Build output](config/tsconfig-build-output.md) - `outDir`, `rootDir`, source maps, declaration output  
[Strictness](config/tsconfig-strictness.md) - `strict` and related checks worth enabling  
[Paths](config/tsconfig-paths.md) - `baseUrl`, `paths`, aliases, and runtime caveats  

## Language

[Type annotations](language/type-annotations.md) - where types are written and where inference is enough  
[Primitive and special types](language/primitive-and-special-types.md) - `string`, `number`, `unknown`, `never`, `any`, `void`  
[Objects, arrays, tuples](language/objects-arrays-tuples.md) - object shapes, optional fields, readonly, arrays, tuples  
[Unions and intersections](language/unions-intersections.md) - `A | B`, `A & B`, literals, discriminated unions  
[Type narrowing](language/type-narrowing.md) - `typeof`, `in`, equality checks, predicates, control flow  
[Interfaces and type aliases](language/interfaces-and-type-aliases.md) - when to use each and how extension works  
[Functions](language/functions.md) - parameter types, return types, overloads, callbacks  
[Classes](language/classes.md) - class fields, access modifiers, implements, abstract classes  
[Generics](language/generics.md) - type parameters, constraints, defaults, inference  
[Utility types](language/utility-types.md) - `Partial`, `Pick`, `Omit`, `Record`, `ReturnType`, etc.  
[Modules and types](language/modules-and-types.md) - type-only imports/exports and module typing patterns  
[Declaration files](language/declaration-files.md) - `.d.ts`, ambient declarations, typing untyped libraries  
