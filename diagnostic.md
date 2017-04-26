# Rails API Relationships Diagnostic

Place your responses inside the fenced code-blocks where indivated by comments.

1.  Describe a reason why a join tables may be valuable.

  ```md
  You can use them for a many-to-many relationship, EG books and borrowers.
  Using a join table with a FK from each will allow you to get what you need
  from each table.
  ```

1.  Provide a database table structure and explain the Entity Relationship that
  describes a many-to-many relationship for `Profiles`, `Movies` and `Favorites`
  (Think of Netflix). A `Profile` has a `given_name`, `surname` and `email` and a
  `Movies` have `title`, `release_date`, and `length` and `Favorites` would be the
  join table with references to `Movies` and `Profiles`.

  ```md
  create_table "Profiles", force: :cascade do |t|
    t.string   "given_name",  null: false
    t.string   "surname", null: false
    t.string   "email"
    t.datetime "created_at",  null: false
    t.datetime "updated_at",  null: false
  end
    create_table "Movies", force: :cascade do |t|
      t.string   "title",  null: false
      t.string   "release_date", null: false
      t.string   "length"
      t.datetime "created_at",  null: false
      t.datetime "updated_at",  null: false
  end
      create_table "Favorites", force: :cascade do |t|
        t.string   "given_name",  null: false
        t.string   "surname", null: false
        t.string   "email"
        t.datetime "created_at",  null: false
        t.datetime "updated_at",  null: false
  end

add_foreign_key "favorites", "profiles"
add_foreign_key "favorites", "movies"
add_foreign_key "profiles", "movies"
  end
  ```

1.  For the above example, what needs to be added to the Model files?

  ```rb
  class Profile < ActiveRecord::Base

    #one to many
    belongs_to :somename, class_name: 'Movie', foreign_key: 'movie_id'

    #many to many
  has_many :movies, through: :favorites
  has_many :favorites, dependent: :destroy

    #validations

    validates :given_name, presence: true
    validates :surname, presence: true
  end
  end

  ```

  ```rb
  class Movie < ActiveRecord::Base
  end
  ```

  ```rb
  class Favorite < ActiveRecord::Base
  end
  ```

1.  What is the purpose of a serializer? What would our `Profile` serializer look
like to show all movies favorited by a profile on
`http://localhost:3000/profiles/1`

  ```md
    It helps ensure that the object is correctly created
  ```

  ```rb
  class ProfileSerializer < ActiveModel::Serializer
  end
  ```

1.  What would the command be to _scaffold_ out a **join table** for Favorites from
the above `Movies` and `Profiles`.

  ```sh
    # < Your Response Here >
  ```

1.  What is `Dependent: Destroy` and where/why would we use it?

  ```md
    It ensures relationship integrity.  If you have tables with records relating to one
    another, it ensures that you can't delete one piece without deleting the other.

    You put it in the class xxx < ApplicationRecord for the many-to-many references.
  ```

1.  Think of **ANY** example where you would have a one-to-many relationship as well
as a many-to-many relationship in an application. You only need to list the
description about the resources and how they relate to one another.

  ```md
    # < Your Response Here >
  ```
