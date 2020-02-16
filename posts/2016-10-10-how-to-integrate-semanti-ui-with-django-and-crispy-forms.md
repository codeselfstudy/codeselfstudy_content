---
title: How to Integrate Semantic UI with Django and Crispy Forms
date: 2016-10-10
---

This post explains how to integrate <a href="http://semantic-ui.com/">Semantic UI</a> with <a href="https://www.djangoproject.com/">Django's</a> <a href="http://django-crispy-forms.readthedocs.io/en/latest/">Crispy Forms</a>. After a lot of troubleshooting, it started working. It should be possible to improve parts of this process in the future, but it works for now.

<h2>Step 1</h2>

Install Crispy Forms. See <a href="http://django-crispy-forms.readthedocs.io/en/latest/install.html">the docs</a> for instructions.

<h2>Step 2</h2>

I downloaded <a href="https://github.com/acidjunk/crispy-forms-semanticUI-templates">this code</a> from Github. Save it in <code>templates/semantic-ui/</code>.

<h2>Step 3</h2>

Put this code in settings.py:

```python
CRISPY_TEMPLATE_PACK = 'semantic-ui'
CRISPY_ALLOWED_TEMPLATE_PACKS = ('semantic-ui')
```

<h2>Step 4</h2>

Create a form in one of your Django apps. The example below is modified from the Crispy Forms docs.

```python
from django import forms
from crispy_forms.helper import FormHelper
from crispy_forms.layout import Submit


class ExampleForm(forms.Form):

    def __init__(self, *args, **kwargs):
        super(ExampleForm, self).__init__(*args, **kwargs)
        self.helper = FormHelper()
        self.helper.form_id = 'someId'
        self.helper.form_class = 'some-class'
        self.helper.form_method = 'post'
        self.helper.form_action = 'sample_form_name'

        # Note that the submit button is added separately, with a Semantic UI class.
        self.helper.add_input(Submit('submit', 'Submit',
                              css_class='ui button'))

    like_website = forms.TypedChoiceField(
        label='Do you like this website?',
        choices=((1, 'Yes'), (0, 'No')),
        coerce=lambda x: bool(int(x)),
        widget=forms.RadioSelect,
        initial='1',
        required=True,
    )

    favorite_food = forms.CharField(
        label='What is your favorite food?',
        max_length=80,
        required=True,
    )

    favorite_color = forms.CharField(
        label='What is your favorite color?',
        max_length=80,
        required=True,
    )

    favorite_number = forms.IntegerField(
        label='Favorite number',
        required=False,
    )

    notes = forms.CharField(
        label='Additional notes or feedback',
        required=False,
    )
```

<h2>Step 5</h2>

Update your view:

```python
def sample_form(request):
    context = {'form': ExampleForm}

    return render(request, 'someform/someform_create.html', context)
```

<h2>Step 6</h2>

Put the form in a template:

```
{% extends 'coreapp/layouts/main.html' %}
{% load crispy_forms_tags %}

{% block content %}
<div class="ui form">
    {% crispy form %}
</div>
{% endblock %}
```

<h2>All Done</h2>

If it doesn't work, or if you have suggestions for improvement, please comment below!

**Update:** a commenter in the old blog mentioned this tip on 2017-11-07:

> This can now be done even more easily with <a href="https://github.com/thetarkus/django-semanticui-forms">Django Semantic UI Forms</a>.  It even includes layout capability.