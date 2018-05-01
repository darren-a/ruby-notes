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
:match  (see Smiley Face example in regex section)



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
:size # alias for :length  
:count  
:first  
:last  
:[n]  
:take
:each  
:each_with_index  
:map  (also you can chain .with_index to map)
:map! (remember that map does NOT mutate unless you use the bang version!!)
:reduce  
:inject  
:reverse  
:uniq  

(part 2 stuff)
:reduce  
:permutation  
:repeated_permutation  
:combination  
:repeated_combination  
:all  
:max  
:min  
:clear  
:compact  
:select  
:reject  
:sort_by  
:to_h  (converts nested array of two-element arrays to a hash)  




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

count  
```
[1, 2, 3, 3, 2, 1].count #=> 6
[1, 2, 3, 3, 2, 1].count(2) #=> 2
[1, 2, 3, 3, 2, 1].count {|int| int.odd?} #=> 4
```

reduce  
```
> array = [1, 2, 3, 4]       # => [1, 2, 3, 4]
> array.reduce(0, :+) => 10  # initial value is 0; action is to sum each element
```

map  


map.with_index  (NOTE: this is chained, not a single method)



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

use "===" to check if num is in range   
```
irb(main):078:0> (1..25) === 14
=> true
irb(main):079:0>
irb(main):081:0> (1..25) === 25
=> true
irb(main):082:0>
irb(main):083:0> (1...25) === 25
=> false
```
other  
```
# create array
irb(main):088:0> (1..9).to_a
=> [1, 2, 3, 4, 5, 6, 7, 8, 9]

# create arrays with Range's new method (exc and inc)
irb(main):094:0> digits = Range.new(1, 9, true).to_a
=> [1, 2, 3, 4, 5, 6, 7, 8]
irb(main):095:0> digits = Range.new(1, 9).to_a
=> [1, 2, 3, 4, 5, 6, 7, 8, 9]
```
flip flop (the logic of this confuses me)
it's basically:  
- false until LHS evaluates to true (ie. when n == 2)
- remains true until RHS evaluates to true; so keep printing nums until n >= 5  
(so why is '5' printed out?)   
```
irb(main):105:0> (1..7).each {|n| puts n if n == 2..n >= 5}
2
3
4
5
=> 1..7
```



