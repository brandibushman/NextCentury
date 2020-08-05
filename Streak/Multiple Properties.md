# Drop Down Menu

Trying to first make a dropdown menu in Java and then I will make it more dynamic.'

Javascript itself does not support a dropdown option so it wants to use HTML, I don't know if Streak can use HTML.


# Multiple Properties
### Goal: to have multiple property URLs. I think that we will be able to sort through this column easier than a premade column. 
Features
- multiple URLs
- have the URLs be formatted more like a hyper link. 

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
A limitation of the above is that if there were parenthesis in the property name surrounding numbers it will select those. We may need to get more specific. like ```\(\D*[Ii][Dd]\D*(\d*)\D*\)``` Which would allow for a lot of input error but would specifically look for "ID".
<span style="color:red">This is something that I will look into after I have been able to successfully allow for multiple property entries.</span>

So for the multiple Properties We could have multiple URLs?:
First I will develop what will happen if there were multiple properties entered and spearated by a "/". 
I do not fully understand the ``` /\(\D*(\d*)\D*\)/.exec($'Property (ID: #)')[1] ``` but it looks similar to how I remember SQL notation.

It is [SQL](https://en.wikipedia.org/wiki/Regular_expression#Basic_concepts) the "/" surrounding the SQL are just a Javascript thing. Reminder for my brain: the /D stands for non digits and the /d stands for digits.

So it appears that ```[n] // | n in the set of real numbers``` is a thing in Javascript that asks to return an object. The regular expression creates two groups. So the (Id:1234) is the 0 group and 1234 is the 1 group. 

I think what I will try to do is create a loop that counts a special character that does not occur property names like "<" and basically count those. So It will look at the string and count the number of "<", ```|{>}|= m-1```, then the loop will go m times. 
The loop can just be something like 

So if we have a string like Property (ID: 1234) > Propertyalso (ID: 2345) the *regular expression* would look like 
~~~
\(>+\D*(\d*)\D*>+\)
~~~
This would create a group 0 that is ```Property (ID: 1234)```
And a group 1 that is ``` 1234 ````

I need to figure out how to make either a regular expression iterative or. . . basically how to get that to repeat itself. 





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
