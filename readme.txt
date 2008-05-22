This paginator works in tandem with render_to decorator which can be found 
http://hg.piranha.org.ua/byteflow/file/tip/apps/lib/decorators.py#l6

Example usage:


settings.py
___________
INSTALLED_APPS += ('paginator', )   # for templates and templatetags


views.py
________
from app.models import Model
from lib.decorators import render_to
from paginator import paginate


@render_to('template.html')
@paginate()
def some_view(request):
     return {'some_list': Model.objects.all()}



template.html
_____________
{% load paginatortags %}
<ul>
{% for entry in object_list %}    <!-- important! iterable object should be named object_list -->
    <li>{{ entry }}</li>
{% endfor %}
</ul>

{% paginator %}



styles.css
__________
#paginator {
    margin: 25px 0px; 
    text-align: center;
}
    #paginator ul li {
        display: inline;
        background-image: none;
        padding: 0px 3px;
        margin: 1px;
        text-align: center;
        border: 1px solid black;

    }
        #paginator ul li.current {
            border: 1px solid #ccc;
        }
        #paginator ul li.nav { 
            border: 0px;
            margin: 3px;
        }
        #paginator ul li.nav a { 
            font: normal 10px Verdana;
        }
