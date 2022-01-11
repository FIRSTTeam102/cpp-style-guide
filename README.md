# Introduction
This guide lists C++ coding conventions/recommendations for use with WPILib-based robot programming. It is based on [GeoSoft's](https://geosoft.no/development/cppstyle.html), [WPILib's](https://github.com/wpilibsuite/styleguide/blob/main/cppguide.html), and conventions previously used in our code.

## Layout
Conventions are grouped by topic, and each convention has an ID to make it easier to refer to. They are written using this layout:

**S#. Short description**

`Example (if available)`

Longer description and reasoning

## "Importance" terms
The terms *must*, *should*, and *can* have special meaning. A *must* requirement must be followed, a *should* is a strong recommendation, and a *can* is a general guideline.

## Common terms
These non-C++ terms will commonly be used throughout the guide:
* __camelCase__: naming convention where the first letter of each word in a compound word is capitalized, except for the first word
* __PascalCase__: naming convention where the first letter of each word in a compound word is capitalized, including the first word

# General
#### G1. Any violation to the guide is allowed if it enhances readability.
The goal of these conventions is to improve readability, which increases the maintanibility and quality of our code. Every specific case will not be listed, so use your own discretion. If you think something should look different as it is easier to read, then make it look different.

# Naming conventions
This section derermines how things should be named inside of code.

#### N1. Class or enum names must be in PascalCase.
`Indexer`, `DriveLikeACar`

#### N2. Variable names must be in camelCase.
`speed`, `turnRadius`

Makes variables easy to distinguish from types.

##### N2a. Constants must be prefixed with `k`.
`kMode`, `kTurnSpeed`

##### N2b. Member variables must be prefixed with `m`.
`mSpeed`, `mDriveLeft`

##### N2c. Pointer variables should also be prefixed with `p`.
`pDriveTrain`, `mpDriveTrain`

If a member variable is also a pointer, then it should be labeled as both (`mp`)

#### N3. Method or function names must be written in camelCase and should be verbs.
`getSpeed()`, `drive()`

This excludes `Initialize`, `Execute`, `End`, and `IsFinished`.

#### N4. Variables with a large scope should have long names, variables with a small scope can have short names.
Scratch variables used for temporary storage or indices and are best kept short. (like `i` in a loop) A programmer reading it should be able to assume that its value is not used outside of a few lines of code.

# Files
This section determines how files should be organized.

#### F1. A class should be declared in a header file and defined in a source file, where the name of the files match the name of the class.
`MyClass.h` declares the class, `MyClass.cpp` defines the class, and `MyClass` is the name of the class

#### F2. Commands should be grouped into folders based on their subsystem.
`commands/intake/LowerIntake`, `commands/intake/RaiseIntake`, `commands/shooter/StopShooter`

This keeps related files together and the commands folder unclutered.

#### F3. Simple methods (like getters) that are less than 3 lines should be defined in the header file.

# Layout
This desction determines how code should be formatted.

#### L1. Basic indentation should be one TAB. (not spaces)
```cpp
void Shooter::toggleServo() {
	if (mHoodIn) {
		extendServo();
	} else {
		retractServo();
	}
	mHoodIn = !mHoodIn;
}
```
Indentation is used to emphasize the logical structure of the code. Tabs are standardized, more efficent, and can be configured to display at any chosen width.

#### L2. Write minimal but sufficient comments.
The use of comments should be minimized by making the code self-documenting, like appropriate naming and an explicit logical structure. However, the code can only tell a reader how the code words and not what it is supposed to do.

#### L3. Block layout must be used. Opening curly brackets must be on the same line as the statement.
```cpp
if (condition) {
	// ...
} else {
	// ...
}
```

#### L4. Conditionals with a single statement should be written on one line and without brackets, if it enhances readability.
```cpp
if (condition) doSomething();
```
This makes it clear that the single statement is the only one in the conditional.

#### L5. Operators should be surrounded by a space character, excluding pointer and member operators. Commas, C++ reserved words, single-line comments, colons, and inline semicolons must be followed by a white space. Opening/closing parenthesis must not have a space after/before.
```cpp
a = (b + c) * d;
doSomething(a, b, c, d);
if (condition) {}
for (i = 0; i < 10; i++) {}
// Comment
pObject = *object;
object.a = 2;
b = pObject->b;
```

#### L6. Logical units within a block should be separated by one blank line.
```cpp
std::shared_ptr<NetworkTable> table = nt::NetworkTableInstance::GetDefault().GetTable("limelight");

double x = table->GetNumber("tx", 0.0);
double y = table->GetNumber("ty", 0.0);
double v = table->GetNumber("tv", 0.0);

// Aim only if a target is found
if (tv != 0.0) aimTarget(x, y);
```
A logical unit is a set of lines of code that fit together logically and contextually. Small units of code can make sense by themselves, but combining them with surrounding code can make it confusing to read. This also allows you to clearly have a comment for a specific unit.

#### L7. Include statements must be at the top of the file. Library includes should use angled brackets and project file includes should use quotes. Include statements within groups should be sorted alphabetically. Inlude statements should be placed in the below order:
```cpp
// Related header file
#include "subsystems/Shooter.h"

// C++ libraries
#include <cmath.h>

// Other libraries
#include <ctre/Phoenix.h>
#include <frc/Encoder.h>

// Additional project files
#include "Constants.h"
#include "subsystems/Indexer.h"
```
