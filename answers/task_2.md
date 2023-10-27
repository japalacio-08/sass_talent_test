# Task 2: Rails Components

[< Back to solutions menu](../readme.md)

Within Rails, we have a model named ‘User’. The User table has only 2 relevant fields: ‘name’ (string) and ‘active’ (boolean). We have two controllers with index methods where we need to find active users (SessionController and ApiController). Write simple code for all three classes (2 or 3 liner codes ) (1 model, 2 controllers ).  You don’t need to worry about security etc.

## Solution

### Model

```ruby
# app/models/user.rb

class User < ApplicationRecord
  validates :name, presence: true

  scope :active, -> { where(active: true) }
end
```

### Concern

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

### Controllers (SessionController and ApiController)

```ruby
# app/controllers/session_controller.rb

class SessionController < ApplicationController
  include ActiveUsersSetter

  def index
    render json: @active_users
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
end
```
