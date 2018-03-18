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
