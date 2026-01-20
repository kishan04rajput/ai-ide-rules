---
name: coding-in-ruby-on-rails
description: Follow these rules while coding in ruby on rails.
---

Follow these rules strictly when coding in Ruby on Rails to ensure a maintainable, high-performance, and secure codebase.

### 1. General Rails Structure
*   **Follow Rails Conventions**: Adhere strictly to the standard MVC architecture and Rails directory structure.
*   **The Rails Way**: Use built-in Rails features (helpers, callbacks, etc.) before implementing custom solutions.

### 2. Model Best Practices (Keep it DRY)
*   **Logic in Models**: If a method is used multiple times or contains complex business logic, it **must** reside in its suitable model.
*   **Skinny Controllers**: Controllers should only handle requests and responses. Business logic belongs in models or service objects.
*   **Scopes**: Use model scopes for common database queries to keep logic reusable and readable.
*   **Query Objects**: For complex queries involving multiple tables, use Query Objects.

### 3. Service Objects
*   **Business Workflows**: Use Service Objects (e.g., `app/services`) for operations that involve multiple models or complex third-party integrations.

### 4. API Responses (Jbuilder)
*   **JSON.Jbuilder**: Always use `.json.jbuilder` files for crafting API responses. Do not render complex JSON directly in controllers.
*   **Decoupling**: Keep the response structure separate from the controller logic.

### 5. Performance (N+1 Prevention)
*   **Eager Loading**: Always use `.includes`, `.preload`, or `.eager_load` to prevent N+1 query issues.
*   **Bullet**: Utilize tools (like the Bullet gem) during development to catch N+1 queries early.

### 6. Security & Parameters
*   **Strong Parameters**: Strictly use `params.require(...).permit(...)` to prevent mass assignment vulnerabilities.
*   **Sanitization**: Never trust user input. Use Rails' built-in sanitization and escaping.

### 7. Coding Style & Naming
*   **Standard Conventions**: Use `snake_case` for methods and variables, and `CamelCase` for classes/modules.
*   **Meaningful Names**: Give variables and methods descriptive, intent-revealing names.
