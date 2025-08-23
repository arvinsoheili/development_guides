# 🟢 Basics of Writing Tests in Vitest

## 1. Structure

Every test file usually has:

- `describe()` → groups related tests
- `it()` / `test()` → actual test cases
- `expect()` → assertions (what should be true)

Example:

```ts
import { describe, it, expect } from "vitest";

describe("Math", () => {
  it("adds numbers correctly", () => {
    const result = 2 + 2;
    expect(result).toBe(4);
  });

  it("subtracts numbers correctly", () => {
    const result = 5 - 3;
    expect(result).toBe(2);
  });
});
```

---

## 2. Testing React Components

For React, we use `@testing-library/react`.

**Example: `Button.tsx`**

```tsx
type Props = { label: string; onClick: () => void };

export default function Button({ label, onClick }: Props) {
  return <button onClick={onClick}>{label}</button>;
}
```

**Test: `Button.test.tsx`**

```tsx
import { render, screen, fireEvent } from "@testing-library/react";
import Button from "./Button";

describe("Button", () => {
  it("renders label", () => {
    render(<Button label="Click me" onClick={() => {}} />);
    expect(screen.getByText("Click me")).toBeInTheDocument();
  });

  it("fires onClick when clicked", () => {
    const mockFn = vi.fn();
    render(<Button label="Press" onClick={mockFn} />);
    fireEvent.click(screen.getByText("Press"));
    expect(mockFn).toHaveBeenCalledTimes(1);
  });
});
```

---

## 3. Form Example

**Component: `LoginForm.tsx`**

```tsx
import { useState } from "react";

export default function LoginForm({ onSubmit }: { onSubmit: (data: { email: string; password: string }) => void }) {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");

  return (
    <form
      onSubmit={(e) => {
        e.preventDefault();
        onSubmit({ email, password });
      }}
    >
      <input
        type="email"
        placeholder="Email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      <input
        type="password"
        placeholder="Password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
      />
      <button type="submit">Login</button>
    </form>
  );
}
```

**Test: `LoginForm.test.tsx`**

```tsx
import { render, screen, fireEvent } from "@testing-library/react";
import LoginForm from "./LoginForm";

describe("LoginForm", () => {
  it("submits form with email and password", () => {
    const mockSubmit = vi.fn();
    render(<LoginForm onSubmit={mockSubmit} />);

    fireEvent.change(screen.getByPlaceholderText("Email"), { target: { value: "test@mail.com" } });
    fireEvent.change(screen.getByPlaceholderText("Password"), { target: { value: "1234" } });
    fireEvent.click(screen.getByText("Login"));

    expect(mockSubmit).toHaveBeenCalledWith({ email: "test@mail.com", password: "1234" });
  });
});
```

---

## 4. Table Example

**Component: `ProductTable.tsx`**

```tsx
type Product = { id: number; name: string; price: number };

export default function ProductTable({ products }: { products: Product[] }) {
  return (
    <table>
      <tbody>
        {products.map((p) => (
          <tr key={p.id}>
            <td>{p.name}</td>
            <td>{p.price}</td>
          </tr>
        ))}
      </tbody>
    </table>
  );
}
```

**Test: `ProductTable.test.tsx`**

```tsx
import { render, screen } from "@testing-library/react";
import ProductTable from "./ProductTable";

describe("ProductTable", () => {
  it("renders all products", () => {
    const products = [
      { id: 1, name: "Apple", price: 100 },
      { id: 2, name: "Banana", price: 50 },
    ];
    render(<ProductTable products={products} />);
    expect(screen.getByText("Apple")).toBeInTheDocument();
    expect(screen.getByText("Banana")).toBeInTheDocument();
    expect(screen.getByText("100")).toBeInTheDocument();
    expect(screen.getByText("50")).toBeInTheDocument();
  });
});
```

---

✅ With just this, you can test **UI rendering, user interactions, forms, and data tables**.
