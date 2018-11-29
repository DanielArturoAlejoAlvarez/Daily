# Daily
## Description

This repository is a Software of Application with Python.

## Installation
Using Django 2.0 preferably.

## Usage
```html
$ git clone https://github.com/DanielArturoAlejoAlvarez/Daily.git [NAME APP] 

$ npm start
```
Follow the following steps and you're good to go! Important:


![alt text](https://i.imgur.com/JlfC7Eh.gif)


## Coding

### Model 

```python
...
class Todo(models.Model):
    text=models.CharField(max_length=100)
    complete=models.BooleanField(default=False)

    def __str__(self):
        return self.text
...
```

### Urls

```python
...
from django.urls import path
from . import views

urlpatterns = [    
    path('add', views.addTodo, name='add')
]
...
```

### Views

```python
...
from django.views.decorators.http import require_POST

@require_POST
def addTodo(request):
    form=TodoForm(request.POST)

    #print(request.Post['text'])
    if form.is_valid():
        new_todo=Todo(text=request.POST['text'])
        new_todo.save()

    return redirect('index')
...
```

### Form

```python
...
from django import forms 

class TodoForm(forms.Form): 
    text=forms.CharField(
        max_length=100, 
        widget=forms.TextInput(
            attrs={
                'class': 'form-control', 
                'placeholder': 'Enter todo e.g Delete junk files', 
                'aria-label': 'Todo', 
                'aria-describedby': 'add-btn'
            }
        ))
...
```

### Template 

```html
...
<form action="{% url 'add' %}" method="POST" role="form">
    {% csrf_token %}
    <div class="form-group">
        <div class="input-group">
            {{ form.text }}
            <span class="input-group-append">
                <button class="btn btn-success" id="add-btn">ADD</button>
            </span>

            
        </div>
        <div class="form-group mt-2">
            <a href="{% url 'deletecomplete' %}"><button type="button" class="btn btn-primary btn-lg btn-block"><i class="fas fa-times-circle"></i> Delete Complete</button></a>
            <a href="{% url 'deleteall' %}"><button type="button" class="btn btn-secondary btn-lg btn-block"><i class="fas fa-minus-circle"></i> Remove All Items</button></a>
        </div>
        
    </div>
</form>
...
```


## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/DanielArturoAlejoAlvarez/Daily. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).