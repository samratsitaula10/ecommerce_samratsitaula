# Objectives:

* preparing tempalates for Djanngo
* creating another template and extending the base template.

# Introduction

    A Django template is a text document or a Python string marked-up using the Django template language. Some constructs are recognized and interpreted by the template engine. The main ones are variables and tags.

    A template is rendered with a context. Rendering replaces variables with their values, which are looked up in the context, and executes tags. Everything else is output as is.

The syntax of the Django template language involves four constructs.

* Variables
* Tags
* Filters
* Comments

# Procedure:

1. Create a directory named templates and add a base template file named "base.html".

        <!DOCTYPE html>
        <html lang="en">
        <head>
        
            <!-- Bootstrap icons-->
            <link href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.5.0/font/bootstrap-icons css" rel="stylesheet" />
            <!-- Core theme CSS (includes Bootstrap)-->
            {% comment %} <link href="css/styles.css" rel="stylesheet" /> {% endcomment %}
            <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">

            <script src="https://code.jquery.com/jquery-3.2.1.slim.min.js" integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN" crossorigin="anonymous"></script>
            <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.9/umd/popper.min.js" integrity="sha384-ApNbgh9B+Y1QKtv3Rn7W3mgPxhU9K/ScQsAP7hUibX39j7fakFPskvXusvfa0b4Q" crossorigin="anonymous"></script>
            <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js" integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl" crossorigin="anonymous"></script>


            <!-- Libraries Stylesheet -->
            <link rel="stylesheet" type="text/css" href="{% static 'css/styles.css' %}" />
            
            <title>{% block title %} Electronics Commerce {% endblock %}</title>
            <style type="text/css">
                .min-h-100 {
                min-height: 100%;
            }
            </style>
        </head>
        <body>
            <!-- Navigation-->
            <nav class="fixed-top navbar navbar-expand-lg navbar-light bg-light">
                <div class="container px-4 px-lg-5">
                    <a class="navbar-brand" href="#!">E-Commerce</a>
                    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation"><span class="navbar-toggler-icon"></span></button>
                    <div class="collapse navbar-collapse" id="navbarSupportedContent">
                        <ul class="navbar-nav me-auto mb-2 mb-lg-0 ms-lg-4">
                            <li class="nav-item"><a class="nav-link active" aria-current="page" href="#!">Home</a></li>
                            <li class="nav-item dropdown">
                                <a class="nav-link dropdown-toggle" id="navbarDropdown" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false">Members</a>
                                <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                                
                                    <li><a class="dropdown-item" href="/admin/"><i class="bi bi-person-circle" aria- hidden="true"></i>Admin</a></li>
                                    <li><hr class="dropdown-divider" /></li>
                                    <li><a class="dropdown-item" href="/">Product</a></li>
                                    <li><a class="dropdown-item" href="/cart/"><i class="bi-cart-fill me-1" aria- hidden="true"></i>Cart</a></li>
                                
                                </ul>
                            </li>
                            <li class="nav-item dropdown">
                                <a class="nav-link dropdown-toggle" id="navbarDropdown" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false">Shop</a>
                                <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                                {% block categories %}
                                    <li><a class="dropdown-item" href="/">All Product</a></li>
                                    <li><hr class="dropdown-divider" /></li>
                                    <li><a class="dropdown-item" href="#!">Categories</a></li>
                                    <li><a class="dropdown-item" href="#!">Brand</a></li>
                                    {% endblock %}
                                </ul>
                            </li>
                        </ul>
                        
                        <div class="dropdown">
                            <button type="submit" class="btn dropdown" id="navbarDropdown" data-bs-toggle="dropdown" aria-expanded="false"><i class="bi bi-search"></i></button>
                            
                            <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                                <li><a class="dropdown-item" href="#!">
                                    {% block search %}                            
                                    <form class="d-flex" role="search" method="POST">
                                    <input class="form-control me-2" type="search" placeholder="Search / enter price" aria-label="Search" value="{{search_query}}">
                                    </form>
                                    {% endblock %}
                                </a></li>
                            </ul>  
                        </div>
                        

                        {% block cart %} 
                        <form class="d-flex">
                            <button class="btn btn-outline-dark" type="submit">
                                <i class="bi-cart-fill me-1"></i>
                                Cart
                                <span class="badge bg-dark text-white ms-1 rounded-pill">0</span>
                            </button>
                        </form>
                        {% endblock %} 
                    </div>
                </div>
            </nav>


            <div class="head">
            </div>


            <!-- Product section-->
            <section class="py-5">
                {% block Product_section %}

                {% endblock %} 
            </section>

            {% block content %}
                <!-- Related items section-->
            <section class="py-5 bg-light">

            </section>
            {% endblock %}

            {% block cart_section%}
            
            {% endblock %}

            <!-- Footer-->
            <footer class="py-5 bg-dark">
                <div class="container"><p class="m-0 text-center text-white">Copyright &copy; Your Website 2022</p></div>
            </footer>
            <!-- Bootstrap core JS-->
            <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js"></script>
            <!-- Core theme JS-->
            <script src="{% static 'js/scripts.js' %}"></script>

            </body>
        </html>



2. in setting.py add the following code:

        TEMPLATES = [
            {
                'BACKEND': 'django.template.backends.django.DjangoTemplates',
                'DIRS': [BASE_DIR / 'templates'],
                .......
            }
        ]
    

