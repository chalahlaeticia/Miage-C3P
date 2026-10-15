 # Weekly Report 05

## Glauriel

**What I Learned:**

To prepare for next week's exam, I reviewed the previous lectures and the key concepts we covered.

I focused on important points, including the answers to the questions on the worksheet distributed during our first class.

For example, I reviewed the difference between `this` and `super`: both refer to the receiver of a message, but `this` starts method lookup in the receiver's class, whereas `super` starts the lookup in the superclass of the class where the expression appears.

I also reviewed the structure and purpose of different design patterns, such as Composite, which uses recursion to work with composite structures, and Visitor, which uses double dispatch to separate operations from the object structure on which they are performed.

****Projects Link:****

* [DoubleDispatch](https://github.com/badjilaglaurielfauster-glitch/DoubleDispatch): The Rock-Paper-Scissors-Lizard-Spock game implemented using the Double Dispatch approach.

* [SystemFiles](https://github.com/badjilaglaurielfauster-glitch/SystemFiles): A file explorer simulator developed to practice the Composite pattern.

* [Chess](https://github.com/badjilaglaurielfauster-glitch/Chess): The chess game project.

* [MyCounter](https://github.com/badjilaglaurielfauster-glitch/MyCounter): An introductory exercise to become familiar with Pharo.



## Tien

**What I Learned**

* Avoid globals because they create hidden dependencies that make code hard to test and maintain.
* Hence, that explains why the Singleton pattern is so misunderstood and should usually be avoided—people often just use it as a disguised global variable >>> solution: to use parameters instead.
* Passing what we need directly into a method keeps the coupling low.
* Read lectures and watched videos about Chess project: even though it doesn't help to debug the current version but it gives the idea and also super helpful for using effectively the Pharo IDE.

**Exercises**

**[Chess Game](https://github.com/nttt1400/Chess)** : 3 refactor commits