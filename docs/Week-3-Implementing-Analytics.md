# 3. Data Analytics
This week you will be querying the data in the database to build a basic analytics dashboard for this application. Again, let's not worry about verifying the QR codes just yet (that's next week's project).

## Step 1. The `/app/overview?course=xyz` View
An instructor can visit the `/app/overview?course=xyz`, this should load summary statistics about class attendance for the course associated with the code `xyz`. This view should only load if the user is logged in and they are an instructor. If not logged in, redirect the user too the login view `/accounts/login`.

These summary statistics should have:
1. The class name/number printed at the top
2. The total number of students in the class
3. For each class meeting, you should have the fraction of students with any image uploaded.
 
## Step 2. The `/app/student?course=xyz` View
An instructor can visit the `/app/student?course=xyz`, this should load specific stats for a student in a course code `xyz`. This view should only load if the user is logged in and they are an instructor. If not logged in, redirect the user too the login view `/accounts/login`.

These statistics should have:
1. The class name/number printed at the top
2. For each class meeting, whether the student has an uploaded image or not.

## Step 3. Testing Plan (Write Below)
*As you add more functionality to the application, testing becomes much harder. Write a detailed plan on how you are testing all of this functionality.*

Testing the application is a crucial step in its development, because we require it to make sure everything is working as expected. However, as the program becomes more complex, it also requires more intricate testing. Thus, while manual testing is extremely useful during the first stages, creating a way to systematically test the application is eventually a necessity. Fortunately, in the design of AttendanceChimp we implemented the use of mixins which are inherited by models and forms. This simplifies the process by reducing the number of objects and features that need to be individually tested.

We then begin by writing tests for the mixins that define access to the models and forms of the application. `ModelAccessMixinTest`, that inherits `TestCase` from Django’s testing framework, will first generate a sample model containing test values. Then, it will contain testing functions that verify the behavior of their respective methods in `ModelAccessMixin`, which are `get_length`, `get_value`, and `get_model`. This will be done by using `assertRaises`, that confirms that the correct error is raised every time an invalid value is introduced in the model. Similarly, `FormAccessMixinTest` will perform these tasks, but focusing on a mock request object and a sample form instead of a model.

Now, we need to find a way to systematically introduce invalid values to the models and test how they respond. We will accomplish this by developing `test_invalid_field`, which receives a type of model and its attributes as arguments and creates the instance that will be tested. Then, this function iterates over every attribute in the model and introduces invalid values to assert that the instance fails validation.

This `test_invalid_field` function will be used when writing tests for the `Profile` and `Course` Models. For both models we will create dictionaries containing possible valid and invalid values for each attribute. Finally, will pass these attributes to the function and verify that validation is in fact failed and the correct alerts are raised.

## Step 4. Implement (Step 3)
Implement Step 3 in code and include the results with your submitted pull request. 
