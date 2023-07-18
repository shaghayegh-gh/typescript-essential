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



