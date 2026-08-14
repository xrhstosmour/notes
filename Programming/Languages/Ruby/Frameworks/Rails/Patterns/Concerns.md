#ruby #rails #concerns #design-patterns #modules

A concern is a [[Modules|module]] used to share behavior across models or controllers. `ActiveSupport::Concern` is Rails' wrapper around `include`/`prepend` that adds hooks for class-level macros.

``` ruby
module SoftDeletable
  extend ActiveSupport::Concern

  included do
    default_scope { where(deleted_at: nil) }
  end

  def soft_delete
    update(deleted_at: Time.current)
  end

  class_methods do
    def only_deleted
      unscoped.where.not(deleted_at: nil)
    end
  end
end

class Order < ApplicationRecord
  include SoftDeletable
end
```

What `ActiveSupport::Concern` adds over a plain module:

- `included`/`prepended` blocks run in the context of the including class, so you can call class-level macros (like `default_scope` above) at include time.
- `class_methods do ... end` defines methods that become class methods on the includer, instead of needing a nested `ClassMethods` module and `self.included` boilerplate.
- Declaring more than one `included`/`prepended` block raises, unlike a plain module where you'd just overwrite the hook.

Use a concern when the shared behavior is genuinely a mixin, it doesn't need a life of its own outside the classes that include it. Once it needs to be tested, instantiated, or called independently of a specific model, it's a [[Service Objects|service object]] instead.
