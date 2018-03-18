# 才华横溢 workout_log 案例 8
```
cd workspace
rails new workout_log
cd workout_log
rails s
```
![image](https://ws3.sinaimg.cn/large/006tKfTcgy1fpgpkeefzwj31720zi1kx.jpg)

```
git init
git add .
git commit -m "initial commit"
git remote add origin https://github.com/shenzhoudance/workout_log.git
git push -u origin master
```
```
git checkout -b model workout
rails g model workout date:datetime workout:string mood:string length:string
rake db:migrate
```
![image](https://ws2.sinaimg.cn/large/006tKfTcgy1fpgptkw61gj31a00gqadi.jpg)

rails g controller workouts
![image](https://ws4.sinaimg.cn/large/006tKfTcgy1fpgpy5916nj31a20e076a.jpg)
```
config/routes.rb
---
Rails.application.routes.draw do
  resources :workouts
  root 'workouts#index'
end
---
rails s
```
![image](https://ws4.sinaimg.cn/large/006tKfTcgy1fpgq1kkdhgj31300baab3.jpg)

```
app/controllers/workouts_controller.rb
---
class WorkoutsController < ApplicationController
  def index
  end
end
---
```
![image](https://ws2.sinaimg.cn/large/006tKfTcgy1fpgq4y0ev0j31kw0l1gt7.jpg)
```
app/views/workouts/index.html.erb
---
<h1>欢迎来到才华横溢的世界</h1>
```
![image](https://ws1.sinaimg.cn/large/006tKfTcgy1fpgq9fom2oj313a09ywfc.jpg)

```
git add .
git commit -m "add workout controller index & routes"
```
```
git checkout -b gem
https://rubygems.org/
gem 'haml', '~> 5.0', '>= 5.0.4'
gem 'bootstrap-sass', '~> 3.3', '>= 3.3.7'
gem 'simple_form', '~> 3.5', '>= 3.5.1'
bundle install
rails server
---
https://github.com/twbs/bootstrap-sass
app/assets/stylesheets/application.css.scss
---
@import "bootstrap-sprockets";
@import "bootstrap";
---
app/assets/javascripts/application.js
//= require bootstrap-sprockets
//= require turbolinks
---
https://github.com/plataformatec/simple_form
rails generate simple_form:install --bootstrap
---
app/views/jobs/index.html.haml
%h1 欢迎来到才华横溢的领域
rails server
```
![image](https://ws1.sinaimg.cn/large/006tKfTcgy1fpgqkr5o1jj310o096gmk.jpg)

```
app/controllers/workouts_controller.rb
---
class WorkoutsController < ApplicationController
  def index
  end

  def show
  end

  def new
  end

  def create
  end

  def edit
  end

  def update
  end

  def destroy
  end

  private

  def workout_params
  end

  def find_workout
  end
end
---
class WorkoutsController < ApplicationController
  def index
  end

  def show
  end

  def new
    @workout = Workout.new
  end

  def create
    @workout = Workout.new(workout_params)
    if @workout.save
      redirect_to @workout
    else
      render 'new'
    end
  end

  def edit
  end

  def update
  end

  def destroy
  end

  private

  def workout_params
    params.require(:workout).premit(:date,:workout,:mood,:length)
  end

  def find_workout
  end
end

---
rails s
http://localhost:3000/workouts/new
```
![image](https://ws4.sinaimg.cn/large/006tKfTcgy1fpgqvpq9gmj31kw0ncjyn.jpg)
```
app/views/workouts/_form.html.haml
---
= simple_form_for(@workout, html: { class: 'form-horizontal' }) do |f|
	= f.input :date, label: "Date"
	= f.input :workout, label: "What area did you workout?", input_html: { class: "form-control" }
	= f.input :mood, label: "How were you feeling?", input_html: { class: "form-control" }
	= f.input :length, label: "How long was the workout?", input_html: { class: "form-control" }
	%br/
	= f.button :submit
---
app/views/workouts/new.html.haml
---
%h1 new workout

= render 'form'

= link_to "cancel", root_path
---
rails s
http://localhost:3000/workouts/new
```
![image](https://ws1.sinaimg.cn/large/006tKfTcgy1fpgri0i7fij31cg0ssdib.jpg)

```
app/views/workouts/show.html.haml
---
#workout
	%p= @workout.date
	%p= @workout.workout
	%p= @workout.mood
	%p= @workout.length



= link_to "Back", root_path
= link_to "Edit", edit_workout_path(@workout)
= link_to "Delete", workout_path(@workout), method: :delete, data: { confirm: "Are you sure?" }
---
rails s
http://localhost:3000/workouts/1
```
![image](https://ws4.sinaimg.cn/large/006tKfTcgy1fpgrsh663zj31kw0jowhz.jpg)
```
app/controllers/workouts_controller.rb
---
class WorkoutsController < ApplicationController

  before_action :find_workout, only: [:show, :edit, :update, :destroy]

  def index
  end

  def show
  end

  def new
    @workout = Workout.new
  end

  def create
    @workout = Workout.new(workout_params)
    if @workout.save
      redirect_to @workout
    else
      render 'new'
    end
  end

  def edit
  end

  def update
  end

  def destroy
  end

  private

  def workout_params
    params.require(:workout).permit(:date,:workout,:mood,:length)
  end

  def find_workout
    @workout = Workout.find(params[:id])
  end
end
---
```
![image](https://ws4.sinaimg.cn/large/006tKfTcgy1fpgs1bwgexj30iw0cejs1.jpg)

```
---
app/views/workouts/index.html.haml
---
%h1 欢迎来到才华横溢的领域

- @workouts.each do |workout|
	%p= workout.date
	%p= workout.workout
---
app/controllers/workouts_controller.rb
---
def index
  @workouts = Workout.all.order("create_at DESC")
end
---
```
![image](https://ws1.sinaimg.cn/large/006tKfTcgy1fpgsnp8661j30qc0d6myg.jpg)

```
---
app/views/workouts/index.html.haml
---
%h1 欢迎来到才华横溢的领域

- @workouts.each do |workout|
	%h2= link_to workout.date,workouts
	%h3= workout.workout
---
rake routes
```
![image](https://ws4.sinaimg.cn/large/006tKfTcgy1fpgsqato1vj30sc0ikjte.jpg)

```
app/controllers/workouts_controller.rb
---
def update
  if @workout.update(workout_params)
    redirect_to @workout
  else
    render 'edit'
end

def destroy
  @workout.destroy
  redirect_to root_path
end
```
![image](https://ws1.sinaimg.cn/large/006tKfTcgy1fpgzs6r2k6j30wi0emgn2.jpg)
![image](https://ws1.sinaimg.cn/large/006tKfTcgy1fpgzryb2dnj30m80baaao.jpg)
![image](https://ws1.sinaimg.cn/large/006tKfTcgy1fpgzrm2zx7j31860s2q5a.jpg)
![image](https://ws1.sinaimg.cn/large/006tKfTcgy1fpgzr6qk9rj30xg0s80uz.jpg)---
```
https://getbootstrap.com/docs/3.3/css/
https://getbootstrap.com/docs/3.3/components/
---
app/views/layouts/application.html.haml
---
!!!
%html
%head
	%title Workout Log Application
	= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track' => true
	= javascript_include_tag 'application', 'data-turbolinks-track' => true
	= csrf_meta_tags
%body
	%nav.navbar.navbar-default
		.container
			.navbar-header
				= link_to "Workout Log", root_path, class: "navbar-brand"
			.nav.navbar-nav.navbar-right
				= link_to "New Workout", new_workout_path, class: "nav navbar-link"

	.container
		= yield

```
```
app/assets/stylesheets/application.scss
---
@import "bootstrap-sprockets";
@import "bootstrap";

html {
	height: 100%;
}

body {
	background: -webkit-linear-gradient(90deg, #616161 10%, #9bc5c3 90%); /* Chrome 10+, Saf5.1+ */
  background:    -moz-linear-gradient(90deg, #616161 10%, #9bc5c3 90%); /* FF3.6+ */
  background:     -ms-linear-gradient(90deg, #616161 10%, #9bc5c3 90%); /* IE10 */
  background:      -o-linear-gradient(90deg, #616161 10%, #9bc5c3 90%); /* Opera 11.10+ */
  background:         linear-gradient(90deg, #616161 10%, #9bc5c3 90%); /* W3C */
}

.navbar-default {
	background: rgba(250, 250, 250, 0.5);
	-webkit-box-shadow: 0 1px 1px 0 rgba(0,0,0,.2);
	box-shadow: 0 1px 1px 0 rgba(0,0,0,.2);
	border: none;
	border-radius: 0;
	.navbar-header {
		.navbar-brand {
			color: white;
			font-size: 20px;
			text-transform: uppercase;
			font-weight: 700;
			letter-spacing: -1px;
		}
	}
	.navbar-link {
		line-height: 3.5;
		color: rgb(48, 181, 199);
	}
}

#index_workouts {
	h2 {
		margin-bottom: 0;
		font-weight: 100;
		a {
			color: white;
		}
	}
	h3 {
		margin: 0;
		font-size: 18px;
		span {
			color: rgb(48, 181, 199);
		}
	}
}
```
![image](https://ws2.sinaimg.cn/large/006tKfTcgy1fph02y293uj31kw0n4gxe.jpg)

```
git checkout -b exercise
rails g model exercise name:string sets:integer reps:integer workout:references
rake db:migrate
```
![image](https://ws4.sinaimg.cn/large/006tKfTcgy1fph09ywsuyj31bk0i20xd.jpg)
```
app/models/workout.rb
---
class Workout < ApplicationRecord
  has_many :exercises
end
---
rake routes
```
![image](https://ws2.sinaimg.cn/large/006tKfTcgy1fph0euidpij31540eyjvd.jpg)
```
rails g controller exercises
---
class ExercisesController < ApplicationController
 def create
   @workout = Workout.find(params[:workout_id])
   @exercises = @workout.exercises.create(params[:exercise].permit(:name, :sets, :reps))

   redirect_to workout_path(@workout)
 end
end
---
app/views/exercises/_form.html.haml
---

= simple_form_for([@workout, @workout.exercises.build]) do |f|
	= f.input :name, input_html: { class: "form-control" }
	= f.input :sets, input_html: { class: "form-control" }
	= f.input :reps, input_html: { class: "form-control" }
	%br/
	= f.button :submit

---
app/views/exercises/_exercises.html.haml
---
%p= exercise.name
%p= exercise.sets
%p= exercise.reps
---
```
![image](https://ws3.sinaimg.cn/large/006tKfTcgy1fph0yff4ryj31kw0s6tpk.jpg)

```
https://hackhands.com/format-datetime-ruby/
```
![image](https://ws3.sinaimg.cn/large/006tKfTcgy1fph2buermzj31kw0m2ncv.jpg)
![image](https://ws3.sinaimg.cn/large/006tKfTcgy1fph2box5ssj31kw0jmna5.jpg)
![image](https://ws4.sinaimg.cn/large/006tKfTcgy1fph2bfeyzkj31kw0qvdwz.jpg)
![image](https://ws2.sinaimg.cn/large/006tKfTcgy1fph2ah4vfhj31kw0q57km.jpg)
