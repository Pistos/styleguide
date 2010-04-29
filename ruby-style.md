# Pistos' Ruby Style Guide

(forked from Christian Neukirchen's Ruby Style Guide)

Chris' original message:

"You may not like all rules presented here, but they work very well for
me and have helped producing high quality code.  Everyone is free to
code however they want, write and follow their own style guides, but
when you contribute to my code, please follow these rules:"


## Formatting

* Use ASCII (or UTF-8, if you have to).

* Use 2 space indent, no tabs.

* Use Unix-style line endings.

* Put spaces around operators, and after commas, colons and semicolons
  (unless at EOL, and besides symbols).

* Put a space after opening parentheses and braces; and before
  closing parentheses and braces.  e.g.:

  iterator( hash[ :symbol ] ) { |o| o.foo }

* Brackets may or may not be accompanied by space, at your discretion.
  These are both okay:

  my_hash[ :foo ]
  my_hash[:foo]

* Only use postfix modifiers (if/unless/while/until/rescue) if the modified
  expression is extremely short; otherwise use a full code block (if-end,
  etc.)

* Use two spaces before postfix modifiers.

* Use an empty line between defs.

* Don't put an empty line between comment block and def.

* Use newlines liberally, even within a single Ruby expression, if it will
  improve readability (by clarifying expression components).  e.g. break up
  long conditional expressions and lists (method arguments, Enumerable
  literals, etc.)

* Avoid long method chains on a single line (break it up across multiple lines).

* Use empty lines to break up a long method into logical paragraphs.  The
  return value of a long method should be considered a paragraph on its own.

* Aim to have lines shorter than 80 characters.

* Never have trailing whitespace.  (Enable relevant editor settings, if any.)

* Indent "when" as deep as "case".

* Always use a comma after the last element of list literals.  e.g.

  [
    'foo',
    'bar',
  ]
  {
    'bin' => 'baz',
    'blue' => 'green',
  }

* Never indent relative to an opening parenthesis, bracket, etc.  Always indent
  just one level deeper.  e.g.

  # Bad
  some_hash = {
                'foo' => 'bar',
              }

  # Good
  some_hash = {
    'foo' => 'bar',
  }

## Syntax

* Use parentheses with def when there are arguments.

* Avoid "for".

* Never use "then".

* Use when x; ... for one-line cases.

* Use && and || for boolean expressions; "and" and "or" for control flow.
  (Rule of thumb: If you have to use outer parentheses, you are using the
  wrong operators.)

* Avoid multiline ternary "? :"; use if-else instead.

* Use parentheses with method calls except when calling single-argument methods
  and not using the return value.

    x = Math.sin( y )
    place_at( row, col )
    array.delete e
    puts value

* Use {} when using the return value of a block; use do-end otherwise.

* Multiline {} blocks are fine.

* Only use "return" when prematurely exiting a method (i.e. never at the end of
  a method).

* Use "return" only at or very near the top of a method, if at all.

* Avoid line continuation (\) where not required.

* Never use assignment in a condition:

    # Avoid:
    if v = array.grep(/foo/) ...

* Use ||= freely.

* Only use "common" sigil variables.


## Naming

* Use snake_case for methods and variables; avoid concatenating words
  (e.g. badlychosenidentifier)

* Use CamelCase for classes and modules.  Keep acronyms like HTTP,
  RFC, XML uppercase.

* Use SCREAMING_SNAKE_CASE for other constants.

* When choosing identifiers, reader understanding trumps laziness and
  inability to type fast.

* When defining binary operators, name the argument "other".

* Prefer map over collect, find over detect, find_all over select.


## Comments

* Avoid comments; aim for self-explanatory code.

* Use yardoc and its conventions for API documentation.  http://yard.soen.ca/

* Prefer method and class comments; avoid comments inside methods.

* Comments longer than a word should be capitalized and use punctuation.


## The rest

* Avoid long methods.

* Avoid having too many parameters.

* Prefer guard clauses over method-encompassing conditional blocks.  e.g.

  # Bad
  def foo
    if condition
      # many lines
    end
  end

  # Good
  def foo
    return  if ! condition
    # many lines
  end

* Sort conditional blocks by size (smaller first).  e.g.

  # Avoid
  if condition
    do_many
    things
    here
  else
    one_line
  end

  # Prefer
  if ! condition
    one_line
  else
    do_many
    things
    here
  end

* Use def self.method to define singleton methods.

* Add "global" methods to Kernel (if you have to) and make them private.

* Avoid alias when alias_method will do.

* Write for Ruby 1.9+, except when required to maintain legacy code.

* Avoid needless metaprogramming.

* Do not mess around in core classes when writing libraries.

* Keep things as simple as possible (but no simpler).

* Be consistent.

* Use common sense.
