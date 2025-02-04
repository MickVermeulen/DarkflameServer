# Contributing to Darkflame Universe

This document outlines how to contribute to Darkflame Universe as well as guidelines and rules for contribution.

## Filing Issues

Issues should be used to report problems with the project, request a new feature, or to discuss potential changes before a PR is created.

If you find an Issue that addresses the problem you're having, please add your own reproduction information to the existing issue rather than creating a new one.

Issues should include (when applicable):
- Expected Behavior
- Current Behavior
- Possible Solution
- Steps to Reproduce
- Your Enviorment

## Pull Requests

PRs to this project are always welcome and can be a quick way to get your fix or improvement slated for the next release. In general, PRs should:

- Only fix/add the functionality in question **OR** address wide-spread whitespace/style issues, not both.
- Address a single concern in the least number of changed lines as possible.
- Include documentation in the repo.

For changes that address core functionality or would require breaking changes (e.g. a major release), it's best to open an Issue to discuss your proposal first. This is not required but can save time creating and reviewing changes.

In general, we follow the "fork-and-pull" Git workflow

- Fork the repository to your own Github account
- Clone the project to your machine
- Create a branch locally with a succinct but descriptive name
- Commit changes to the branch
- Following any formatting and testing guidelines specific to this repo
- Push changes to your fork
- Open a PR in our repository.

PRs should include (when applicable):
- Description
- Motivation and Context
- Type of Changes
- How Has This Been Tested?
- Screenshots

## Development Resources

Check out a compiled list of development resources and tools [here](https://lu-dev.net/).

## Coding Style

This project has gone through multiple iterations of coding style. In the code you'll find a number of different coding styles in use. What follows is the preferred style for this project.

### General

**Never** use spaces instead of tabs. 1 Tab = 4 space character's width by default.

Use typically trailing braces everywhere (if, else, functions, structures, typedefs, class definitions, etc.)

```cpp
if (x) {
}
```

The else statement starts on the same line as the last closing brace.

```cpp
if (x) {
} else {
}
```


Do not pad parenthesized expressions with spaces

```cpp
if (x) {
}
```

Instead of 

```cpp
if ( x ) {
}
```

And

```cpp
x = (y * 0.5f);
```

Instead of

```cpp
x = ( y * 0.5f );
```


Use precision specification for floating point values unless there is an explicit need for a double.

```cpp
float f = 0.5f;
```

Instead of

```cpp
float f = 0.5;
```

And

```cpp
float f = 1.0f;
```

Instead of

```cpp
float f = 1.f;
```


Function names start with an upper case:

```cpp
void Function();
```


In multi-word function names each word starts with an upper case:

```cpp
void ThisFunctionDoesSomething();
```


The standard header for functions is:

```cpp
/**
 * Function description
 * @param param1 Description of param1
 * @return Description of return value
 */
```


Variable names start with a lower case character.

```cpp
float x;
```


In multi-word variable names the first word starts with a lower case character and each successive word starts with an upper case.

```cpp
float maxDistanceFromPlane;
```


Typedef names use the same naming convention as variables, however they always end with `_t`.

```cpp
typedef int fileHandle_t;
```

Do not use C style enums, instead use enum classes.

```cpp
enum class Contact {
	None,
	Edge,
	ModelVertex
};
```

Instead of

```cpp
enum Contact {
	CONTACT_NONE,
	CONTACT_EDGE,
	CONTACT_MODELVERTEX,
	CONTACT_TRMVERTEX
};
```

Never use ambiguous integer types.

```cpp
uint16_t myInteger = 0;
```

Instead of

```cpp
unsigned short myInteger = 0;
```

Defined names use all upper case characters. Multiple words are separated with an underscore.

```cpp
#define SIDE_FRONT		0
```


Use `const` as much as possible.

Use:

```cpp
const int* p;			// pointer to const int
int* const p;			// const pointer to int
const int* const p;		// const pointer to const int
```

Don’t use:

```cpp
int const* p;
```


### Classes

The standard header for a class is:

```cpp
/**
 * Class description
 */
```


Class names should not start with a prefix and each successive word starts with an upper case.

```cpp
class Vec3;
```


Class variables start with `m` and each successive word starts with an upper case.

```cpp
class Vec3 {
	float m_X;
	float m_Y;
	float m_Z;
}
```

Class methods have the same naming convention as functions.

```cpp
class Vec3 {
	float Length() const;
}
```

Ordering of class variables and methods should be as follows:

1.	constructor and destructor (followed by a line break)
2.	list of friend classes
3.	public variables
4.	public methods
5.	protected variables
6.	protected methods
7.	private variables
8.	private methods

This allows the public interface to be easily found at the beginning of the class.


Always make class methods `const` when they do not modify any class variables.

Avoid use of `const_cast`.  When object is needed to be modified, but only const versions are accessible, create a function that clearly gives an editable version of the object.  This keeps the control of the "const-ness" in the hands of the object and not the user.

Return `const` objects unless the general usage of the object is to change its state.

Function overloading should be used in most cases. For example, instead of:

```cpp
	const Anim*	GetAnimByIndex(int index) const;
	const Anim*	GetAnimByName(const char* name) const;
	const Anim*	GetRandomAnim(float randomDiversity) const;
```

Use:
```cpp
	const Anim*	GetAnim(int index) const;
	const Anim*	GetAnim(const char* name) const;
	const Anim*	GetAnim(float randomDiversity) const;
```


### Header Files

At the beginning of all header files, there should be a `#pragma once` to prevent circular includes.


Ordering of includes should be as follows, with each section getting a line break:

1.	relevant header file (example: `Vec3.h` for `Vec3.cpp`)
2.	c system headers (use angle brackets)
3.	c++ standard library headers (use angle brackets)
4.	third party library headers
5.	internal headers

For example, `Vec3.cpp`'s includes may look like:

```cpp
#include "Vec3.h"

#include <math.h>

#include <cstdint>
#include <vector>

#include "BitStream.h"

#include "dCommonVars.h"
```


Use forward declarations to your advantage, they decrease compile time.

Use:

```cpp
class Vec3;

class Player {
	Vec3 m_Position;
}
```

Don't use:

```cpp
#include "Vec3.h"

class Player {
	Vec3 m_Position;
}
```


### File Names

Each class should be in a separate source file unless it makes sense to group several smaller classes.
All source files should use the `.cpp` extension and all header files should use the `.h` extension.
The file name can be the same as the name of the class.

```cpp
class Winding;
```

files:

```
Winding.cpp
Winding.h
```
