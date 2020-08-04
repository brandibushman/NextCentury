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
I believe if I first establish my variable. The /\(\D*(\d*)\D*\)/.exec($'Property (ID: #)')[1] seems superr unecessary
'/dashboard' BUT IT IS NOT I think that is what they were using to isolate the ID numbers?

So I wonder if I tried to isolate that code first if that would work. 
~~~
= var propId=/\(\D*(\d*)\D*\)/.exec($'Property (ID: #)')[1] ; 

if ($'Property (ID: #)'){
'https://app.nextcenturymeters.com/p/' + propId +'/dashboard'
}
~~~~
The above worked!! WOOHOO!!

So for the multiple Properties We could have multiple URLs?:
First I will develop what will happen if there were multiple properties entered and spearated by a "/". 
I do not fully understand the ``` /\(\D*(\d*)\D*\)/.exec($'Property (ID: #)')[1] ``` but it looks similar to houw I remember SQL notation based off of the ``` [1] ```. 

I AM AN ALL KNOWING WIZARD BECAUSE IT IS [SQL](https://en.wikipedia.org/wiki/Regular_expression#Basic_concepts) and the /D stands for non digits and the /d stands for digits! Oof. . . I was starting to worry I forgot my touch. I think I am close to figuring this out!!!!













~~~
= var thing=$'Multiple Properties';

if (thing = 0) then{
if ($'Property (ID: #)' && $'Billing Company (ID: #)'){
'https://app.nextcenturymeters.com/p/' +
/\(\D*(\d*)\D*\)/.exec($'Property (ID: #)')[1] + 
}
else{

}
~~~
