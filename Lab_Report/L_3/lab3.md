# Objectives:
    - To implement the search operations in the models.
    - Implement the image tag to store and display images in the product model.


# Introduction:
    Application search operates similarly to a standard search engine. Users can check their search results after typing in their query.


# Procedure:

    1. In 'admin.py' implement the following code:
     code:
     class ProductAdmin(admin.ModelAdmin):
         list_display = ["name", "price", "brand", "category",]
         search_fields = ["name", "price", "brand__name", "category__name",]
         list_filter = ["brand","category",]
         readonly_fields = ["quantity",]
         class Meta:
         model = Product
     admin.site.register(Product, ProductAdmin)

    In this code, the column designated as "search files" is used to implement a search for the brand table, whose primary key is used as a foreign key reference.


     2. Similarly, implement the same changes in other models as well:
          # Implementaion of search in the brand model:
          Codes: 
              class BrandAdmin(admin.ModelAdmin):
           list_display = ["name",]
           search_fields = ["name",]
           class Meta:
               model = Brand
               admin.site.register(Brand, BrandAdmin)

          # Implementation of search in the category model:
          Codes:
           class CategoryAdmin(admin.ModelAdmin):
               list_display = ["name",]
               search_fields = ["name",]
               class Meta:
                   model = Category
           admin.site.register(Category, CategoryAdmin)


      3. Add the field for displaying the image in the list view. For this add a field "image_tag" to the product class in the 'models.py' to enter the image URLs in the database.
         #import the mark_safe from the django.utils.html first:
            from django.utils.html import mark_safe

         # add the following code to add the image_url field in the model:
          Codes:
          class Product(models.Model):
               def image_tag(self):
                   return mark_safe(f'<img src="{self.image_url}" width="50" height="50" />')
               image_tag.short_description = "Product"
               def __str__(self):
                   return self.name

              the usage of mark_safe is to mark a custom string as a safe string for HTML/output rendering.


      4. In the class ProductAdmin in 'admin.py' implement the following changes:
        Codes:  
        class ProductAdmin(admin.ModelAdmin):
             list_display = ["image_tag", "name", "price", "brand", "category",]
             search_fields = ["name", "price", "brand__name", "category__name",]
             list_filter = ["brand","category","price",]
             # readonly_fields = ["quantity",]
             class Meta:
             model = Product
        admin.site.register(Product, ProductAdmin)

      5. Run the project and navigate to admin to check the result.
        python manage.py runserver



# Conclusion:
In this lab session, we learned how to connect a search engine to a specific module, insert images into the database by inputting the images' link URL, and show them in the list view.
