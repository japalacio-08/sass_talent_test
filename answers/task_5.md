# Task 5: Person is not being created

[< Back to solutions menu](../readme.md)

Someone points out that even though a User is being created, a Person isn't being created. How would you go about troubleshooting it?

## Solution

1. Ensure that `after_create :create_person` callback is present in `User` model.

2. Use always `create!` instead of `create` to ensure that an exception is raised if the record is invalid.

3. Ensure that `Person` model has a validation for `name` field.

4. Ensure that `Person` model is receiving all the valid parameters from `User` model.

5. Check the logs to see if there is any error.

6. Manual testing using `rails console`:

```ruby
rails console
User.create(name: "Test User", active: true)
```

After runing this, check if a `Person` record was created.
