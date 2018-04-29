 ### using ripper / lex to see tokens
 
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
