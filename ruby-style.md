# Pistos' Ruby Style Guide

(forked from Christian Neukirchen's Ruby Style Guide)

Chris' original message:

"You may not like all rules presented here, but they work very well for
me and have helped producing high quality code.  Everyone is free to
code however they want, write and follow their own style guides, but
when you contribute to my code, please follow these rules:"

## Principles

Almost all the individual points below are manifestations of an intent to
adhere to one core principle:

**Write code in a way that helps future coders understand and manipulate the code quickly and easily.**

Brevity and superficial visual aesthetics should not be favoured at the expense
of this main principle.

Some subprinciples:

1. Be considerate of the reader.
2. Communicate design and intent.
3. Reveal structure and hierarchy.
4. Make expressions distinct.

## Formatting

* Use ASCII (or UTF-8, if you have to).

* Use 2 space indent, no tabs.

* Use Unix-style line endings.

* Put spaces around operators, and after commas, colons and semicolons
  (unless at EOL, and besides symbols).

* Put a space after opening parentheses and braces; and before
  closing parentheses and braces.  e.g.:

        iterator( hash[:symbol] ) { |o| o.foo }

* Brackets may or may not be accompanied by space, at your discretion.
  These are both okay:

        my_hash[ :foo ]
        my_hash[:foo]

* Only use postfix modifiers (if/while/until/rescue) if the modified
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

* Always make the last line of a source code file an empty line.

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

* Never use "unless"; always use "if" with "!".

* Use when x; ... for one-line cases.

* Use && and || for boolean expressions; "and" and "or" for control flow.
  (Rule of thumb: If you have to use outer parentheses, you are using the
  wrong operators.)

* Avoid multiline ternary "? :"; use if-else instead.

* Use parentheses with method calls using the return value, or when it would improve readability.

        x = Math.sin( y )
        place_at row, col
        array.delete e
        puts value
        method_name(
          many,
          arguments: given,
          to: the,
          method: nil
        )

* Use {} when using the return value of a block, or when a small block can fit on one line; use do-end otherwise.

* Never call a method on a do-end block.  Use {}.

        # Don't:
        lambda do
          # ...
        end.should # ...

* Multiline {} blocks are fine.

* Only use "return" when prematurely exiting a method (i.e. never at the end of
  a method).

* Use "return" only at or very near the top of a method, if at all.

* Avoid line continuation (backslash at EOL) where not required.

* Never use assignment in a conditional expression:

        # Avoid:
        if v = array.grep(/foo/) ...

        # Avoid:
        def has_enough_foo?
          ( v = calculation(@foo) ) && v > 10
        end

* Never assign the result of an if block.

        # Avoid:
        foo = if condition
          bar(blah, bleh)
        else
          baz(bluh, blih)
        end

        # Better:
        if condition
          foo = bar(blah, bleh)
        else
          foo = baz(bluh, blih)
        end

        # Avoid:
        foo = if condition
          short_expression
        else
          small_expression
        end

        # Better:
        foo = condition ? short_expression : small_expression

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

* When naming several related things, name them so that they become grouped
  together logically when sorted.  Towards this end, tend to put nouns before
  adjectives.  Think of the words as namespaces.  Examples:

        # Less desirable:
        opened_file
        current_file
        favourite_company
        twitter_token
        facebook_token
        current_page
        next_page

        # More desirable:
        file_opened
        file_current
        company_favourite
        token_twitter
        token_facebook
        page_current
        page_next

* After initially clarifying its meaning, use a very short identifier when
  a variable appears several times in a small area.  Examples:

        e = doodad.last_error
        if e.severe?
          log e
        else
          process e
        end

        def binomial_probability( num_successes, num_trials, prob_success, prob_failure )
          n, k, p, q = num_successes, num_trials, prob_success, prob_failure
          (
            n.facto / (
              k.facto * ( n - k ).facto
            )
          ) * p**k * q**(n-k)
        end

* When defining binary operators, name the argument "other".

* Prefer map over collect, find over detect, find_all over select.

* Write greppable code.  Don't build identifiers or external/remote names with
  concatenation or interpolation.

        # Bad
        class ExternalAPI
          def initialize
            @client = RESTClient.new
          end
          [ 'foo', 'bar' ].each do |x|
            define_method "process_#{x}".to_sym do
              @client.call "http://example.com/api/process-#{x}.xml"
            end
          end
        end

        # Better
        class ExternalAPI
          def initialize
            @client = RESTClient.new
          end
          def process_foo
            @client.call "http://example.com/api/process-foo.xml"
          end
          def process_bar
            @client.call "http://example.com/api/process-bar.xml"
          end
        end


## Comments

* Avoid comments; aim for self-explanatory code.

* Use yardoc and its conventions for API documentation.  http://yardoc.org/

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

* Restrict bare (unadorned) identifiers to "nearby" code, where possible, to
  reduce how much the reader has to search for definition or initialization.
  To this end, prefer decorated identifiers as much as possible, when given
  a choice:
  * Don't use accessor methods in a class code (use the instance variables themselves).
  * Prefix with `self.` for a class's own methods, including accessors.
  * Don't use `let` in specs.

* Use def self.method to define singleton methods.

* Symbols are for internal use only: If it comes in as input, or goes out as
  output, it should be a String. If you find yourself applying to_s to Symbols,
  they should have been Strings to begin with.  Avoid turning Strings into
  Symbols (just use the Strings).

* If you must add "global" methods, add them to Kernel (if you have to) and
  make them private.

* Avoid alias when alias_method will do.

* Write for Ruby 2.0+, except when required to maintain legacy code.

* Avoid needless metaprogramming.

* Don't engage in code golfing or newline golfing.

* Err on the side of more spaces or newlines.

* Make your code read vertically, not horizontally;
  make it tall, not wide;
  many short lines, not few long lines.

* Do not mess around in core classes when writing libraries.

* Keep things as simple as possible (but no simpler).

* Be consistent.

* Use common sense.
