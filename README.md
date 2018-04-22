# ruby-notes

## String
```
>> String.ancestors
=> [String, Comparable, Object, Kernel, BasicObject]
>> "fg".class.ancestors
=> [String, Comparable, Object, Kernel, BasicObject]
```
:length  
:[n]  
:split  
:strip  
:upcase  
:downcase  
:capitalize  
:reverse  
:rjust  
:ljust  
:each_char  
:chars  

```
>> str = "qwer"
=> "qwer"
>> str.length
=> 4
>> str[2]
=> "e"
```
:first will work for an array (and others), not for string (likewise :last, :count and plenty of others)
```
>> str.first
Traceback (most recent call last):
        2: from /Users/kub3r/.rbenv/versions/2.5.0/bin/irb:11:in `<main>'
        1: from (irb):113
NoMethodError (undefined method `first' for "qwer":String)
>>
>> str[0]
=> "q"

>> str.split("")
=> ["q", "w", "e", "r"]
>>
>> arr = str.split("")
=> ["q", "w", "e", "r"]

>> arr.first
=> "q"
>>
>> arr.count
=> 4
>> arr.length
=> 4
```

.strip whitespace
```
>> a = "  stuff       "
=> "  stuff       "
>>
>> a
=> "  stuff       "
>>
>> b = a.strip
=> "stuff"
>> b
=> "stuff"
>> a
=> "  stuff       "
```

"bang" methods will generally mutate the receiver (or do other "risky" stuff)
```
>> str
=> "qwer"
>>
>> str.reverse
=> "rewq"
>>
>> str
=> "qwer"
>>
>> str.reverse!
=> "rewq"
>>
>> str
=> "rewq"
>>
```


## Array
```
>> [1,2,3].class.ancestors
=> [Array, Enumerable, Object, Kernel, BasicObject]
```
:count  
:length  
:count  
:first  
:last  
:[n]  
:each  
:map  
:reverse  
:uniq  



## Range
```
>> Range.ancestors
=> [Range, Enumerable, Object, Kernel, BasicObject]
```
:count  
:first  
:last  
:each  

```
>> r = (0...5)
=> 0...5
>> r.first
=> 0
>>
>> r.last
=> 5
```
WEIRD! I expected 4 to be last but it's by design, apparently (see: https://stackoverflow.com/questions/11467846/ruby-range-last-does-not-give-the-last-value-why)  
Note that with no arguments last will return the object that defines the end of the range even if exclude_end? is true.
```
(10..20).last      #=> 20
(10...20).last     #=> 20
(10..20).last(3)   #=> [18, 19, 20]
(10...20).last(3)  #=> [17, 18, 19]

>>
>> r.count
=> 5
>>
>> r1 = (0..5)
=> 0..5
>> r1.count
=> 6
```



## Hash
```
>> {}.class.ancestors
=> [Hash, Enumerable, Object, Kernel, BasicObject]
```

```
>> h = {CA: "Sacramento"}
=> {:CA=>"Sacramento"}
>> h[:NY] = "Albany"
=> "Albany"
>> h
=> {:CA=>"Sacramento", :NY=>"Albany"}

>> h.keys
=> [:CA, :NY]
>> h.values
=> ["Sacramento", "Albany"]
```

## Float
```
>> Float.ancestors
=> [Float, Numeric, Comparable, Object, Kernel, BasicObject]
```


# Integer
```
>> Integer.ancestors
=> [Integer, Numeric, Comparable, Object, Kernel, BasicObject]
```

```
>> 3.times do
?>   puts "Hi!"
>> end
Hi!
Hi!
Hi!
=> 3
>>
>> 3.times { puts "Hi!" }
Hi!
Hi!
Hi!
=> 3
>>
```


## Math
```
>> Math::E
=> 2.718281828459045
>>
>> Math::PI
=> 3.141592653589793
>>
>> Math.sqrt(9)
=> 3.0
```


## Symbol
```
>> Symbol.ancestors
=> [Symbol, Comparable, Object, Kernel, BasicObject]
```
for some reason the Symbol class doesn't have a :new method so you have to create a symbol with the shortcut (eg. sym = :my_symbol)
```
>> Array.respond_to?(:new)
=> true
>>
>> String.respond_to?(:new)
=> true
>>
>> Symbol.respond_to?(:new)
=> false
>>
>> sym = :darren
=> :darren
>>
>> puts sym
darren
=> nil
```

## Enumerables

to find out if an object inherits from Enumerable:
```
>> [1,2,3].class.ancestors
=> [Array, Enumerable, Object, Kernel, BasicObject]
```

```
>> [1,2,3].min
=> 1
>>
>> [1,2,3].max
=> 3
>>
>> (1..10).min
=> 1
>>
>> (9...21000).max
=> 20999
```



## Techniques
NOTE: these are by no means proposed as optimal, or even that good. There are no doubt plenty of better ways out there but it's a work in progress.

#### iterate through an enumerable (eg array)


#### find/create an "exclusion" array (ie. an array containing every
element but a specific one - usually the one you're currently
looking at with a counter, say in an each loop)


