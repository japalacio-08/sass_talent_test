# Task 4: Create Person afer create User.

[< Back to solutions menu](../readme.md)

Let’s create another model, ‘Person’, with two fields: name and active, just like the User model. Any time a user is added, it needs to be added to Person as well.
Let's add another method to ApiController called create. We will create a User with your name and active set to true. Please add it to Person after you create a User.

## Solution

1. Create new model

```bash
rails generate model Person name:string active:boolean
```

2. Run migrations

```bash
rails db:migrate
```

3. Add `after_create` callback to `User` model

```ruby
# app/models/person.rb

class Person < ApplicationRecord
  validates :name, presence: true
end
```

```ruby
# app/models/user.rb

class User < ApplicationRecord
  validates :name, presence: true

  scope :active, -> { where(active: true) }

  after_create :create_person

  private

  def create_person
    Person.create!(name: name, active: active)
  end
end
```

4. Add `create` action to `ApiController`

```ruby
# app/controllers/concerns/active_users_setter.rb

module ActiveUsersSetter
  extend ActiveSupport::Concern

  included do
    before_action :set_active_users
  end

  private

  def set_active_users
    @active_users = User.active_users
  end
end
```

```ruby
# app/controllers/api_controller.rb

class ApiController < ApplicationController
  include ActiveUsersSetter

  def index
    render json: @active_users
  end

  def create
    user = User.create!(user_params)
    render json: { message: 'User created successfully' }, status: :created
  rescue ActiveRecord::RecordInvalid => e
    render json: { message: e.message }, status: :bad_request
  rescue StandardError => e
    render json: { message: e.message }, status: :internal_server_error
  end

  private

  def user_params
    params.require(:user).permit(:name, :active)
  end
end

```

```ruby
# config/routes.rb
Rails.application.routes.draw do
  namespace :api do
    resources :users, only: [:index, :create]
  end
end
```
