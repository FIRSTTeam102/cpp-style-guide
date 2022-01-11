# Introduction
This guide lists C++ coding conventions/recommendations for use with WPILib-based robot programming.

This guide is based on [GeoSoft's](https://geosoft.no/development/cppstyle.html), [WPILib's](https://github.com/wpilibsuite/styleguide/blob/main/cppguide.html), and conventions previously used in our code.

## Layout
Conventions are grouped by topic, and each convention is numbered to make it easier to refer to.

Conventions are written using this layout:
<h4>n. Short description</h4>

`Example (if available)`

Longer description and reasoning

## "Importance" terms
The terms *must*, *should*, and *can* have special meaning. A *must* requirement must be followed, a *should* is a strong recommendation, and a *can* is a general guideline.

## Common terms
These non-C++ terms will commonly be used throughout the guide:
* __camelCase__: naming convention where the first letter of each word in a compound word is capitalized, except for the first word
* __PascalCase__: naming convention where the first letter of each word in a compound word is capitalized, including the first word

# General
#### 1. Any violation to the guide is allowed if it enhances readability.
The main goal of the recommendations is to improve readability, which increases the maintanibility and quality of the code. Every specific case will not be listed, so use your own discretion. If you think something should look different as it is easier to read, then make it look different.

# Naming conventions
#### 2. Class or enum names must be in PascalCase.
`Indexer`, `DriveLikeACar`

#### 3. Variable names must be in camelCase.
`speed`, `turnRadius`

Makes variables easy to distinguish from types.

##### 3a. Constants must be prefixed with `k`.
`kMode`, `kTurnSpeed`

##### 3b. Member variables must be prefixed with `m`.
`mSpeed`, `mDriveLeft`

##### 3c. Pointer variables should also be prefixed with `p`.
`pDriveTrain`, `mpDriveTrain`

If a member variable is also a pointer, then it should be labeled as both (`mp`)

#### 4. Method or function names must be written in camelCase and should be verbs.
`getSpeed()`, `drive()`

##### 4a. WPILib-defined methods must be written in PascalCase.
`Initialize`, `Execute`, `End`, `IsFinished`

#### 5. Variables with a large scope should have long names, variables with a small scope can have short names.
Scratch variables used for temporary storage or indices and are best kept short. (like `i` in a loop) A programmer reading it should be able to assume that its value is not used outside of a few lines of code.