#### check if something is a vowel


#### to replace parts of a string (.tr probably means transform but ri isn't
explicit. Note: also look up gsub, global substitution)

```
>> "hello".tr('el', 'ip')
=> "hippo"
>>
>> "hello".tr('aeiou', '*')
=> "h*ll*"
>>
>> "hello".tr('aeiou', 'AA*')
=> "hAll*"
```


#### bubble sort (iterate through a fixed outer loop with an ever-decreasing inner loop)



#### (a) to find the character code for a string element:
```
>> "A".ord
=> 65
>> "Z".ord
=> 90
>> "a".ord
=> 97
>> "z".ord
=> 122
```
#### (b) to find the char that corresponds to an ASCII code number:
```
>> 65.chr
=> "A"
```


## Object / Class stuff
```
>> obj = Object.new
=> #<Object:0x00007f8db2026dd0>

>> obj.class.ancestors
=> [Object, Kernel, BasicObject]

>> Object.instance_methods.sort
=> [:!, :!=, :!~, :<=>, :==, :===, :=~, :__id__, :__send__,
:class, :clone, :define_singleton_method, :display, :dup, :enum_for,
:eql?, :equal?, :extend, :freeze, :frozen?, :hash, :inspect,
:instance_eval, :instance_exec, :instance_of?, :instance_variable_defined?,
:instance_variable_get, :instance_variable_set, :instance_variables,
:is_a?, :itself, :kind_of?, :method, :methods, :nil?, :object_id, :pp,
:private_methods, :protected_methods, :public_method, :public_methods,
:public_send, :remove_instance_variable, :respond_to?, :send, :singleton_class,
:singleton_method, :singleton_methods, :taint, :tainted?, :tap, :to_enum,
:to_s, :trust, :untaint, :untrust, :untrusted?, :yield_self]

>> Object.instance_methods.grep(/clo/)
=> [:clone]
>>
>> obj.methods.grep(/clo/)
=> [:clone]
>>
>> {}.class.ancestors
=> [Hash, Enumerable, Object, Kernel, BasicObject]
>>
>> Hash.ancestors
=> [Hash, Enumerable, Object, Kernel, BasicObject]
>>
>> Range.ancestors
=> [Range, Enumerable, Object, Kernel, BasicObject]
>>
>> true.class.ancestors
=> [TrueClass, Object, Kernel, BasicObject]
>>
>> false.class.ancestors
=> [FalseClass, Object, Kernel, BasicObject]
```



## Regex, patterns, grep etc

Strange that there is no grep instance method for String but there are other ways
around this
```
>> "".respond_to?(:grep)
=> false
>>
```
BEWARE: even though hash responds to :grep it appears to always give empty results, see:  
https://www.safaribooksonline.com/library/view/ruby-cookbook/0596523696/ch05s15.html)
```
>> {}.respond_to?(:grep)
=> true
>>
```
*use grep on arrays* (noting that :keys and :values in Hash give array results)
```
>> [].respond_to?(:grep)
=> true
>>
>> :sym.respond_to?(:grep)
=> false
>>
>> 7.respond_to?(:grep)
=> false
>>
>> 7.8.respond_to?(:grep)
=> false
```

contains "f":
```
>> ["f", "gee", "zfe"].grep(/f/)
=> ["f", "zfe"]
```
starts with "f":
```
["f", "gee", "zfe"].grep(/^f/)
=> ["f"]
```
ends with "e":
```
["f", "gee", "zfe"].grep(/e$/)
=> ["gee", "zfe"]
```

```
>> h
=> {:CA=>"Sacramento", :NY=>"Albany"}
>> h.values
=> ["Sacramento", "Albany"]
>> h.keys.grep(/CA/)
=> [:CA]
>> h.keys
=> [:CA, :NY]
> h.values.grep(/acr/)
=> ["Sacramento"]
```
