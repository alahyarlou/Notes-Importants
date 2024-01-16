# useMemo

`useMemo` is a React hook that memoizes the result of a computation. It is used to optimize performance by avoiding unnecessary calculations when a component re-renders. Memoization is a technique where the result of a function call is stored and returned when the same inputs occur again.

Here is a simple tutorial on how to use useMemo in React with examples:

### Basic Usage

Let's start with a simple example where we calculate the square of a number using useMemo.

```jsx
import React, { useState, useMemo } from "react";

const SquareCalculator = ({ number }) => {
  // Calculate the square using useMemo
  const square = useMemo(() => {
    console.log("Calculating square...");
    return number * number;
  }, [number]); // Dependency array: Recalculate when 'number' changes

  return (
    <div>
      <p>Number: {number}</p>
      <p>Square: {square}</p>
    </div>
  );
};

const App = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      <SquareCalculator number={count} />
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};

export default App;
```

In this example, the `SquareCalculator` component calculates the square of a number using `useMemo`. The calculation only occurs when the number prop changes.

### Performance Optimization

You can use `useMemo` to optimize the performance of expensive calculations or computations that depend on certain props or state.

```jsx
import React, { useState, useMemo } from "react";

const ExpensiveCalculation = ({ data }) => {
  // Expensive calculation using useMemo
  const result = useMemo(() => {
    console.log("Performing expensive calculation...");
    // Simulate an expensive calculation
    return data.reduce((acc, value) => acc + value, 0);
  }, [data]);

  return (
    <div>
      <p>Result of Expensive Calculation: {result}</p>
    </div>
  );
};

const App = () => {
  const [numbers, setNumbers] = useState([1, 2, 3, 4, 5]);

  return (
    <div>
      <ExpensiveCalculation data={numbers} />
      <button onClick={() => setNumbers([...numbers, Math.random()])}>
        Add Random Number
      </button>
    </div>
  );
};

export default App;
```

In this example, the `ExpensiveCalculation` component performs a potentially expensive calculation using `useMemo`. The calculation only occurs when the data prop changes.

### Avoiding Unnecessary Rerenders

`useMemo` can be used to avoid unnecessary re-renders when computing a value that does not change.

```jsx
import React, { useState, useMemo } from "react";

const ConstantValue = () => {
  // A constant value using useMemo
  const constantValue = useMemo(() => {
    console.log("Calculating constant value...");
    return "This value does not change";
  }, []); // Empty dependency array: Never recalculate

  return (
    <div>
      <p>Constant Value: {constantValue}</p>
    </div>
  );
};

const App = () => {
  // Changing state to trigger re-renders
  const [count, setCount] = useState(0);

  return (
    <div>
      <ConstantValue />
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};

export default App;
```
In this example, the `ConstantValue` component calculates a constant value using `useMemo`, and it won't recalculate unless the dependencies change.

Remember, while `useMemo` can optimize certain scenarios, it's essential to use it judiciously, as unnecessary memoization can lead to code complexity. Always profile your application's performance before and after using `useMemo` to ensure that it provides the intended optimizations.