# Edit ./config/routes.rb
```rb
  devise_for :users, :skip => [:registrations], controllers: {
    sessions: 'users/sessions',
  }
  as :user do
    get 'users/edit' => 'devise/registrations#edit', :as => 'edit_user_registration'
    put 'users' => 'devise/registrations#update', :as => 'user_registration'
  end

# And then modify the app/views/devise/shared/_links.erb
```
