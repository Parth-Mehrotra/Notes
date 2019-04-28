# Type Safety

Type safety is one of the tools that help programmers garuntee that their programs are "correct". A common form of error happens when you are opperating on the wrong type of data. These can take the obvious form of:

```
"Parth Mehrotra" - 10
```

or the more subtle form off:

```
def navigate(address: String) { ... }

navigate("Einstein Mehrotra")
```

The obvious stuff is easier to catch, as `-` won't be defined for `String`s in most languages. When you go to compile such code, you'll be greeted with a compiler error and will be forced to fix it before continuing.

But with the second example, if it's a `String` we're taking, there is a possibility this function will have a `TypeError`. We can get around this by maybe taking an `Address` object instead of a `String`. Perhaps we can't create the `Address` object without supplying a valid `String` that passes a regex in the constructor of `Address`. Now we've offloaded the problem to the person using our function, but we have reduced the possibility of a TypeError. 

It's worth noting that this check will happen at Runtime rather than at Compile Time.
