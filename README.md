Coqueror is a shell script which I am writing to practice shell scripting and which checks (and sometimes improves) formatting and syntax of other shell scripts.

See below for what you should likely use instead of this and what my references are, 
(my preliminary, subjective) target scripts' quality criteria and 
TODOs.

"Coque" is french and means "shell".

### Formatting/syntactic ideals

##### Ideal structure
1. Interpreter directive (hashbang): use `#!/usr/bin/env bash`, nothing else.
2. Header comment block 
3. `set -euo pipefail`
4. variable assignments
5. Functions
6. Code
7. *Cleanup boilerplate*

##### Commenting
 - Header comment block, definition for each function and other "major" comment blocks should have `###` in a line above and below its respective lines (*unspecific*)
 - Header comment:
   - script name and function at time of writing,
    - versioning reference
    - link to its repo,
    - links to relevant docs or manpages,
    - creation date (MM/YYYY)
 - TODO comments need to contain the word `TODO`
 - Avoid in-line comments longer than a few words
 - Comment should reference stuff below itself, not above
 - Function comments:
   -  a short description (no desc>shitty desc, tho)
   -  variables+arguments used/taken and 
   -  outputs+results returned 
 - For tests, comment what they test for - I **WILL** FORGET OTHERWISE

##### Indentations/NLs/Quotes/Braces/
- Indentation with 2 spaces each, no tabs!
- Avoid width > 80 chars, prefer inserting NL or use `<<EOF`style syntax 
- NL for each `|`/`||`/`&&`
- Variables should be double-quoted
- Variables should be in curly braces
- except for shell specials/position args (e.g. `"${NORMAL_VAR}"`,`"$@"` and `"$1"`)

##### Naming stuff:
- File name preferred to end in `.sh` (except when it's to be contained in a $PATH dir)
- Local var names in snake_case
- Global var names in ALL_CAPS
- Use "`function`" before function name
- **Always** use explicit paths when using wildcard expansion (e.g. `/home/dude/*` instead of just `*`)
  
##### `ìf/for/while`- and `case` statements: 
-   `; then` and `; do` go in the same line, 
-   `elif/else` go in their own line,
-   `fi/done`/`esac` go in their own line and with the opening statement vertically.
- Case statement options should have at least 3 lines containing the "`pattern)`", what to do if matched and the ";;", respectively; except where that'd be ridiculously over the top. `*)`should be their last, catch-all wildcard pattern

##### Testing stuff:
- Use `[[ ... ]]` ; don't use `[ ... ]` or `test ...`
- Test for string length zero/non-zero using `-z`/`-n`,
  e.g. ```if [[-z "${var_string} ]]; do```
- `<`and `>` do letters stuff; test math stuff inside `(() ... ))` where they do numbers stuff

##### Stuff I'll try to do but have no personal opinion of (ex Google Shell Style Guide):
- Store lists of items in arrays using `declare -a`
- Declare constants as `readonly`
- Have the "main code" wrapped in it's own function called "`main`" and have the last non-comment line of the script be a call to said function (i.e. `main "$@"`)

#### Stuff to avoid:
- Fiddle with SUID/GUID
- Put stuff into STDERR, have a "error printing + exit" function instead
- Using aliases inside a script (use a function if really needed)
  
### TODO

- Of the above stuff, extrapolate ways for Bash to comment on deficits

- Have it do a suggestion list (/dry-run) by default with list of stuff to be improved
  
- Check for presence of `set -euo pipefail`, offer setting it if not present

- Add a comment to target script when checked containing a code word & Coquerors version# at time of checking (debugging purposes)
  
### TOmaybeDO
- Form an opinion on the stuff in the above list that I don't have one on