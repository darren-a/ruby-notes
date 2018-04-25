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
:tr  
:count  
:scan  



```
>> str = "qwer"
=> "qwer"
>> str.length
=> 4
>> str[2]
=> "e"
```
:first will work for an array (and others), not for string (likewise :last,  
:count and plenty of others)
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

strip whitespace (from front and back of string)
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

example of removing all whitespace from a string
```
def Palindrome(str)

  # :gsub, global substitution (also check out :scan)
  # bang to mutate;
  # / / to denote regex;
  # \s+ => one or more whitespace
  # replace with nothing ""
  str.gsub!(/\s+/, "")  
  p str
  str == str.reverse

end
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

count number of vowels in a string:  
```
irb#1(main):051:0> "facetious".count("aeiou")
=> 5
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
:take  
:each  
:map  
:reduce  
:reverse  
:uniq  



shortcut for strings so you don't need to type " " etc:  
```
irb(main):021:0> arr = %w[a, b, c, d, e, f, g]
=> ["a,", "b,", "c,", "d,", "e,", "f,", "g"]
```

often better, create array from a range:  
```
irb(main):028:0> arr = ("A".."Z").to_a
=> ["A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O",
"P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z"]
```

to remove single character parts from an array:
```
arr -= [nil, '']
#=> [1, 2, "s", "d"]

# or something like this

> arr = [4, 5, 6, nil, '', 7, 8, '']
=> [4, 5, 6, nil, "", 7, 8, ""]
>
> clean_arr = arr - [nil, ""]
=> [4, 5, 6, 7, 8]

# also look at :compact and :delete_if
```

to remove general whitespace and control chars from an array:
```
> arr = [1, 2, "s", nil, "     ", "d", "\n"]
> arr.reject!{|a| a.nil? || (a.to_s.strip.empty?) }
> [1, 2, "s", "d"]
```



## Range
```
>> Range.ancestors
=> [Range, Enumerable, Object, Kernel, BasicObject]
```
:count  
:first  
:last  
:each  
:step


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
Note that with no arguments last will return the object that defines the  
end of the range even if exclude_end? is true.
```
(10..20).last      #=> 20
(10...20).last     #=> 20
(10..20).last(3)   #=> [18, 19, 20]
(10...20).last(3)  #=> [17, 18, 19]

>> r = (0...5)
=> 0...5
>>
>> r.count
=> 5
>>
>>
>> r2 = (0..5)
=> 0..5
>> r2.count
=> 6
```



## Hash
```
>> {}.class.ancestors
=> [Hash, Enumerable, Object, Kernel, BasicObject]
```

```
>> blank_hash = {}
=> {}
>>
>> # create has with a key-value pair
>> my_hash = {CA: "Sacramento"}
=> {:CA=>"Sacramento"}
>>
>> # add a new k-v pair to existing hash
>> my_hash[:NY] = "Albany"
=> "Albany"
>>
>> my_hash
=> {:CA=>"Sacramento", :NY=>"Albany"}
>>
>> # show all keys
>> my_hash.keys
=> [:CA, :NY]
>>
>> # show all values
>> my_hash.values
=> ["Sacramento", "Albany"]
```

## Object

:clone  



## Float
```
>> Float.ancestors
=> [Float, Numeric, Comparable, Object, Kernel, BasicObject]
```


## Integer
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

rand(n) gives a random # from 0...n  
dice example:
```
irb(main):025:0> 10.times { p (rand(6) + 1) }
5
2
6
2
5
4
1
3
5
4
```


## Symbol
```
>> Symbol.ancestors
=> [Symbol, Comparable, Object, Kernel, BasicObject]
```
for some reason the Symbol class doesn't have a :new method so you have  
to create a symbol with the shortcut (eg. sym = :my_symbol)
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
NOTE: these are by no means proposed as optimal, or even that good. There are no  
doubt plenty of better ways out there but it's a work in progress.


#### iterate through an enumerable (eg array)
tbd  

#### find/create an "exclusion" array (ie. an array containing every
element but a specific one - usually the one you're currently
looking at with a counter, say in an each loop)


#### check if something is a vowel
tbd  

#### sum of series (or partial series)
```
def sum_to(n)
  # sum of a series = number of terms * ( (1st term + nth term) / 2 )
  # eg. 100 terms: 100 * ( (1 + 100) / 2 ) = 100 * 50.5 = 5050
  # (I remember it as: "# of terms * avg of first + last")

  return nil if n < 1
  float_sum = n * ( (1 + n) / 2.0 )
  sum = float_sum.to_i
end

=begin
>> sum_to(1)
=> 1
>> sum_to(3)
=> 6
>> sum_to(100)
=> 5050
>> sum_to(5)
=> 15
>> sum_to(0)
=> nil
>> sum_to(-4)
=> nil
=end
```

