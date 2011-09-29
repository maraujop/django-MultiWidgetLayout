# django-MultiWidgetLayout

* Author: <a href="http://www.github.com/maraujop/">Miguel Araujo</a>
* Licence: BSD

## Usage

This is an enhanced class based on `MultiWidget` that lets you control the rendering of a subclass using a layout specified by a list. Let's see an example first:

    class AddressWidget(MultiWidgetLayout):
        def __init__(self, attrs=None):
            layout = [ 
                "<label for='%(id)s'>Street:</label>", TextInput()
                "<label for='%(id)s'>Number:</label>", TextInput(),
                "<label for='%(id)s'>Zip Code:</label>", TextInput()
            ]
            super(AddressWidget, self).__init__(layout, attrs)

        def decompress(self, value):
            if value:
                return value.split(",")
            return [None, None, None]

This is what you get:

    <label for='id_address_field_0'>Street:</label>
    <input id="id_address_field_0" type="text" name="address_field_0" class="addresswidget" />
    <label for='id_address_field_1'>Number:</label>
    <input id="id_address_field_1" type="text" name="address_field_1" class="addresswidget" />
    <label for='id_address_field_2'>Zip Code:</label>
    <input id="id_address_field_2" type="text" name="address_field_2" class="addresswidget" />

Compared to `MultiWidget`, the differences are:

* `widgets` parameter no longer exists.
* `layout` The layout is a list of strings and widgets that will be rendered. They are rendered in that exact order. String will be formatted using the dictionary `attrs`.

## Bugs or Suggestions

This is an experiment to improve the rendering of MultiWidgets. I have openned <a href="https://code.djangoproject.com/ticket/16959">a ticket in Django (#16959)</a> to see if the concept is accepted, meanwhile you can use this. If you have suggestions or you come across bugs, please open an issue.
