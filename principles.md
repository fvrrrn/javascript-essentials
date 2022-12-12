
# SOLID

## Single responsibility principle (SPR)

1. One entity does one thing

Typical example would be a HTML form. Let's say there's a form which field are needed for a user creation.

```javascript
export const UserForm: FC = () => {
  const handleSubmit = (event: FormEvent<HTMLFormElement>) => {
    event.preventDefault()
    // ...
  }

  const handleReset = () => {
    // ...
  }

  return (
    <form onSubmit={handleSubmit}>
      <h1>User</h1>
      <input type="text" placeholder="name" />
      <input type="text" placeholder="surname" />
      <input type="text" placeholder="login" />
      <button type="submit">Save</button>
      <button type="button" onClick={handleReset}>Reset</button>
    </form>
  )
}
```

What if there's a different form for different user country of origin? What if there's a edit form, delete form etc.? That would break SRP so we take logic somewhere else:

```javascript
export type UserFormProps = {
	onSubmit: (event: FormEvent<HTMLFormElement>) => void
	onReset: () => void
}

export const UserForm: FC<UserFormProps> = ({ onSubmit, onReset }) => (
    <form onSubmit={onSubmit}>
      <h1>User</h1>
      <input type="text" placeholder="name" />
      <input type="text" placeholder="surname" />
      <input type="text" placeholder="login" />
      <button type="submit">Save</button>
      <button type="button" onClick={onReset}>Reset</button>
    </form>
  )
```
---

## Open-closed Principle (OCP)

The Open-Closed Principle requires that classes should be open for extension and closed to modification. So what this principle wants to say is: We should be able to add new functionality without touching the existing code for the class. This is because whenever we modify the existing code, we are taking the risk of creating potential bugs. So we should avoid touching the tested and reliable (mostly) production code if possible.

---

## Liskov Substitution Principle (LSP)

The Liskov Substitution Principle states that subclasses should be substitutable for their base classes. 

This means that, given that class B is a subclass of A (inheritance), A methods in B should behave the same way there do in A, and not to be overriden.

This is the expected behavior, because when we use inheritance we assume that the child class inherits everything that the superclass has. The child class extends the behavior but never narrows it down.

Therefore, when a class does not obey this principle, it leads to some nasty bugs that are hard to detect.

---

## Interface Segregation Principe (ISP):

The principle states that many client-specific interfaces are better than one general-purpose interface. Clients should not be forced to implement a function they do no need.

---

## Dependency Inversion Principle (DIP):

The Dependency Inversion principle states that our classes should depend upon interfaces or abstract classes instead of concrete classes and functions.

In his article (2000), Uncle Bob summarizes this principle as follows:

"If the OCP states the goal of OO architecture, the DIP states the primary mechanism".
These two principles are indeed related and we have applied this pattern before while we were discussing the Open-Closed Principle.

We want our classes to be open to extension, so we have reorganized our dependencies to depend on interfaces instead of concrete classes. Our PersistenceManager class depends on InvoicePersistence instead of the classes that implement that interface.
