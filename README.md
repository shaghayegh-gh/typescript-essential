## Typescript Essential

### Basic Types
TypeScript has several basic types that you can use to define the static type for variables, function parameters, and return values.
-  **boolean:** A true/false value.
      ```ts
      let b: boolean = true;
      ```
-  **number:** A numeric value, either floating point or big integer.
      ```ts
      let n: number = 2;
      ```
-  **string:** A text value.
      ```ts
      let s: string = 'a string';
      ```
-  **array:** A collection of values of the same type, either written as type[] or Array<type>.
     ```ts
      let list1: number[] = [1, 2, 3];
      let list2: Array<number> = [1, 2, 3];
      ```
-  **tuple:** A fixed-length array of values of different types.
      ```ts
      let pair: [string, number] = ["Bob", 42];
      ```
-  **enum:** A named set of constant values.
      ```ts
      enum Color {Red, Green, Blue};
      let c: Color = Color.Green;
      ```
-  **any:** A type that can represent any value.
      ```ts
      let anything: any = 4;
      anything = "hello";
      anything = true;
      ```
-  **unknown:** A type that can represent any value, but requires type checking before using.
      ```ts
      let something: unknown = 4;
      something = "hello";
      something = true; // need to check the type before using it
      ```
-  **void:** A type that represents the absence of any value, usually used for functions that do not return anything.
      ```ts
      function log(message: string): void { console.log(message); }
      ```
-  **null and undefined:** Two special values that represent the absence of a meaningful value.
      ```ts
      let x: null = null;
      let y: undefined = undefined;
      ```
-  **never:** A type that represents values that never occur, such as a function that always throws an error or never returns.
      ```ts
      function error(message: string): never { throw new Error(message); }
      ```
-  **object:** A type that represents any non-primitive value.
      ```ts
      let person: object = {name: "Charlie", age: 25};
      ```
### Advance Types

-  **Intersection:**\
   These are types that combine multiple types into one, using the & operator.\
   For example: A & B is a type that has all the properties of both A and B.
      ```ts
      type Person = { name: string; age: number };
      type Employee = { id: number; department: string };
      type Manager = Person & Employee; // a type that has all the properties of Person and Employee
      ```
-  **Union:**\
   These are types that allow a value to be one of several types, using the | operator.\
   For example: A | B is a type that can be either A or B.
      ```ts
      type Shape = Circle | Square | Triangle; // a type that can be either Circle, Square, or Triangle
      ```
-  **Generic:**\
   These are types that can take other types as parameters and produce new types based on them.\
   For example: Array<T> is a type that represents an array of values of type T.
      ```ts
      let person: object = {name: "Charlie", age: 25};
      ```
-  **Mapped:**\
   These are types that create new types based on the shape of existing types, using a syntax similar to object literals.\
   For example: { [P in keyof T]: T[P] } is a type that maps over the properties of T and preserves their types.
      ```ts
       // a type that has properties "a", "b", and "c" with values of type number
       type Keys = "a" | "b" | "c";
       type Obj = { [K in Keys]: number };
      ```
-  **Type guards:**\
   These are expressions that perform runtime checks on values and narrow their types within a certain scope.\
   For example: typeof x === "string" is a type guard that ensures that x is a string in the true branch of an if statement.
      ```ts
      // a function that checks if x is a string and narrows its type to string
      function isString(x: unknown): x is string { return typeof x === "string"; }
      ```
-  **Conditional:**\
   These are types that select one of two possible types based on a condition, using the syntax T extends U ? X : Y.\
   For example: Exclude<T, U> is a conditional type that excludes from T those types that are assignable to U.
      ```ts
      // a type that excludes null and undefined from T
      type NonNullable<T> = T extends null | undefined ? never : T;
      ```
