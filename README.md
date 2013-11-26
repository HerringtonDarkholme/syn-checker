Style-Checker
===========
A Node-wrapped style checker for coding style. Notice: what it does is just _lexical_ matching against rules.

Intro
===========
This command line tool is written to handle the least consequential yet the most contentious stuff in programming.

Usage
===========
Command take the form like below:
`./chekcer -t --rule [dest] [--more-rules]`

No options are mandatory, but at least one option should be given to the checker.

* -t : file types to check. Supported file types are: j(JavaScript), c(SCSS) and h(slim).
Multiple types can be passed after one hyphen like `-jc`, which means checking both JavaScript and SCSS.
`-a` is an alias for all file types `-jch`. If no type is given, '-a' is default.

* --rule : specify which rule to check against. See `rules.json` for rule-list. Note that rules are written in JSON, so it should be converted from `camelCase` to `spinal-case`. Rules are classified into three file types, so the best way to specify rule is providing both type and rule arguments. Example : `./checker -j --trailing-space` => check JavaScript files against the rule 'trailingSpace'. Multiple rules can be specified in one check. If no rule is given, the program will check files against all available rules given the file types.

* dest : the destination of check. This option accepts filename as well as directory name. The directory is traversed recursively. Default destination is the current directory.

Dependencies
===============
1. GNU GREP : Support `-P` flag. [for mac](http://codelife.me/blog/2012/11/12/install-gnu-grep-in-mountain-lion/http://codelife.me/blog/2012/11/12/install-gnu-grep-in-mountain-lion/)
2. Node.Js : node's version should be v0.10 or above. This checker take advantages of `setImmediate`.

Installation
===============
1. clone this repository and `cd` to it
2. change `checker`'s access so as to execute it. `sudo chmod 755 checker`
3. configure the command location of grep. Modify `rules.json`. The `alias` key stores an dictionary for checker to lookup for the location of grep. Default value for grep is `/usr/local/bin/grep`. Change it to your own GNU GREP's installation path.
4. `./checker ~/destination/` (Check all files under the destination directory against all rules)

Configuration
===============
The rules can be found in `rules.json` (which is self-explanatory). Every rule is just a command that you can type in shell terminal. You can add or remove rules by your own predilection. What the checker does is concatenating file path to one command and executing it. For example, `./checker -j --leading-tab test.js` is translated to `grep -P '^\t+' test.js`. Shell commands can be used in rules. (Currently no pipe supported.)

Miscellaneous
===============
Under MIT licence. PULL request welcome!
