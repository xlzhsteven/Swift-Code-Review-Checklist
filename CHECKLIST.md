# iOS Code Submittion Checklist
## 1 - Static Code Analyzer(Swiftlint)
[1.1] Make sure No compilation error or warning.

## 2 - General
[2.1] Single Responsibility Principle (SRP)
- Do not place more than one responsibility into a single class or function, refactor into separate classes and functions **(Plain Objects).**
[2.2] Open Closed Principle
- While adding new functionality, existing code should not be modified. New functionality should be written in new classes and functions **(extensions)**.
[2.3] KISS(Keep it simple and stupid)
- The KISS principle is descriptive to keep the code simple and clear, making it easy to understand. After all, programming languages are for humans to understand, computers can only understand 0 and 1 — so keep coding simple and straightforward. Keep your methods small. Each method should only solve one small problem, not many use cases. If you have a lot of conditions in the method, break these out into smaller methods. It will not only be easier to read and maintain, but also help finding bugs a lot faster
[2.4] Comments
- If you need to add a comment to describe anything in your code then probably the code is ugly and not understandable so you need to revise naming and logic to keep it simple (This does not include comments to help reader understand product decisions)
[2.5] Magic #
- Avoid any magic number, define constants instead. Think first if this constant is specific for this view or it's a global setting that should be shared between views
[2.6] DRY(do not repeat yourself), we should avoid any code duplication as much as possible
[2.7] Unit test your code
- Writing unit tests can force you to break your logic into testable pieces
- It forces you to consider using dependency injection
- Add/modify/remove logic should also include Unit tests changes
- If you follow everything from above. It will give you and others peace of mind when making change later
[2.8] Clarity is more important than brevity
- Take more time when writing code to optimize for reading. Code is read much more often than written.
- Naming is extremely important, try your best to name a variable/function/class/struct/protocol to describe its responsibility
[2.9] Unused code
- Always delete unused code. In code review when you see empty method, unused variable, outdated comments, imports hanging around your code, don't just leave it, remove it
[2.10] Naming
- When naming class or variable/function name
- Name of class and variable should describe "what"
- Function name should describe "how"
- In both cases, make sure it doesn't leak implementation detail through the name.
- Prefer declarative over imperative programming
- Declarative style: Describe what it does rather than how. It can greatly help with readability at the call site. It also hides implementation details and minimize call site change when implementation changes in the future.
- Imperative style: Describe how something is achieved. When implementation changes in the future, name used may not be accurate anymore. It also leaks too much implementation details to the call site.
[2.11] Avoid Nested if.
[2.12] Prefer switch over if-else.
[2.13] Localization, do you have any unlocalized strings. All customer facing strings shall be localized.
[2.14] Third party dependency version, please make sure to add the dependency version.

## 3 - Architecture
[3.1] Project architectural pattern, make sure you follow the project's architectural pattern.
[3.2] Responsibility, ask yourself if this code is the responsibility of the layer you added in or not. eg.rounded corner, shadows are the view responsibility not the model or the business logic, but if it's for a cell shall the cell set it or the viewController ?!
- Naming convention, make sure you follow the project's naming convention.
- Prefer dependency injection for dependencies, avoid hidden dependencies
- Prefer Composition over inheritance as Swift does not support multiple inheritance.
- create Protocols and extend them using Protocol Extensions to provide default method implementations. This allows us to create much cleaner code, compared to what we could implement by relying solely on the Classical Inheritance pattern.
[3.3] When functions created has potential to be reused frequently, consider making the function available under an extension.
[3.4] Create protocol to provide extra sets of functionalities
- When adding new functionalities to existing class/struct. Consider creating protocols describing functionalities added.
- A generic type may be able to satisfy the requirements of a protocol only under certain conditions, such as when the type’s generic parameter conforms to the protocol. You can make a generic type conditionally conform to a protocol by listing constraints when extending the type. (protocol ... where ...) TODO: Provide example
- Create protocol with associated types to provide same functionality to multiple types. Each type conform to the PATs will provide their own associatedType and implementation to the functions defined in the protocol. TODO: provide example
[3.5] (Optional, but recommended) Create/modify a diagram when adding/updating new features
- Diagram can be included in the code review description for better clearity to reviewer

## 4 - Performance
[4.1] Main thread, heavy operation shall not be done on main thread, main thread is designed mainly for UI operations.
[4.2] To determine if you have any UI issue or overlapping views, please debug view hierarchy.
[4.3] Debug memory graph. To determine if you have any strong reference cycle, please debug the memory graph and make sure we don't have any memory leak.
- For help on understanding on when to use `weak self` please check this [article](https://www.donnywals.com/when-to-use-weak-self-and-why/)
- If you are using combine,  please take a look at this [article](https://www.swiftbysundell.com/articles/combine-self-cancellable-memory-management/) as well
[4.4] Remove observers/invalidate timer on view dismissing.
- If your app targets iOS 9.0 and later or macOS 10.11 and later, and you used addObserver:selector:name:object:, you do not need to unregister the observer.

## 5 - UI
[5.1] Different screen sizes, does the design fit on all screen sizes.
[5.2] Constraints logic, does the constraints logic makes sense or will break in any case. Look for constraint conflicts in console during testings.
[5.3] Fonts, spacing and colors, do they match the prototype, are they added in a generic place for reusing.
[5.4] Consider adding "Empty states" for views
[5.5] (Optional) Consider taking a look at Combine and see if UI can be derived from data change

## 6 - Styling
[6.1] Code separation and organization, user pragma marks to organize the code as well as extensions eg.extension for the view controller conforming to UITableViewDataSource
[6.2] Files architecture, make sure you follow the project's files architecture

## 7 - Bugfix
[7.1] Understand what the root cause is before starting to apply any fix

## 8 - MISC
[8.1] Only ask for review after CI passes
[8.2] If you have doubts of your current solution to the issue you are trying to solve
- Talk to other developers and see what they think of your solution.
- It may very well save the time and energy of yourself and people who's going to review your logic.
[8.3] When receive product requirements
- Clarify product requirements and make sure to understand what functionalities product manager is really asking for
- Only look into solution if requirement is a valid one. Otherwise it may cause potential over-engineering
- Make sure feature design is aligned with Apple/Google's design guideline
- There maybe a lot of right answers to the wrong questions. Make sure to ask the right questions first.

## Notes:
- For diagram, if possible provide detail to n + 1 layer of the lowest layer modified/added

## References:
- [Original content](https://github.com/FadiOssama/Swift-Code-Review-Checklist)