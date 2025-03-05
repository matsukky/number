<div align="center">
    <h1 style="border-bottom: none">
        <img src="./icon.svg" width="150" height="150">
        <h1>Number</h1>
        <p>Lightweight, dependency-free library for get string from a number in multiple languages</p>
        <h4>English - French - Spanish - Italian - German - Japanese - Chinese - Arabic - Russian</h4>
    </h1>
</div>

A minimalist library that provides a comprehensive way to handle gender representation in various languages. Zero dependencies, tree-shakeable, and type-safe.

## Table of Contents

- [Installation](#installation)
- [Features](#features)
- [Usage](#usage)
  - [Basic Usage](#basic-usage)
  - [Localization](#localization)
  - [Custom Properties](#custom-properties)
  - [Capitalization](#capitalization)
- [API Reference](#api-reference)
- [Types](#types)

## Installation

```bash
npm install @matsukky/number
# or
yarn add @matsukky/number
# or
bun add @matsukky/number
```

## Features

- 🪶 Lightweight
- 📦 Zero dependencies
- 🌍 Support for multiple languages
- 🔠 Automatic capitalization
- 💪 Fully typed (TypeScript)

## Usage

### Basic Usage

```typescript
import gender from '@matsukky/number';

const female = gender('F');
console.log(female.genderName);    // "woman"
console.log(female.childTerm);     // "girl"
console.log(female.emoji);         // "🚺"

const male = gender('MALE');       // Alias support
console.log(male.genderName);      // "man"
console.log(male.colors.primary);  // "#1e90ff"

const neutral = gender('X');
console.log(neutral.genderName);   // "person"
```

### Localization

```typescript
import { locale, gender } from '@matsukky/number';

// Load French locale
await locale('fr');

const female = gender('F');
console.log(female.genderName);    // "femme"
console.log(female.childTerm);     // "fille"
```

### Custom Properties

```typescript
import gender from '@matsukky/gender';

// Definition of context-specific terms
const result = gender('F', {
  custom: {
    occupation: {
      F: "actress",
      M: "actor",
      X: "performer"
    },
    workplace: {
      F: "actresses' room",
      M: "actors' room",
      X: "performers' room"
    },
    award: {
      F: "best actress",
      M: "best actor",
      X: "best performance"
    }
  }
});

// Basic usage
console.log(result.occupation);     // "actress"
console.log(result.workplace);      // "actresses' room"

// Combination with standard properties
console.log(`${result.title} ${result.genderName}`);          // "Mrs woman"
console.log(`${result.occupation} ${result.objectPronoun}`);   // "actress her"

// Usage with capitalization
const capitalizedResult = gender('F', {
  capitalize: true,
  custom: {
    occupation: {
      F: "actress",
      M: "actor",
      X: "performer"
    }
  }
});

console.log(capitalizedResult.occupation);  // "Actress"
```

The `gender` function allows extending standard properties with custom terms while maintaining gender consistency. Each custom property must define a value for all three genders (F, M, X) to ensure inclusive usage.

### Capitalization

```typescript
import gender from '@matsukky/gender';

const result = gender('F', { capitalize: true });
console.log(result.genderName);    // "Woman"
console.log(result.childTerm);     // "Girl"
```

## API Reference

### gender(type, options)

```typescript
gender(type: AvalaibleGender, options?: {
  capitalize?: boolean;
  custom?: Record<string, Record<'F' | 'M' | 'X', string>>;
  language?: AvalaibleLanguage;
}): GenderData
```

### locale(language, define?)

```typescript
locale(language: AvalaibleLanguage, define?: boolean): Promise<GenderCollection>
```

## Types

### GenderData Properties

| Property                 | Description                    | Example (Female)    |
|-------------------------|--------------------------------|-------------------|
| emoji                   | Gender emoji                   | 🚺                |
| colors                  | Color palette object           | { rose, petal, bloom, blush, berry } |
| genderName              | Gender name                    | "woman"          |
| childTerm               | Term for child                 | "girl"           |
| adultTerm              | Term for adult                 | "woman"          |
| combined               | Mostly used in social media as pronouns | "she/her"
| subjectPronoun         | Subject pronoun               | "she"            |
| objectPronoun          | Object pronoun                | "her"            |
| indirectPronoun        | Indirect pronoun               | "her"            |
| possessiveAdjective    | Possessive adjective           | "her"            |
| reflexivePronoun       | Reflexive pronoun              | "herself"        |
| demonstrative          | Demonstrative pronoun          | "she"            |
| indeterminateArticle   | Indeterminate article          | "a"             |
| genderAdjective        | Gender adjective               | "female"         |
| pluralSubjectPronoun   | Plural subject pronoun         | "they"          |
| pluralPossessiveAdj    | Plural possessive adjective    | "their"         |
| title                  | Full honorific title           | "Mrs."          |
| shortTitle             | Short honorific title          | "Ms."           |

### Avalaible Gender Keys

| Role | Values                                    |
|------|-------------------------------------------|
| F    | F, ♀, WOMAN, GIRL, FEMALE, SHE, HER       |
| M    | M, H, ♂, MAN, MEN, BOY, MALE, HE, HIM     |
| X    | X, N, ⚧, NEUTRAL, HUMAN, THEY, THEM      |
