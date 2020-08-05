# Drop Down Menu

Trying to first make a dropdown menu in Java and then I will make it more dynamic.'

Javascript itself does not support a dropdown option so it wants to use HTML, I don't know if Streak can use HTML.


# Multiple Properties
## Goal: 
To have multiple property URLs. I think that we will be able to sort through this column easier than a premade column. 
### Features
- multiple URLs
- have the URLs be formatted more like a hyper link. 
## Plan
What I am going to try with this is to make a check box to indicate multiple properties or not. If it is selected then I will use a loop and regular expressions to make an iterative process that will create multiple urls. Next I will look for way to innovate and avoid errors based off of user input- a concern is if the process breaks down part way through that it will cause all of the links to no longer exist. Last I will try to formar the cell so that there are hyper links with property names displayed so that it is more user friendly.

### Step 1: Innovate Current Code
Below it the current version of the Javascript URL on our current pipline. 

A limitation of this is that if there were parenthesis in the property name surrounding numbers it will select those instead of the property ID number. We may need to get more specific. like ```\(\D*[Ii][Dd]\D*(\d*)\D*\)``` Which would allow for a lot of input error but would specifically look for "ID". This is something I will incorporate towards the end of this but I wanted to draw attention to that before we begin. 

~~~
= if ($'Property (ID: #)' && $'Billing Company (ID: #)'){
'https://app.nextcenturymeters.com/p/' +
/\(\D*(\d*)\D*\)/.exec($'Property (ID: #)')[1] + 
'/dashboard'
}
~~~
I believe if I first establish a variable to be ```/\(\D*(\d*)\D*\)/.exec($'Property (ID: #)')[1]`` then we can create several variables and in the end produce several urls. I hope that this tactic will avoid having a working or not workin scenario. 
~~~
= var propId=/\(\D*(\d*)\D*\)/.exec($'Property (ID: #)')[1] ; 

if ($'Property (ID: #)'){
'https://app.nextcenturymeters.com/p/' + propId +'/dashboard'
}
~~~~
The above worked!! WOOHOO!! 

### Step 2: Make it iterative
Next I will develop what will happen if there were multiple properties entered and spearated by a ">".

They are using basic [regular expressions](https://en.wikipedia.org/wiki/Regular_expression#Basic_concepts) and the "/" surrounding the regular expression is just a Javascript thing. <sub>(Reminder for my brain: the /D stands for non digits and the /d stands for digits.)<sub>

So it appears that ```[1]``` is a thing in Javascript that asks to return an object. The regular expression creates two [nested groups](https://regexone.com/lesson/nested_groups). So the (Id:1234) is the 0 group and 1234 is the 1 group. 

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
