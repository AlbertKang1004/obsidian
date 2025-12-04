```java
Animal d = new Dog();

Animal d1 = new Animal();
Animal d2 = new Dog();
```
- In line 1, `Animal` is called the **reference type**, and `Dog` is called the **object type**.
- **Reference type** cannot be a subclass of the **object type**.
	- ex) `Dog d3 = new Animal();`

| Name | Reference Type | Object Type |
| ---- | -------------- | ----------- |
| `d1` | `Animal`       | `Animal`    |
| `d2` | `Animal`       | `Dog`       |
## Methods

![[Reference Type|500]]

| Name | Reference Type | Object Type |
| ---- | -------------- | ----------- |
| `d1` | `Animal`       | `Animal`    |
| `d2` | `Animal`       | `Dog`       |
| `d3` | `Dog`          | `Dog`       |
- `d1.bark();` causes an error because it cannot find `bark()` in its reference type, `Animal`. 
- `d1.breathe();` works as its reference type is `Animal`, and `Animal` has method `breathe()`.
- `d2.breathe();` works as its reference type is `Animal`, and `Animal` has method `breathe()`.
	- Then Java will track up from its object type, `Dog`, to find if there are any overridden versions.
- `d3 = (Dog) d2;` casts `d2`'s reference type to `Dog` and assigns it to `d3`.
- `d3.bark();` works as its reference type is `Dog`, and `Dog` has method `bark()`.
> If the subclass wants Java to treat it as an **override**, the method signature must stay the same. (name  / parameters / return type)
## Instances

![[Reference Type 2]]

| Name | Reference Type | Object Type |
| ---- | -------------- | ----------- |
| `d1` | `Animal`       | `Animal`    |
| `d2` | `Animal`       | `Dog`       |
| `d3` | `Dog`          | `Dog`       |
- `d1.x;` works, because its reference type `Animal` does not have `x`, so the compiler moves up to its superclass `Object` and finds `x`.
- `d2.age;` causes a **compile-time error** because the reference type `Animal` does not have `age`, and neither does its superclass `Object`.
	- Note: The compiler **does not check** `Dog` even though the object is a `Dog`.
- `d3.name;` works, because its reference type `Dog` does not have `name`, so the compiler moves up to its superclass `Animal` and finds `name`.
- `d3.age;` works, because its reference type `Dog` has `age`.