3. Inside “product_module”, create a directory “templates”. Create a html “index.html” and add the following code:

        {% extends "base.html" %} 
        {% load static %}
        {% block title %} E-Commerce {% endblock %} 

        <!--/.Navbar Categories and Product-->

        {% block categories %}
            
        <li><a class="dropdown-item" href="/">All Products</a></li>
        <li><hr class="dropdown-divider" /></li>
        {% for category in categories %}
        <li><a class="dropdown-item" href="/?category={{category.id}}">{{category.name}}</a></li>
        {% endfor %}
        {% for brand in brands %}
        <li><a class="dropdown-item" href="/?brand={{brand.id}}">{{brand.name}}</a></li>
        {% endfor %}

        {% endblock %}

        {% block search %}                            
            <form class="d-flex" role="search" method="POST">
            {% csrf_token %}
            <input name= "query" class="form-control me-2" type="search" placeholder="Search / enter price price -range" aria-label="Search" value="{{search_query}}">
            </form>

        
        {% endblock %}

        {% block cart %} 
                <form class="d-flex">
                <a href="#cart-model" data-toggle="modal">
                    <button class="btn btn-outline-dark" type="submit">
                        <i class="bi-cart-fill me-1"></i>
                        Cart
                        <span class="badge bg-dark text-white ms-1 rounded-pill">{{cart_items|length}}</span>
                    </button>
                </a>
                </form>
        {% endblock %}

        {% comment %} Nav-bar end {% endcomment %}

        {% block Product_section %} 
        {% for product in products %}
            <div class="container px-4 px-lg-5 my-5">
                <div class="row gx-4 gx-lg-5 align-items-center">
                    <div class="col-md-6"><img class="card-img-top mb-5 mb-md-0" src="{{ product.image_url }}" alt="{{ product.name }}" /></div>
                    <div class="col-md-6">
                        <div class="small mb-1">{{ product.brand.name }} </div>
                        <h1 class="display-5 fw-bolder">{{ product.name }}</h1>
                        <div class="fs-5 mb-5">
                            <span class="text-decoration-line-through">$45.00</span>
                            <span>$. {{ product.price }}</span>
                        </div>
                        <p class="lead">Lorem ipsum dolor sit amet consectetur adipisicing elit. Praesentium at dolorem quidem modi. Nam sequi consequatur obcaecati excepturi alias magni, accusamus eius blanditiis delectus ipsam minima ea iste laborum vero?</p>
                        <div class="d-flex">
                        <form class="d-flex" action="/cart" method="GET">
                            <!-- Default input -->
                            <input type="hidden" name="id" value="{{product.id}}" />
                            <input type="number" name="qty" value="1" aria-label="Search" type="num"
                            id="inputQuantity" class="form-control text-center me-3" style="max-width: 6rem"/>
                            
                            <button class="btn btn-outline-dark flex-shrink-0" type="submit" data-toggle="modal" data-target="#cart-model">
                                <i class="bi-cart-fill me-1"></i>
                                Add to cart
                            </button>
                        </form>
                        </div>
                        <br/>
                        <div class="col-md-12">
                        <table class="table table-sm table-bordered table-responsive ">
                            <tr>
                            <td>Available Quantity</td>
                            <td>Color Code</td>
                            <td>Brand</td>
                            <td>Category</td>
                            <td>Registered On</td>
                            <td>Is Active</td>
                            
                            </tr>
                            <tr>
                            <td>{{product.quantity}}</td>
                            <td>
                                <div
                                style="height: 25px; width: 25px; background-color: {{ product.color_code }};"
                                ></div>
                            </td>
                            <td>{{ product.brand.name }}</td>
                            <td>{{ product.category.name }}</td>
                            <td>{{ product.registered_on }}</td>
                            <td>
                                {% if product.is_active %}
                                <input type="checkbox" checked />
                                {% else %}
                                <input type="checkbox" />
                                {% endif %}
                            </td>
                            </tr>
                            
                        </table>
                        </div>
                    </div>
                </div>
            </div>
        {% endfor %}
        {% endblock %}

        {% block content %}


        {% for product in products %}

        {% endfor %} {% endblock %}




4. in views.py add the follwoing code:

        from django.db.models import Q
        from .models import Product, Brand, Category, CartItem
        def index(request):
            if request.method == "GET":
                category_id = request.GET.get("category")
                brand_id = request.GET.get("brand")
                if category_id:
                    filter_query = Q(category__id=category_id)
                    products = Product.objects.filter(filter_query)
                elif brand_id:
                    filter_query = Q(brand__id=brand_id)
                    products = Product.objects.filter(filter_query)
                else:
                    products = Product.objects.all()
                

                categories = Category.objects.all()

                brands = Brand.objects.all()
                context = {
                    'products': products,
                    'categories': categories,
                    'brands': brands,
                    'search_query': '',
                }

                return render(request, 'index.html', context)

            elif request.method == "POST":
                q = request.POST.get("query")
                if "-" in q:
                    price_values = q.split("-")
                    filter_query = Q(price__gte=price_values[0]) & Q(price__lte=price_values[1])
                else:
                    filter_query = Q(name__icontains=q) | Q(price__icontains=q) | Q(brand__name__icontains=q)
                products = Product.objects.filter(filter_query)
                categories = Category.objects.all()
                brands = Brand.objects.all()
                context = {
                    'products': products,
                    'categories': categories,
                    'brands': brands,
                    'search_query': q,
            }

            return render(request, 'index.html', context)
    

5. In urls.py add the path:

        from django.contrib import admin
        from django.urls import path, include
        urlpatterns = [
            path('admin/', admin.site.urls),
            path('', include('product_module.urls')),
        ]
    

6. Run the server and check the output is correct or not.

    # Output: 



# Conclusion:

    Here in this lab session we understood how a base template is extended by another template and how to manupulate data and retrive from database using django.

