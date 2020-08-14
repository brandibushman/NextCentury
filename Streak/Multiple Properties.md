# Multiple Properties
## Goal: 
To have multiple property URLs. I think that we will be able to sort through this column easier than a premade column. 
### Features
- multiple URLs
- have the URLs be formatted more like a hyper link. 
## Plan
What I am going to try with this is to make a check box to indicate multiple properties or not. If it is selected then I will use a loop and regular expressions to make an iterative process that will create multiple urls. Next I will look for way to innovate and avoid errors based off of user input- a concern is if the process breaks down part way through that it will cause all of the links to no longer exist. Last I will try to formar the cell so that there are hyper links with property names displayed so that it is more user friendly.

### Step 1: Observe Current Code
Below is the current version of the Javascript URL on our current pipline. 

~~~
= if ($'Property (ID: #)' && $'Billing Company (ID: #)'){
'https://app.nextcenturymeters.com/p/' +
/\(\D*(\d*)\D*\)/.exec($'Property (ID: #)')[1] + 
'/dashboard'
}
~~~
There are a few limitations of this is and I don't know whow much we need to worry about them. ONe weakness is if there were, for some reason, parenthesis with digits in the name of the property, this would pick it up. However, there is room for input error if we have it looking specifically for "ID". This is something I will incorporate towards the end of this but I wanted to draw attention to that before we begin. 

An alternative is to establish a variable to be ```/\(\D*(\d*)\D*\)/.exec($'Property (ID: #)')[1]``` then we can create several variables and in the end produce several urls. I hope that this tactic will avoid having a working or not workin scenario. 
~~~
= var propId=/\(\D*(\d*)\D*\)/.exec($'Property (ID: #)')[1] ; 

if ($'Property (ID: #)'){
'https://app.nextcenturymeters.com/p/' + propId +'/dashboard'
}
~~~~


### Step 2: Make it iterative
Next I will develop what will happen if there were multiple properties entered and spearated by a ",,".

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

OR WE COULD USE A WHILE LOOP. I am starting to think this might not work because we would need to first create several variables and that it the part I don't know how to do for an infinite set. .

So sounds like there are code options [to break up strings using Regular Expressions](https://stackoverflow.com/questions/881085/count-the-number-of-occurrences-of-a-character-in-a-string-in-javascript) using [```console.log()```](https://github.com/brandibushman/NextCentury-again/edit/master/Java%20Basics)

## Pieces
- count the variables  ```console.log((cellName.match(new RegExp("ID:", "g")) || []).length); ``` will count the number of times ID: is entered. It makes is a little vulnerable if people type "id" or "Id", but that can be addressed later. 
So now I just need to make it so that is a variable. 

- Turn into Variable (now what we want, we want a number) 
~~~
var cellName = "Property 1 (ID:1234),, Property 2 (ID: 2345)";
var cat =(cellName.match(new RegExp("ID:", "g")) || []).length; // This counts 
cat;
~~~

- separete string into an array and [identifying parts](https://stackoverflow.com/questions/35094916/javascript-adding-new-label-and-data-to-existing-array) in that array 
```
var splitString1 = cellName.split(', '); // This splits the string up based on a comma 
```
- [Loops](https://www.w3schools.com/js/js_loop_for.asp)

## Step 3: Trying to combine everything 
Ultimately I did a few things. The first loop is to see if there is information in those cells or not. Then it defines a few key variables then if there is more than one property entered then a loop gets enabled making multiple URLs, otherwise just one gets made. Lastly if the required boxes are not filled in then it displays "No Property Entered". That way it is clear that the N/A boxes have been filled out, just insufficiently. 
~~~
= if ($'Property (ID: #)' && $'Billing Company (ID: #)'){

   var lngth = ($'Property (ID: #)'.match(new RegExp("ID:", "g")) || []).length; // there are lngth number of props

   var splitString = $'Property (ID: #)'.split(',,'); // this makes an array of different props

   var i;
   var url = "";
   if (lngth >1){
      for (i = 0; i < lngth; i++) {
         url += 'https://app.nextcenturymeters.com/p/' + /\(\D*(\d*)\D*\)/.exec(splitString[i])[1] +'/dashboard  ,  ';
   }
   } else{
      'https://app.nextcenturymeters.com/p/' +
      /\(\D*(\d*)\D*\)/.exec($'Property (ID: #)')[1] +
      '/dashboard'
   }
   } else {
   'No Property Entered'
}
~~~
so obviously the array hates me
