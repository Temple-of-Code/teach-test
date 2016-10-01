Creating a Shop App from scratch with Rails
===========================================

1) From your projects or workspace directory (or home directory, wherever you like) in the terminal type:

```sh
rails new my-shop
```
(You can pick a better name than this - remember the rails convention is to seperate words with hypens `-` in the shell and in file names).

This will create a new directory called 'my-shop' and in it will be the structure and building blocks for your new app.

2) In the terminal, run:

```sh
bundle install
```

This installs the gems that make up your building blocks for your rails app.

Groovy! an app. Does it work? In your terminal (in the correct directory for your app) type:
```sh
rails server
```
to run the rails server. Then in your browser go to `localhost:3000`

If it says 'YAY! youre on rails! Then congratulations :)

3) Navigate to the app folder and open it in your text editor. Under the top directory - called 'app' - you will see the sub-directory 'controllers'. If you browse this you will see that it only contains a folder called 'concerns' (ignore this for now) and a file called `application_controller.rb`. This is one of the three *main* kinds of file that your app will have - the 'controller' in 'Model-View-Controller which is the architecture that rails apps are built on. 

Thing is, we want to have stuff in our app, stuff like a home page, maybe an about page or a contact details page... even before we do things like add products our shop needs these things. These things (home, about, contacts) are often called static pages, because the content in them doesn't change much (unlike your products page for example which you will update a lot). But we still need to be able to control these pages so we need a controller. We could call it static-pages controller, or we could call it shop controller, we can chose. To make our controller, in the terminal we type:

```sh
rails generate controller shop
```

(we could have typed `rails generate controller static-pages` too.

GREAT now in your controllers folder you should have a file called `shop_controller.rb`. So far, it is mostly empty. One of the main functions of a controller though, is to recieve input from the user (or client) and then decide which view is going to be sent as display output. 

In terms of the internet, the browser makes a request: 
'Hey I wanna see or do a thing' 
and the controller recieves that message and thinks:
'Ah, so its *that* thing that you want? Ok...'

(and then on the inside of the app, 
'Hmmm so their request corresponds *this* Action in the Route... what have I got for this? Ah here we are... This action says to render this View... 
'Hey! Views! Send this page to the display.'

The controller is kind of bossy. But as you can see from above, it needs Actions. Lets say that your user or client wants to see your home page they type that into their browser and this request comes in to your controller... Then the controller will say ah ok, this request corresponds to this action and this action WAIT

HOW does the controller know which request corresponds to which action?? We are missing something. The thing that says which request responds to which action is called the ROUTER. And so before we even put any action in our controller we need to put a ROUTE in that says what Action corresponds to each request.

4) In the file tree for the app, find the folder called 'config' and open it. You should see a files called `routes.rb` so open that. You might see text that says 

```ruby
  # For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html
```

That is a good start. If you just read section 1.1 of that page (it's short) you will see that we can define a route for our home page like this:

```ruby
get '/', to: 'shop#home'
```

The `get` part is the *type* of request. When the user or client input is *just* a url, and there are no forms and the user doesn't send any other information *except* the url of the page they want to see, then the *type* of request is usually a `get` request. The `'/'` part is the url. Usually the home page is just `'/'` in code because it is like the base of your directory tree in files and folders. Just like in directories, it is called the 'root'. So you can think of 'root and `'/'` as being the same thing.
`to:` is a method that is provided by Rails and it tells us where we are going *to*. The last part `'shop#home'` is telling us which controller (we only have one so far, and it is 'shop') and then we have the action after the `#` and it is `'home'`. So first, in your config file (after `do` but before `end`) type:

```ruby
get '/', to: 'shop#home'
```
Now that we have a route, we need to put the corresponding action in our shop controller. So in your controller type:

```ruby
def home
end
```
Now, go to your browser and type localhost:3000 again (and make sure you still have the rails server running)

4) HOORAY!!! Oh no wait, you should have a massive error messsage that looks like this:

'ShopController#home is missing a template for this request format and variant'
 
BUT that is ok. Because Rails is telling us that what we don't have, is our View sorted out. Because templates are kept in Views. Remember when we said that the controller says to view, 'hey what have you got?' Well our controller is smart enough (because of Rails) to know that just by defining an action for `home` we want to ask Views for a *template* for `home`. So lets go to our Views folder. Rails has already created a subdirectory for us called 'shop' so let's look in there. Right. It is empty. so Controller says to Views, 'hey, what have you got...' and Views has got nothing. We need to make a *template* inside 'views/shop', for home. So make a file in here called `home.html`. Inside this file, type:
```html
Welcome to my shop
```
Now go to localhost:3000 in your browser again (or hit refresh)

TA DAAAAAA you should see a page containing the words
'Welcome to my shop'

So far we have pretty much all the basics that we need. There is just one more thing that would be pretty cool. If we could make the home page look a little bit more exciting that would be really groovy. This is done with *stylesheets*.

5) Stylesheets are a bit different to anything we have done so far. They aren't kept inside the models or views or controllers. This is because actually they don't add any functionality. They don't MAKE anything, they just change how it looks. So they are kept in a different place. But Rails knows how to find them. You don't though but they are in app/assets/stylesheets folder. Rails has already created a stylesheet for shop: app/assets/stylesheets/shop, so now we can open it.
It is empty (apart from some comments that tell us what it is for) it tells you in here that you can use Sass, which is a type of CSS. Or you can just use CSS. CSS is a *Domain Specific Language* which means that it's another thing you have to learn, but it isn't so hard. Go and read how to do some CSS.

