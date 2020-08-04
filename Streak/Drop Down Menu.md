## Drop Down Menu

Trying to first make a dropdown menu in Java and then I will make it more dynamic.'

Javascript itself does not support a dropdown option so it wants to use HTML, I don't know if Streak can use HTML.


# Multiple Properties

What I am going to try with this is to make a check box and then have the URL column know if check box is unchecked then to make the URL as normal. If not then make multiple URLs where the properties are separated by a "/"

Below it the current version of the Javascript URL on our current pipline
~~~
= if ($'Property (ID: #)' && $'Billing Company (ID: #)'){
'https://app.nextcenturymeters.com/p/' +
/\(\D*(\d*)\D*\)/.exec($'Property (ID: #)')[1] + 
'/dashboard'
}
~~~
I believe if I first establish my variable
~~~
= var thing=$'Multiple Properties';

if (thing = 0) then{
if ($'Property (ID: #)' && $'Billing Company (ID: #)'){
'https://app.nextcenturymeters.com/p/' +
/\(\D*(\d*)\D*\)/.exec($'Property (ID: #)')[1] + // the /\(\D*(\d*)\D*\)/ seems superr unecessary
'/dashboard' BUT IT IS NOT I think that is what they were using to isolate the ID numbers?
}
else{

}
~~~
