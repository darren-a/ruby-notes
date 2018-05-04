
## Ripper/lex etc  


### using ripper / lex to see tokens

 pp Ripper.lex(<code_name>)  

 ```
 rb(main):040:0> require 'ripper'
=> true
irb(main):041:0> require 'pp'
=> true
irb(main):042:0> code = <<END
irb(main):043:0" puts 2 + 9
irb(main):044:0" END
=> "puts 2 + 9\n"
irb(main):045:0> p code
"puts 2 + 9\n"
=> "puts 2 + 9\n"
irb(main):046:0>
irb(main):047:0> pp Ripper.lex(code)
[[[1, 0], :on_ident, "puts", EXPR_CMDARG],
 [[1, 4], :on_sp, " ", EXPR_CMDARG],
 [[1, 5], :on_int, "2", EXPR_END|EXPR_ENDARG],
 [[1, 6], :on_sp, " ", EXPR_END|EXPR_ENDARG],
 [[1, 7], :on_op, "+", EXPR_BEG],
 [[1, 8], :on_sp, " ", EXPR_BEG],
 [[1, 9], :on_int, "9", EXPR_END|EXPR_ENDARG],
 [[1, 10], :on_nl, "\n", EXPR_BEG]]
=> [[[1, 0], :on_ident, "puts", #<Ripper::Lexer::State: EXPR_CMDARG>], [[1, 4], :on_sp, " ", #<Ripper::Lexer::State: EXPR_CMDARG>], [[1, 5], :on_int, "2", #<Ripper::Lexer::State: EXPR_END|EXPR_ENDARG>], [[1, 6], :on_sp, " ", #<Ripper::Lexer::State: EXPR_END|EXPR_ENDARG>], [[1, 7], :on_op, "+", #<Ripper::Lexer::State: EXPR_BEG>], [[1, 8], :on_sp, " ", #<Ripper::Lexer::State: EXPR_BEG>], [[1, 9], :on_int, "9", #<Ripper::Lexer::State: EXPR_END|EXPR_ENDARG>], [[1, 10], :on_nl, "\n", #<Ripper::Lexer::State: EXPR_BEG>]]
irb(main):048:0>
```

### to see parsed code
pp Ripper.sexp(<code_name>)  

```
irb(main):051:0> pp Ripper.sexp(code)
[:program,
 [[:command,
   [:@ident, "puts", [1, 0]],
   [:args_add_block,
    [[:binary, [:@int, "2", [1, 5]], :+, [:@int, "9", [1, 9]]]],
    false]]]]
=> [:program, [[:command, [:@ident, "puts", [1, 0]], [:args_add_block, [[:binary, [:@int, "2", [1, 5]], :+, [:@int, "9", [1, 9]]]], false]]]]
irb(main):052:0>
```

### to see YARV instructions

```
irb(main):061:0> puts RubyVM::InstructionSequence.compile(code).disasm
== disasm: #<ISeq:<compiled>@<compiled>:1 (1,0)-(1,10)>=================
0000 putself                                                          (   1)[Li]
0001 putobject        2
0003 putobject        9
0005 opt_plus         <callinfo!mid:+, argc:1, ARGS_SIMPLE>, <callcache>
0008 opt_send_without_block <callinfo!mid:puts, argc:1, FCALL|ARGS_SIMPLE>, <callcache>
0011 leave            
=> nil
irb(main):062:0>
```

Also check out:


display info about AST node structure:  
```
ruby --dump parsetree your_script.rb
```

-y option to display internal debug info:  
```
ruby -y your_script.rb
```


## Benchmarking

From this website: https://www.engineyard.com/blog/five-ruby-methods-you-should-be-using  

```
require 'benchmark'

data = (0..50_000_000)

Benchmark.bm do |x|
  x.report(:find) { data.find {|number| number > 40_000_000 } }
  x.report(:bsearch) { data.bsearch {|number| number > 40_000_000 } }
end

         user       system     total       real
find     3.020000   0.010000   3.030000   (3.028417)
bsearch  0.000000   0.000000   0.000000   (0.000006)
```


## System calls  

```
irb(main):286:0> system 'pwd'
/Users/kub3r/Desktop/ruby
=> true
```