Ok, cool, so now the first thing you will have realised is that sylesheets contain lots of rules, and they apply those rules to *classes* and *IDs*. We will ignore IDs for now. But the reason for this is so that we can seperate out the things on our page and make them all look defferent. We do that by putting each thing we want to be different into a *class* and giving that class its own rules. If we don't seperate things into classes, the rules in our stylesheet won't know what to apply to. If we don't have any classes yet, we can use `html` as our class, and that is like a pre-defined class, it sort of means ALL our html file, so our css rules will apply to everything in the html file. We only have one thing in out html file (so one thing on our page, and it is the line that says 'welcome to my shop') so lets add a style rule and see what happens. In your `shop.css` file type:

```scss
html {
  color: red;
}
```

Refresh and you should see that the text has turned red. YAY. If you learnt more fancy things when you read about CSS you can try them out to see if they work. But for now, we have the basics and we can move on.

Part 2. Models and Migrations

1) So far we have looked at Controllers and Views (andd stylesheets) but we are using an MVC architecture. What is missing here? Ah yes, Model. The main fuction of the model in a standard Rails map is to contain information about the objects that correspond to tables in the database... WHAT? Ok, look at it like this: A shop has products that it sells. Our rails app doesn't need to contain a huge long list of products and their descriptions, prices, sell-by-dates, suppliers etc etc. It can tell us that we *have* products, and the products *have* these attributes... but the actual values for all of these things, the products and the attributes, will be stored in a database. Our Models usually correspond to tables in our database. You could say that Models talk to the database, like the Controllers talk to the Views. We are going to create a Model for products, the Product model, and that will correspond to a table in our database. Things like the name, price etc of the products will become *columns* in that table. 

Let's create a Model first. As usual, Rails takes care of a lot of this for us. In our terminal (in the root directory for the app) type:

```sh
rails generate model Product name:string description:text price:decimal
```
This tells rails to create a Model called Product, and make a corresponding table in our database (called `products`) which has the columns: `name`, `description`, and `price`. The words after the `:` such as `text`, `string` are the *types* that the columns, or attributes, have.








We can think of the MVC and the rails app like a hotel. The controller is the concierge and on the ground floor he is very important 

