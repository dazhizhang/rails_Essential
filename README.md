# rails_Essential


rails new 
bundle install
rails server
////////////////////////////////////////////////////////////
Setaria
/////////////////////////////////////////////////////////////////////////////////
Setaria.find(1)
Setaria.create()
Setaria.last
Setaria.all().order(:order)
update :
z = Setaria.find(3)
z.playground = "Benny Hills Memorial"
z.save

delete:
Setaria.find(3).destroy

create a model:
class Setaria < ActiveRecord::Base
end

class Setaria < ActiveRecord::Base
  # insert validation here
  validates_presence_of :name
end

class Setaria < ActiveRecord::Base
  # insert validation here
  validates_uniqueness_of :name
end

class Setaria < ActiveRecord::Base
  # insert validation here
  validates :name, presence: true, uniqueness: true
end

class Tool < ActiveRecord::Base
  belongs_to :Setaria
end

class Setaria < ActiveRecord::Base
has_many :tools
end

class Tool < ActiveRecord::Base
belongs_to :Setaria
end

z = Setaria.find(1)
z.tools

<p>
<%= link_to Setaria.name, Setaria %>
</p>

<ul>
<% Setarias.each do |Setaria| %>
  <li><%= Setaria.name %></li>
<% end %>
</ul>

<ul>
  <% Setarias.each do |Setaria| %>
    <li>
      <%= link_to Setaria.name, edit_Setaria_path(Setaria) %>
    </li>
  <% end %>
</ul>

class SetariasController < ApplicationController
  def show
    # put the show code here
    @Setaria = Setaria.find(params[:id])
  end
end

class SetariasController < ApplicationController
  def show
    @Setaria = Setaria.find(params[:id])

    respond_to do |format|
      format.xml {render xml: @Setaria}
    end
  end
end

class SetariasController < ApplicationController
  def create
    @Setaria = Setaria.create(Setaria_params)
    redirect_to Setaria_path(@Setaria)
  end

  private

  def Setaria_params
    params.require(:Setaria).permit(:name, :playground)
  end
end



class SetariasController < ApplicationController
  before_action :find_Setaria
  before_action :check_tweets, only: :show

  def show
    render action: :show
  end

  def find_Setaria
    @Setaria = Setaria.find params[:id]
  end
  
  def check_tweets
    if @Setaria.tweets.size == 0
      redirect_to Setarias_path
    end
  end
  
end

TwitterForSetarias::Application.routes.draw do
  resources :Setarias
end

TwitterForSetarias::Application.routes.draw do
  get '/undead' => 'Setarias#undead'

end

TwitterForSetarias::Application.routes.draw do
  get '/undead', to: redirect('/Setarias')
end

TwitterForSetarias::Application.routes.draw do
  root to: 'Setarias#index'
end

TwitterForSetarias::Application.routes.draw do
  get '/Setarias/:name', to: 'Setarias#index', as: 'playground'
end
