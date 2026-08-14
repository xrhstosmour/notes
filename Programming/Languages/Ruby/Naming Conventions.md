#ruby #naming-conventions #model #class #table #schema

Below is a table summarizing the naming conventions in Ruby:

| Aspect             | Case       | Count    | Example                                              |
| ------------------ | ---------- | -------- | ---------------------------------------------------- |
| Files              | snake_case | Depends  | `user_profile.rb`                                    |
| Class/Module/Model | CamelCase  | Singular | `UserProfile`                                        |
| Table/Schema       | snake_case | Plural   | `user_profiles`                                      |
| Constant           | SCREAMING_SNAKE_CASE | Depends | `MAXIMUM_LOGIN_ATTEMPTS`                    |
| Predicate method   | snake_case, `?` suffix | Depends | `valid?`, `paid?`                         |
| Dangerous method   | snake_case, `!` suffix | Depends | `save!`, `cancel!`                        |

Predicate methods (`?` suffix) return a boolean and must not mutate state. Dangerous methods (`!` suffix) mutate the receiver or raise on failure, where a non-`!` counterpart exists that fails quietly instead (e.g. `save` returns `false`, `save!` raises).
