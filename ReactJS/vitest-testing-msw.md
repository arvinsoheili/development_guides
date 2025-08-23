# Vitest Testing Basics + MSW (Mock Service Worker)

This guide covers writing tests with **Vitest + React Testing Library**
and mocking API calls using **MSW**.

------------------------------------------------------------------------

## ✅ Vitest Setup

`vite.config.ts`:

``` ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import path from "path";
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
  plugins: [react(), tailwindcss()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
  test: {
    globals: true,
    environment: "jsdom",
    setupFiles: "./src/tests/setup.ts",
  },
});
```

------------------------------------------------------------------------

## 🧪 Example: Form Validation Test

``` tsx
import { render, screen, fireEvent } from "@testing-library/react";
import { describe, it, expect } from "vitest";
import Login from "../components/Login";

describe("Login form", () => {
  it("shows error when submitting empty form", async () => {
    render(<Login />);

    fireEvent.click(screen.getByRole("button", { name: /login/i }));

    expect(await screen.findByText(/This Field is Required!/i)).toBeInTheDocument();
  });
});
```

------------------------------------------------------------------------

## 🔌 MSW Setup

Install MSW:

``` bash
npm install msw --save-dev
```

Create `src/tests/mocks/handlers.ts`:

``` ts
import { rest } from "msw";

export const handlers = [
  rest.post("/api/login", async (req, res, ctx) => {
    const { username, password } = await req.json();
    if (username === "admin" && password === "1234") {
      return res(ctx.json({ message: "success", token: "fake_jwt" }));
    }
    return res(ctx.status(401), ctx.json({ message: "Invalid credentials" }));
  }),
];
```

Create `src/tests/setup.ts`:

``` ts
import { afterAll, afterEach, beforeAll } from "vitest";
import { setupServer } from "msw/node";
import { handlers } from "./mocks/handlers";

const server = setupServer(...handlers);

beforeAll(() => server.listen());
afterEach(() => server.resetHandlers());
afterAll(() => server.close());

// Mock window.alert to prevent errors
vi.spyOn(window, "alert").mockImplementation(() => {});
```

------------------------------------------------------------------------

## 🧪 Example: Integration Test with API

``` tsx
import { render, screen, fireEvent, waitFor } from "@testing-library/react";
import { describe, it, expect } from "vitest";
import Login from "../components/Login";

describe("Login integration", () => {
  it("logs in successfully", async () => {
    render(<Login />);

    fireEvent.change(screen.getByLabelText(/username/i), { target: { value: "admin" } });
    fireEvent.change(screen.getByLabelText(/password/i), { target: { value: "1234" } });
    fireEvent.click(screen.getByRole("button", { name: /login/i }));

    await waitFor(() => {
      expect(window.alert).toHaveBeenCalledWith("Welcome back!");
    });
  });

  it("shows error for invalid credentials", async () => {
    render(<Login />);

    fireEvent.change(screen.getByLabelText(/username/i), { target: { value: "wrong" } });
    fireEvent.change(screen.getByLabelText(/password/i), { target: { value: "wrong" } });
    fireEvent.click(screen.getByRole("button", { name: /login/i }));

    await waitFor(() => {
      expect(window.alert).toHaveBeenCalledWith("Invalid credentials");
    });
  });
});
```

------------------------------------------------------------------------

## 📌 Summary

-   ✅ Use **Vitest** with `jsdom` for React components
-   ✅ Mock **window.alert** or other browser APIs
-   ✅ Use **MSW** to intercept & mock API requests
-   ✅ Write both **unit tests** (validation) and **integration tests**
    (API + UI)