## Hash
```
>> {}.class.ancestors
=> [Hash, Enumerable, Object, Kernel, BasicObject]
```
:size  
:length  
:count  
:keys  
:values  
:to_a  (converts to nested array of [key, value] arrays)  
:each  (takes two args: |k, v| for example)  
:each_key
:each_value
:each_pair     
:has_value?  
:value? (same as "has_value?")
:has_key?
:include?  (same as "has_key?")
:key? (same as "has_key?")    
:select  
:reject  
:delete  
:sort_by  (ex to sort by key  
  ```
  my_hash = {b: 11, a: 100, c: -25}
  my_hash.sort_by {|k, v| k} #=> [[:a, 100], [:b, 11], [:c, -25]]
  ```
:include? # tests if hash includes its arg as a key  
:has_key?  (same as "include?")  
:key?  (same as "include?")  
:empty?  
:any?    

shortcut for creation if using symbol keys (v common):
```
irb(main):425:0> my_hash = {:CA => "Sacramento"}
=> {:CA=>"Sacramento"}
```
is the same as:
```
irb(main):428:0> my_hash1 = {CA: "Sacramento"}
=> {:CA=>"Sacramento"}
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

####counter hash and using default start values  

use the "new" method in Hash class to create a new hash object with default values:
```
irb(main):445:0> my_hash = Hash.new(0)
=> {}
irb(main):446:0>
irb(main):447:0> my_hash[:a]
=> 0
```
count num of occurrences of each letter in string:
```
irb(main):483:0> letter_counts = Hash.new(0)
=> {}
irb(main):542:0> str = "The quick brown fox jumps over the lazy dog"
=> "The quick brown fox jumps over the lazy dog"
irb(main):485:0>
irb(main):502:0> letters = str.split("") - [" "]
=> ["T", "h", "e", "q", "u", "i", "c", "k", "b", "r", "o", "w", "n", "f", "o", "x", "j", "u", "m", "p", "s", "o", "v", "e", "r", "t", "h", "e", "l", "a", "z", "y", "d", "o", "g"]
irb(main):485:0>
irb(main):486:0> letters.each do |l|
irb(main):487:1*   letter_counts[l.downcase] += 1
irb(main):488:1> end
irb(main):488:1>
irb(main):557:0> letter_counts
=> {"t"=>4, "h"=>4, "e"=>7, "q"=>2, "u"=>4, "i"=>2, "c"=>2, "k"=>2, "b"=>2, "r"=>4, "o"=>8, "w"=>2, "n"=>2, "f"=>2, "x"=>2, "j"=>2, "m"=>2, "p"=>2, "d"=>3, "v"=>2, "l"=>2, "a"=>2, "z"=>2, "y"=>2, "g"=>2, "s"=>1}
irb(main):558:0>
irb(main):559:0> letter_counts.length
=> 26

# find second most popular letter:  
irb(main):597:0> frequency_array = letter_counts.sort_by {|k,v| v}
=> [["g", 1], ["v", 1], ["l", 1], ["a", 1], ["z", 1], ["y", 1], ["d", 1], ["q", 1], ["i", 1], ["c", 1], ["k", 1], ["b", 1], ["w", 1], ["n", 1], ["f", 1], ["x", 1], ["j", 1], ["m", 1], ["p", 1], ["s", 1], ["h", 2], ["u", 2], ["t", 2], ["r", 2], ["e", 3], ["o", 4]]
irb(main):598:0> frequency_array[-2].first  # return the first element from the second array from the end  
=> "e"
```


## Object
```
> Object.ancestors
=> [Object, Kernel, BasicObject]
```

:class  
:inspect  
:object_id  
:clone (note: a clone of a frozen object is also frozen)
:dup  (note: a dup of a frozen object is not frozen)
:freeze  
:frozen?  
:methods  
:method  




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
:ceil  
:floor  
:round  
:even?  
:odd?  
:lcm  
:gcd  
:chr  
:ord  # returns itself (for compatibility)
:times
:downto
:upto
:next  
: <<
: >>


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
downto example:
```
5.downto(1) { |n| print n, ".. " }
print "  Liftoff!\n"
#=> "5.. 4.. 3.. 2.. 1..   Liftoff!"
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


## Time
```
> Time.public_methods(false)
=> [:now, :at, :utc, :gm, :local, :mktime, :new, :allocate, :superclass]
>
> t1 = Time.now; t2 = Time.new  # check on what the differences are
=> 2018-04-28 18:20:37 -0700
```

strftime  
```
> t2.strftime("%d")
=> "28"
> t2.strftime("%c")
=> "Sat Apr 28 18:20:37 2018"
```
%d - day of month  
%D - date  
%c - date, time  



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

## Enumerable

to find out if an object inherits from Enumerable:
```
>> [1,2,3].class.ancestors
=> [Array, Enumerable, Object, Kernel, BasicObject]
```
:sort  
:uniq  
:find  (passes each entry in enum to block; finds the first entry for which block is true)
:find_all  
:find_index
:drop  
:take   
:map  
:reduce  
:inject  
:max  
:min  
:member?  
:all?  
:any?
:none?  
:include?  
:one?  



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

all?  
```
def all_even?(arr)
  arr.all? {|int| int.even?}
end
```

permutations and combination  
```
irb(main):305:0> [:a,:b,:c].repeated_permutation(2).each { |el|  p el }
[:a, :a] # repeated self  
[:a, :b]
[:a, :c]
[:b, :a]
[:b, :b] # repeated self  
[:b, :c]
[:c, :a]
[:c, :b]
[:c, :c] # repeated self  
=> [:a, :b, :c]
irb(main):306:0>
irb(main):309:0> [:a,:b,:c].permutation(2).each { |el|  p el }
[:a, :b]
[:a, :c]
[:b, :a] # same as :a :b  
[:b, :c]
[:c, :a] # same as :a :c  
[:c, :b] # same as :c :b  
=> [:a, :b, :c]
irb(main):310:0>
irb(main):311:0> [:a,:b,:c].combination(2).each { |el|  p el }
[:a, :b]
[:a, :c]
[:b, :c]
=> [:a, :b, :c]
```


## Enumerator

```
irb(main):004:0> Enumerator.ancestors
=> [Enumerator, Enumerable, Object, Kernel, BasicObject]
```

## Set  
(not part of core Ruby, so you need: _require 'set'_)  
```
irb(main):850:0> Set.ancestors
=> [Set, Enumerable, Object, Kernel, BasicObject]
```
notes:  
- all elements unique
- if you add an existing object to the set nothing will happen
- if you try to delete an object that isn't in the set nothing will happen

```
require 'set'
```
:<<  
:add  
:add?  (returns nil (rather than the set itself) if an add operation fails)
:delete
:&  (intersection)  
:+  (union)  
:|  (union)
:-  (difference)  
:^  (xor - members of set A + members of set B but not members of both)  
:merge  
:subset  
:superset  
:proper_subset  
:proper_superset  


Examples:  

new_england = Set.new(["Connecticut", "Maine", "Massachusetts", "New Hampshire", "Rhode Island", "Vermont"])  
tri_state = Set.new(["Connecticut", "New Jersey", "New York"])


```
irb(main):839:0> new_england = ["Connecticut", "Maine", "Massachusetts", "New Hampshire",
irb(main):840:1*                "Rhode Island", "Vermont"]
=> ["Connecticut", "Maine", "Massachusetts", "New Hampshire", "Rhode Island", "Vermont"]
irb(main):844:0> require 'set'
=> true
irb(main):845:0>
irb(main):846:0> state_set = Set.new(new_england)
=> #<Set: {"Connecticut", "Maine", "Massachusetts", "New Hampshire", "Rhode Island", "Vermont"}>

```


intersection, use '&'  
```
irb(main):864:0>
irb(main):865:0> state_set & tri_state
=> #<Set: {"Connecticut"}>
```
union, use '+' or '|'  
```
irb(main):868:0> state_set + tri_state
=> #<Set: {"Connecticut", "Maine", "Massachusetts", "New Hampshire", "Rhode Island", "Vermont", "New Jersey", "New York"}>
irb(main):869:0>
irb(main):870:0> state_set | tri_state
=> #<Set: {"Connecticut", "Maine", "Massachusetts", "New Hampshire", "Rhode Island", "Vermont", "New Jersey", "New York"}>
```

difference, use '-'  
```
irb(main):872:0> state_set - tri_state
=> #<Set: {"Maine", "Massachusetts", "New Hampshire", "Rhode Island", "Vermont"}>
```

xor, use '^'
```
irb(main):876:0> state_set ^ tri_state
=> #<Set: {"New Jersey", "New York", "Maine", "Massachusetts", "New Hampshire", "Rhode Island", "Vermont"}>
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

# remove non-vowel letters from a word:
>> "facetious".tr('^aeiou', '')
=> "aeiou"
>>
>> "sky".tr('^aeiou', '')
=> ""
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


## Introspection
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
```

to see methods without those of ancestor classes:
```
irb(main):502:0> Ripper.public_methods(false).sort
=> [:allocate, :dedent_string, :lex, :lex_state_name, :new, :parse, :sexp, :sexp_raw, :slice, :superclass, :token_match, :tokenize]
```

in pry you can cd to an object and run ls to see methods
```
[28] pry(main)> cd []
[29] pry(#<Array>):1>
[30] pry(#<Array>):1>
[31] pry(#<Array>):1>
[32] pry(#<Array>):1> ls
Enumerable#methods:
  all?            each_entry        find_all  lazy       none?         slice_when
  chunk           each_slice        flat_map  max_by     one?          sort_by   
  chunk_while     each_with_index   grep      member?    partition     to_set    
  collect_concat  each_with_object  grep_v    min_by     reduce      
  detect          entries           group_by  minmax     slice_after
  each_cons       find              inject    minmax_by  slice_before
Array#methods:
  &              concat
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

Smiley Face example
face:
a) must start with eyes of : or ;
b) may or may not have a nose of - or ~
c) must end with mouth of ) or D
implicit is no whitespace at all and only 2 or 3 chars

this is a hybrid; tried full regex but got too messy for me
```
def count_smileys(arr)

  result = 0
  arr.each do |face|
    next if face.match(/\s/) || face.length > 3
    result += 1 if face
                       .match(/^[:|;]/) && face
                       .match(/[-|~]?/) && face
                       .match(/[)|D]$/)
  end
  result
end
```

## Script

```
#!/usr/bin/env ruby
def say_hello(name)
  puts "Hey there, #{name}!"
end

if $PROGRAM_NAME == __FILE__
  name = gets.chomp
  say_hello(name)
end
```


## Matrix

part of the "sum of all set" problem, using simple arrays here.

```
> arr1
=> [3, 4, 5, 1]
>
> arr2
=> [1, 0, 1, 0]
>
> sum = (arr1.map.with_index {|el, idx| el * arr2[idx]}).reduce(:+)
=> 8
```

Matrix module inner_product (same as 'dot'?) and cross_product should be useful here as well (require )
```
> a.methods.sort.grep(/prod/)
=> [:cross_product, :inner_product]
```
