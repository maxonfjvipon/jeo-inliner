# JEO Inliner
Java to EO inline optimizer. It takes EO that was [created](https://github.com/objectionary/jeo-maven-plugin) from 
java bytecode and tries to apply "inlining" optimization:

The  simple example of optimization:
```java
// BEFORE
class A {
    private int d;
    A(int d) { 
        this.d = d; 
    }
    int foo () { 
        return d + 1; 
    }
}

final class B {
    private final A a;
    B(A a) {
        this.a = a;
    }
    int bar() {
        return a.foo() + 2;
    }
}

int x = new B(new A(42)).bar();

// AFTER
class C {
    private int d;
    C(int d) {
        this.d = d;
    }
    int bar() {
        return d + 1 + 2;
    }
}
int x = new C(42).bar();
```

