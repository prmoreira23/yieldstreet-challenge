# Singleton

Let's say you have a class with dependencies injected via the constructor, but you also want
a singleton default instance, lazily created when first accessed. This is one possible implementation:

```java
public class StuffService {
    private final Object dep1;
    private final Object dep2;

    public StuffService(Object dep1, Object dep2) {
        this.dep1 = dep1;
        this.dep2 = dep2;
    }

    public static StuffService defaultInstance() {
        if (_instance == null) {
            _instance = new StuffService(new Object(), new Object());
        }

        return _instance;
    }

    private static StuffService _instance;
}
```

What's wrong with the `defaultInstance()` implementation? How would you fix it?


The class is not a Singleton class. You can easily instantiate several instances of StuffService.
The dependencies are set using the constructor, when one calls the *defaultInstance()* method, they are not passing
the dependencies, but some blank newly instantiated *Object* instances.
The dependencies are not being passed to the singleton instance, one way to solve it is by creating setters for all your dependencies, so if one of them is missing you could just set it by passing an instance of that dependency.
