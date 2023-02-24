Why use trait objects?
they allow object-oriented programming through dynamic dispatch which is polymorphism which means one method has multiple behaviors and happens when selection of appropriate implementation occurs at run-time so multiple types are allowed to be used

```rs

```

Trait Objects
* allow for many types
* incurs run-time penalty because of lookup costs in virtual method table because dyn traits have two pointers
    1. -> data
    2. -> function pointer table (vtable)

```rs
pub struct Screen {
    pub components: Vec<Box<dyn Draw>>,
}

impl Screen {
    pub fn run(&self) {
        for component in self.components.iter() {
            component.draw();
        }
    }
}
```

Generic Type Parameters with Trait Bounds
* allow for one concrete type
* great for homogenous collections

```rs
pub struct Screen<T: Draw> {
    pub components: Vec<T>,
}

impl<T> Screen<T>
where
    T: Draw,
{
    pub fn run(&self) {
        for component in self.components.iter() {
            component.draw();
        }
    }
}
```

```rs

```