# Initializing
```sh
rails g scaffold pin title
rails active_storage:install
rails db:migrate
rails g action_text:install
# ensure image_processing is in gem file
sudo apt-get update
sudo apt install libvips
# or sudo apt install imagemagick
```

# Optional Switch to Vips
in ./config/environments/development.rb
```rb
config.active_storage.variant_processor = :mini_magick
```

# Model/pin.rb
```rb
class Pin < ApplicationRecord
  has_one_attached :image
  has_many_attached :pictures
  has_rich_text :body
end
```

# controllers/pin_controller.rb
```rb
    # Only allow a list of trusted parameters through.
    def pin_params
      params.require(:pin).permit(:title, :body, :image, pictures: [])
    end
```

# views/pins/_form.html.erb
```erb
    <div>
      <%= form.rich_text_area :body %>
    </div>

    <div>
      <%= form.label :image %>
      <%= form.file_field :image %>
    </div>
  
    <div>
      <%= form.label :pictures %>
      <%= form.file_field :pictures, multiple: true %>
    </div>
```
