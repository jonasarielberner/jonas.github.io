---
layout:     post
title:      "The day that you got a strange NullPointerException with an enum running unit tests"
subtitle:   "A bit of craziness with enums and static methods in unit tests"
date:       2017-06-01 18:00:00
author:     "Cedulio Cezar"
tags: [programming,java,android,unit tests, junit, mockito, powermock, java, android]
header-img: "img/home.png"
social-img: "img/home.png"
summary: "NullPointerException on a switch(enumValue) !"
comments: True
---
It's nothing new to the community that final classes, enums and statics aren't friendly to testing.

Although sometimes you just can't avoid them and at the same time you need to test the class that you are changing.

#### TL;DR

If you, for whatever crazy reason, have an enum and inside you got an static method returning an instance of the enum, if try to mock that method inside a test then you will got strange errors when a switch(enumValue) is called, even if you are debbuging and see that the variable isn't null at all.

## switch statement throwing NullPointerException

For the sake of example imagine that you have an enum called Animal and it's values as described below and inside you have an static method returning a value of the enum.

```
public enum Animal{
    CAT,
    DOG;

    public static Animal geFavoriteAnimal(){
        return DOG;
    }
}
```

Now let's write a class that uses that static method for some crazy logic, that return a string based on the value returned by the static method.

```
public class AnimalLogger {

    public String log() {
        Animal animal = Animal.geFavoriteAnimal();

        switch (animal) {
            case CAT:
                return "MEOWTH";
            case DOG:
                return "WOUF";
            default:
                return "WHAT";
        }
    }
}
```

### Testing
Now we want to test that thing, because this how it should be, right? So you write the test mocking the return of the static method with a test class as shown below.
```
// prepare your tests to be able to mock an static
@RunWith(PowerMockRunner.class)
@PrepareForTest({Animal.class})
public class AnimalLoggerTest {

    @Before
    public void setUp() throws Exception {
        mockStatic(Animal.class); // preprare the test to receive static calls and mock

    }

    @Test
    public void log() throws Exception {

        when(Animal.geFavoriteAnimal()).thenReturn(Animal.CAT); // remember that the actual method returns dog!

        AnimalLogger animalLogger = new AnimalLogger();

        String actualSound = animalLogger.log();

        String expectedSound = "MEOWTH";

        assertEquals(expectedSound, actualSound);

    }

}
```

Everything is fine, and the test should pass, right?

### Not so fast!

If you run this yourself, you will notice that the line with switch(animal) will throw a NullPointerException, that to me was totally crazy.

At this point you should be thinking, "You aren't supposed to do that and that's strange and wrong". I agree with however message error just points to the line with switch and if you run a test with a breakpoint in that line you will notice that the value isn't null at all.

It took me some time to realize that if you mock the interactions with the enum Animal, it will catch everything so when the switch does its thing at some point we are not mocking and the result is a NullPointerException even though the value passed to the switch isn't.


If you move the static method from the enum scope to another class and try to mock everything works.
