#active-record #relationships #many-to-many #association-table #ruby #rails #orm

When dealing with many-to-many relationships in the Ruby on Rails framework, there are two available options.

#### With association table:

``` ruby
class Book < ApplicationRecord
  has_many :book_authors
  has_many :authors, through: :book_authors
  # Other properties.
end

# Association table.
class BookAuthor < ApplicationRecord
  belongs_to :book
  belongs_to :author
  # Other properties.
end

class Author < ApplicationRecord
  has_many :book_authors
  has_many :books, through: :book_authors
  # Other properties.
end
```

#### Without association table:

``` ruby
class Book < ActiveRecord::Base
  has_and_belongs_to_many :users
  # Other properties.
end

class Author < ActiveRecord::Base
  has_and_belongs_to_many :books
  # Other properties.
end
```

#### Which to Use

Prefer the join-model approach (`has_many :through`) by default, even when the join table starts out with no extra columns. It's a real `ActiveRecord` model, so it can later gain its own columns (e.g. a `role` on a membership), callbacks, or validations without a schema migration to convert away from `has_and_belongs_to_many`. Reach for `has_and_belongs_to_many` only for a genuinely simple, unlikely-to-grow join with no foreseeable extra data.