-  **Utility:**\
   These are built-in types that provide some common type transformations, such as Partial<T>, Required<T>, Readonly<T>, etc.\
   - **Partial<Type>**\
      For example: if you have an interface Todo with three properties, you can use Partial<Todo> to create a type that can have any combination of those properties.
      ```ts
      interface Todo {
      title: string;
      description: string;
      completed: boolean;
      }
      
      let todo1: Partial<Todo> = {}; // valid
      let todo2: Partial<Todo> = { title: "Learn TypeScript" }; // valid
      let todo3: Partial<Todo> = { title: "Learn TypeScript", completed: true }; // valid
      let todo4: Partial<Todo> = { title: "Learn TypeScript", priority: 1 }; // invalid, priority is not a property of Todo
      ```
   - **Required<Type>**\
     For example: if you have an interface Person with two optional properties, you can use Required<Person> to create a type that requires both properties.
      ```ts
      interface Person {
      name?: string;
      age?: number;
      }
      
      let person1: Required<Person> = {}; // invalid, name and age are required
      let person2: Required<Person> = { name: "Alice" }; // invalid, age is required
      let person3: Required<Person> = { name: "Alice", age: 21 }; // valid
      let person4: Required<Person> = { name: "Alice", age: 21, location: "New York" }; // invalid, location is not a property of Person
      ```
   - **Readonly<Type>**\
     For example, if you have an interface Point with two properties, you can use Readonly<Point> to create a type that prevents modifying those properties.
      ```ts
      interface Point {
      x: number;
      y: number;
      }
      
      let point1: Readonly<Point> = { x: 10, y: 20 }; // valid
      point1.x = 15; // invalid, x is readonly
      point1.y++; // invalid, y is readonly
      point1.z = 30; // invalid, z is not a property of Point
      ```
   - **ReturnType<Type>:**\
     For example: if you have a function type that returns a number, you can use ReturnType<Type> to create a type that is the same as the return type of the function.
      ```ts
      type Adder = (a: number, b: number) => number;
      
      let result1: ReturnType<Adder> = 10; // valid
      let result2: ReturnType<Adder> = "hello"; // invalid, string is not assignable to number
      ```
     - **Parameters<Type>**\
     For example, if you have a function type that takes two parameters of type string and number, you can use Parameters<Type> to create a tuple type that represents the parameter types 
     of the function.
      ```ts
      type Logger = (message: string, level: number) => void;
      
      let params1: Parameters<Logger> = ["error", 1]; // valid
      let params2: Parameters<Logger> = [1, "error"]; // invalid, number is not assignable to string and vice versa
      ```
   - **Pick<Type, Keys>**\
     For example: if you have an interface User with four properties, you can use Pick<User, "name" | "email"> to create a type that only has the name and email properties.
      ```ts
      interface User {
      name: string;
      email: string;
      password: string;
      role: string;
      }
      
      let user1: Pick<User, "name" | "email"> = {}; // invalid, name and email are required
      let user2: Pick<User, "name" | "email"> = { name: "Bob", email: "bob@example.com" }; // valid
      let user3: Pick<User, "name" | "email"> = { name: "Bob", email: "bob@example.com", password: "secret" }; // invalid, password is not a property of Pick<User, "name" | "email">
      ```
   - **Omit<Type, Keys>**\
     For example: if you have an interface User with four properties, you can use Omit<User, "password" | "role"> to create a type that excludes the password and role properties.
      ```ts
      interface User {
      name: string;
      email: string;
      password: string;
      role: string;
      }
      
      let user1: Omit<User, "password" | "role"> = {}; // invalid, name and email are required
      let user2: Omit<User, "password" | "role"> = { name: "Bob", email: "bob@example.com" }; // valid
      let user3: Omit<User, "password" | "role"> = { name: "Bob", email: "bob@example.com", password: "secret" }; // invalid, password is not a property of Omit<User, "password" | "role">
      ```
   - **Exclude<Type, ExcludedUnion>**\
     For example: if you have a type Animal with four values, you can use Exclude<Animal, "cat" | "dog"> to create a type that excludes the cat and dog values.
      ```ts
      type Animal = "cat" | "dog" | "bird" | "fish";
      
      let animal1: Exclude<Animal, "cat" | "dog"> = "cat"; // invalid, cat is excluded
      let animal2: Exclude<Animal, "cat" | "dog"> = "bird"; // valid
      let animal3: Exclude<Animal, "cat" | "dog"> = "lion"; // invalid, lion is not a value of Animal
      ```
   - **Record<Keys, Type>**\
     For example: if you have a type Color with three values, you can use Record<Color, string> to create an object type that maps each color to a string.
      ```ts
      type Color = "red" | "green" | "blue";
      
      let colorMap: Record<Color, string> = {}; // invalid, colorMap must have properties for each color
      let colorMap: Record<Color, string> = { red: "#FF0000", green: "#00FF00", blue: "#0000FF" }; // valid
      let colorMap: Record<Color, string> = { red: "#FF0000", green: "#00FF00", blue: "#0000FF", yellow: "#FFFF00" }; // invalid, yellow is not a value of Color
      ```