#### recursive example
```
def fac(n)

  # edge case(s)
  return nil if n < 0

  # end stop
  # (you must have some way the repeated calls to this
  # method eventually come to a conclusion)
  return 1 if (n == 0) or (n == 1)

  # other cases
  # (make sure you're modifying the input in some way when
  # you call yourself or you'll enter an infinite loop)
  return ( n * fac(n - 1) )

end

=begin
irb(main):049:0> fac(0)
=> 1
irb(main):051:0> fac(1)
=> 1
irb(main):053:0> fac(5)
=> 120
irb(main):077:0> fac(-3)
=> nil
=end
```
Why is factorial(0) defined as 1: http://mathforum.org/library/drmath/view/57128.html


#### Fibonacci numbers  
(useful example of working backwards from the end of an array, and using Array:take)
```
# return first 'n' Fib numbers

# a/A solution

def fibs(n)
  fib_nums = [0, 1]
  return fib_nums.take(n) if n < 3
  # n = 0 => []
  # n == 1 => [0]
  # n == 2 => [0, 1]

  until fib_nums.length == n
    fib_nums << fib_nums[-2] + fib_nums[-1]
  end

  fib_nums
end

# my solution (below) was a decent effort and worked, but is not as good in several important ways.  

Where a/A's is better:   
a) it's cleaner in general  
b) it starts with an array of the first two numbers and handles all three initial conditions  
(n = 0; 1; 2) by using :take to grab from the start array  
c) the 'until' reads naturally and stops when the array of solutions reaches 'n' - this closely  
matches the English problem description. Mine starts with 'i' as 1 (generally try to keep index  
counters starting at zero) and my condition stops at n - 1; it's a bit clunky.  
d) it's elegant and natural to look at the last two elements of the array when adding to make  
the next Fibonacci number as that is how they are mathematically defined. Mine starts at the  
beginning and looks ahead.  
e) I used an explicit return but I probably wrote this before I was hip to Ruby's implicitness  
(not a big deal).  


def fibs(n)
  return [0] if n == 1
  result = [0, 1]

  i = 1
  while i < n - 1
    result << result[i] + result[i - 1]
    i += 1
  end
  return result
end
```


#### to replace parts of a string  
(.tr maybe means "transform" but ri isn't explicit. Note: also look up gsub,  
global substitution)

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
```
def bubble_sort(arr)

  return [] if arr.empty?
  puts "start arr is: #{arr}\n\n"

  i = 0
  while i < arr.length

    j = 0
    while j < (arr.length - 1) - i
      puts "\tentered j loop"
      puts "\tnum is:           #{arr[j]}"
      puts "\tnum following is: #{arr[j+1]}"
      if arr[j] > arr[j+1]
        temp = arr[j]
        arr[j] = arr[j+1]
        arr[j+1] = temp
        puts "swap. arr is now: #{arr}"
      else
        puts "\tno swap needed"
      end
      j += 1
      puts "j is now: #{j}\n\n"
    end

  i += 1
  end
  arr

end

puts("\nTests for #bubble_sort")
puts("===============================================")
    #puts "bubble_sort([]) == []: "  + (bubble_sort([]) == []).to_s
    #puts "bubble_sort([1]) == [1]: "  + (bubble_sort([1]) == [1]).to_s
    #puts "bubble_sort([9, 4, 1]) == [1, 4, 9]: "  + (bubble_sort([9, 4, 1]) == [1, 4, 9]).to_s
    #puts "bubble_sort([5, 4, 3, 2, 1]) == [1, 2, 3, 4, 5]: "  + (bubble_sort([5, 4, 3, 2, 1]) == [1, 2, 3, 4, 5]).to_s
    puts "bubble_sort([51, 34, 35, 12, 1, 65, 14, 8]) == [1, 8, 12, 14, 34, 35, 51, 65]: "  + (bubble_sort([51, 34, 35, 12, 1, 65, 14, 8]) == [1, 8, 12, 14, 34, 35, 51, 65]).to_s
puts("===============================================")
```


##### (a) to find the ASCII code for a string element:
"ord" is not very memorable (maybe "ABC order" helps?)
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
##### (b) to find the char that corresponds to an ASCII code number:
```
>> 65.chr
=> "A"
```


## Object / Class stuff
```
>> my_obj = Object.new
=> #<Object:0x00007f8db2026dd0>

>> my_obj.class.ancestors
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
>> my_obj.methods.grep(/clo/)
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
*use grep on arrays* (noting that Hash:keys and Hash:values return arrays)
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
>> my_hash
=> {:CA=>"Sacramento", :NY=>"Albany"}
>>
>> my_hash.values
=> ["Sacramento", "Albany"]
>>
>> my_hash.keys.grep(/CA/)
=> [:CA]
>>
>> my_hash.keys
=> [:CA, :NY]
>>
> my_hash.values.grep(/acr/)
=> ["Sacramento"]
```
