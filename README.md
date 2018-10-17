### Cocoon
---

https://github.com/nathanvda/cocoon

```
gem "cocoon"
rails g cocoon:install
rails g scaffold Project name:string description:string
rails g model Task description:string done:boolean project:belongs_to

```

```js
//= require cocoon

= javascirpt_include_tag :cocoon

$('#container').on('cocoon:before-insert', function(e, insertedItem){
  //
});

$(document).ready(function(){
  $('#owner')
    .on('cocoon:before-insert', function(){
      $("#owner_from_list").hide();
      $("#owner a.add_fields").hide();
    })
    .on('cocoon:after-insert', function(){})
    .on("", function(){})
    .on("", function(){});
  $()
    .on()
    .on()
    .on();
});


```

```ruby
class Project < ActiveRecord::Base
  has_many :tasks, inverse_of: :project
  accepts_nested_attributes_for :tasks, reject_if: :all_bank, allow_destory: true
end
class Task < ActiveRecord::Base
  belongs_to :project
end

def project_params
  params.require(:project).permit(:name, :description, tasks_attributes: [:id, :description, :done, :_destroy])
end



```

```
= sematic_form_for @project do |f|
  = f.inputs do
    = f.input :name
    = f.input :description
    %h3 Tasks
    #tasks
      = f.semantic_fields_for :tasks do |task|
        = render 'task_fileds', f: task
      .links
        = link_to_add_association 'add task', f, :tasks
    = f.actions do
      = f.action :submit
      
.neted-fields
  = f.input do
    = f.input :description
    = f.input :done, as: :boolean
    = link_to_remove_association "remove task", f

= simple_form_for @project do |f|
  = f.input :name
  = f.input :description
  %h3 Tasks
  #tasks
    = f.simple_fields_for :tasks do |tasks|
      = render 'task_fields', f: task
    .links
      = link_to_add_association 'add task', f, :tasks
  = f.submit

.nested-fields
  = f.input :description
  = f.input :done, as: :boolean
  = link_to_remove_association "remove task", f

= form_for @project do |f|
  .field
    = f.label :name
    %br
    = f.text_field :name
  .field
    = f.label :description
    %br
    = f.text_field :description
  %h3 Tasks
    = f.fields_for :tasks do |task|
      = render 'task_fields', f: task
    .links
      = link_to_add_association 'add task', f, :tasks
  = f.submit

.nested-fields
  .field
    = f.label :description
    %br
    = f.text_field :description
  .field
    = f.check_box :done
    = f.label :done
  = link_to_remove_association "remove task", f

= link_to_add_asociation 'add something', f, :something,
  render_options: { wrapper: 'incline' }

= link_to_add_association 'add something', f, :something,
  render_options: {locals: { sherlock: 'Holmes' }}

= link_to_add_asociation 'add something', f, :something,
  partial: 'shared/something_fields'

= link_to_add_association('add somehing', @form_obj, :comments,
  wrap_object: Proc.new {|comment| commentDecorator.new(comment) })
  
= link_to_add_association('add something', @form_obj, :comments,
  wrap_object: Proc.new { |comment| comment.name = current_user.name; comment })  

= link_to_add_association('add something', @form_obj, :comments,
  force_non_association_create: true)

= link_to_remove_association('remove this', @form_obj,
  { wrapper_class: 'my-wrapper-class' })

#owner
  #owner_from_list
    = f.associatoin :owner, collection: Person.all(order: 'name'), prompt: 'Choose an existing owner'
  = link_to_add_association 'add a new person as owner', f, :owner
  
```
