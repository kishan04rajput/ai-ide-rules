---
name: coding-in-ruby-on-rails
description: Follow these rules while coding in ruby on rails.
---

Follow these rules strictly when coding in Ruby on Rails to ensure a maintainable, high-performance, and secure codebase.

### 1. General Rails Structure
*   **Follow Rails Conventions**: Adhere strictly to the standard MVC architecture and Rails directory structure.
*   **The Rails Way**: Use built-in Rails features (helpers, callbacks, etc.) before implementing custom solutions.

### 2. Fat Models & Skinny Controllers
*   **Skinny Controllers**: Controllers should only handle requests (params, authentication, session) and responses (rendering, redirection). Business logic **must not** reside in controllers.
*   **Fat Models**: Business logic, complex validations, and data transformations belong in models. If a method is used multiple times or contains complex logic, it **must** reside in its suitable model.
*   **Scopes**: Use model scopes for common database queries to keep logic reusable and readable.
*   **Query Objects**: For complex queries involving multiple tables, use Query Objects.

### 3. Service Objects
*   **Business Workflows**: Use Service Objects (e.g., `app/services`) for operations that involve multiple models or complex third-party integrations.

### 4. API Responses (Jbuilder)
*   **JSON.Jbuilder**: Always use `.json.jbuilder` files for crafting API responses. Do not render complex JSON directly in controllers.
*   **Decoupling**: Keep the response structure separate from the controller logic.
*   **Explicit Render**: If a controller uses `json.jbuilder`, always explicitly call `render` at the end of the controller action to show which file is getting rendered (e.g., `render :show` or `render 'users/show'`).

### 5. Performance (N+1 Prevention)
*   **Eager Loading**: Always use `.includes`, `.preload`, or `.eager_load` to prevent N+1 query issues.
*   **Bullet**: Utilize tools (like the Bullet gem) during development to catch N+1 queries early.

### 6. Security & Parameters
*   **Strong Parameters**: Strictly use `params.require(...).permit(...)` to prevent mass assignment vulnerabilities.
*   **Sanitization**: Never trust user input. Use Rails' built-in sanitization and escaping.

### 7. Coding Style & Naming
*   **Standard Conventions**: Use `snake_case` for methods and variables, and `CamelCase` for classes/modules.
*   **Meaningful Names**: Give variables and methods descriptive, intent-revealing names.
