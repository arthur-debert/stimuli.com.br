---
layout: post
title: "Subclassing final native classes in the Flash Player"
permalink: "/trane/2007/aug/22/subclassing-final-native-classes-flash-player/"
tags: [as3 actionscript design]
categories: [trane]
legacy_id: 16
date: "2007-08-22 -0300"
---
Reading Bruce [Eckel's post about Flex Components](http://www.artima.com/weblogs/viewpost.jsp?thread=212818) I felt the ending suggestion was pretty interesting: porting python's string library to AS3. Python's string library is very useful: it is full of convenience methods such as <strong>startswith</strong>, <strong>endswith</strong> and so on. I can understand why Adobe feels like this doesn't belong in the player: keeping the player footprint small is paramount, and adding a lot of convenience methods is arguable at best. So let's code our own.

The first step it to create a new class, one that will inherit from String. Oops! The string class is marked <strong>final</strong> which means that it can't be extended. So now, you'd think, just trade inheritance for composition, creating a class that looks like this:

    public class SString{
    	private var _string : String;
        private var _length : int;
        public function SString(withString : *){
            _string = withString.toString();
            _length = _string.length;
        }
    
        public function get length() : int{
            return _length;
        }

    	public function toString() : String{
            return _string;
        }
    }

And then add the extra convenience methods. But there's a problem with using composition in this scenario. If you do, every method that takes a vanilla String will not accept the SString class. This means every time you need a string such as in <strong> new URLRequest(myString);</strong> you will need to convert back to a vanilla string. Now using our "enhanced" string class you must perform these extra steps:
* Import the SSTring clas.
* Use a formal constructor instead of quotes.
* Convert back to a regular string for each use where a string is expected.

The first two issues are understandable, it's just harder to take those cases into account. But it starts to be too heavy weight, it feels clunky. This is just bad design. AS3 is a weakly typed language: types are converted behind the scenes in some cases. If you have something such as :


    var s : * = 1 + " some text";
    // s = "1 some text"

The interpreter will convert the Number 1 to a String automagically. So the type of variables depend on the context their being used. But on other cases the compiler will not allow type substitutions. 

The other solution is to code a class that acts manly as a namespace for function. A class that is a collection of static methods such as:

     StringHelper.startsWith(myString, "static");

This is too verbose. Also, for note that a class such as this is mostly a workaround for the fact that no function do not exist by themselves, which is not very OOP at all. OOP is more than mimicking Java. OOP is about creating designs: hierarchy, collections, that are easy to use and make code more versatile. In this case, which is ironic, AS2 would offer us better alternatives. Prototype inheritance is not so bad after all.

For the life of me, I simply cannot understand why make the String class final. I can understand (but not agree to) not allowing to monkey patch the string class. But not allowing users to subclass string, imposes a lot of extra hoops to create an augmented string, which might not be worth the trouble in the end. Since polymorphism in AS3 is "subclassing polymorphism" it hinders any useful enhancements to the native string class of the Flash Player. The ruby community monkey patches with frequency. The python community has a few more hoops to go through for monkey patching but it can be (easily) done. Maybe, maybe, if your are building a nuclear power plant control code, or making the back end that Visa uses to process credit transactions, the extra safety is in place. But for what flash is used at, I simply can't see the point. 

The only reasonable explanation for this would be because of the internal implementation for the native string. The Array class in not final (I have subclassed it more that once, and it was very handy).At any rate, restricting user's choices because of implementation details is bad design all together.

I am just venting my ever growing frustration with AS3. At the first, even though the bondage and discipline coefficient is pretty high, it looks like it will make things easier. Sure, the improved [run time](http://www.stimuli.com.br/trane/2007/apr/03/as2-as3-growing-pains/), [the better design](http://www.stimuli.com.br/trane/2007/may/14/as3-happy-bits-2-displayobject-hierarchy/) for the display hierarchy is great too. But as I code more and more in AS3 I begin to miss AS2. If you know a better solution to this, I am all ears.