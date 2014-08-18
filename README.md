Php Code Style Guidelines
=========================

##Abstract

The first condition for a code to be smart is to look smart. A code written in a well indented, properly styled way is easy on the eye, therefore, more understandable compared to a code which makes you dizzy by looking at it.

In an organization where multiple developers work on a single project’s code base, it is very important that everyone writes appropriately styled code which others can quickly understand. To achieve that, every developer should know what coding style to follow primarily. This document is prepared to bring every PHP developer in this organization on a common ground in that regard.

This document describes the PHP language standards proposed to be followed by all the PHP developers of this organization. These standards are a combination of **PHP Pear coding standards** and **Zend framework coding standards**, both recommended as best options to adapt in order to write a well formatted PHP code.

##Indenting and Line Length

Use an indent of 4 spaces, with no tabs. This helps to avoid problems with conflicts, diffs, patches, GIT  / SVN history and annotations. For your editor you should set the indent (via tab key) to 4 spaces.

##PHP Code Demarcation

PHP code must always be delimited by the full-form, standard PHP tags:

```
<?php
 
?>
```

Short tags are never allowed. For files containing only PHP code, the closing tag must always be omitted.

##Strings

###String Literals

When a string is literal (contains no variable substitutions), the apostrophe or "single quote" should be used to demarcate the string:

```
$a = 'Example String';
```

###String Literals Containing Apostrophes

When a literal string itself contains apostrophes, it is permitted to demarcate the string with quotation marks or "double quotes": 

```
$sql = "SELECT `id`, `name` from `people` "
     . "WHERE `name`='Fred' OR `name`='Susan'";
```

This syntax is preferred over escaping apostrophes as it is much easier to read. 

###Variable Substitution

Variable substitution is permitted using either of these forms: 

```
$greeting = "Hello $name, welcome back!";

$greeting = "Hello {$name}, welcome back!";
```

For consistency, this form is not permitted:

```
$greeting = "Hello ${name}, welcome back!";
```

###String Concatenation

Strings must be concatenated using the "." operator. A space must always be added before and after the "." operator to improve readability:

```
$company = 'Zend' . ' ' . 'Technologies';
```

When concatenating strings with the "." operator, it is encouraged to break the statement into multiple lines to improve readability. In these cases, each successive line should be padded with white space such that the "." operator is aligned under the "=" operator:

```
$sql = "SELECT `id`, `name` FROM `people` "
     . "WHERE `name` = 'Susan' "
     . "ORDER BY `name` ASC ";
```

##Arrays

###Numerically Indexed Arrays

When declaring indexed arrays with the Array function, a trailing space must be added after each comma delimiter to improve readability:

```
$sampleArray = array(1, 2, 3, 'Zend', 'Studio');
```

It is permitted to declare multi-line indexed arrays using the `array` construct. In this case, each successive line must be padded with spaces such that beginning of each line is aligned:

```
$sampleArray = array(1, 2, 3, 'Zend', 'Studio',
                     $a, $b, $c,
                     56.44, $d, 500);
```

Alternately, the initial array item may begin on the following line. If so, all successive lines should be padded at one indentation level greater than the line containing the array declaration; the closing parenthesis should be on a line by itself at the same indentation level as the line containing the array declaration:

```
$sampleArray = array(
    1, 2, 3, 'Zend', 'Studio',
    $a, $b, $c,
    56.44, $d, 500,
);
```

When using this latter declaration, it is encouraged to use a trailing comma for the last item in the array; this minimizes the impact of adding new items on successive lines, and helps to ensure no parse errors occur due to a missing comma.

###Associative Arrays

When declaring associative arrays with the Array construct, breaking the statement into multiple lines is encouraged. In this case, each successive line must be padded with white space such that the keys are aligned. For readability, various assignment operators may (optionally) be aligned with each other:

```
$sampleArray = array('firstKey' => 'firstValue',
                     'secondKey' => 'secondValue');
//or
$sampleArray = array('firstKey'  => 'firstValue',
                     'secondKey' => 'secondValue');
```

Alternately, the initial array item may begin on the following line. If so, all successive lines should be padded at one indentation level greater than the line containing the array declaration; the closing parenthesis should be on a line by itself at the same indentation level as the line containing the array declaration. The `=>` assignment operators should be padded with one space from each side. For readability, various assignment operators may (optionally) be padded to align with each other.

```
$sampleArray = array(
    'firstKey' => 'firstValue',
    'secondKey' => 'secondValue',
);
//or
$sampleArray = array(
    'firstKey'  => 'firstValue',
    'secondKey' => 'secondValue',
);
```

When using this latter declaration, it is encouraged to use a trailing comma for the last item in the array.

##Control Structures

These include `if`, `for`, `while`, `switch`, etc. Control statements should have one space between the control keyword and opening parenthesis (to distinguish them from function calls) and a single space after the closing parenthesis before the opening brace. The opening brace is written on the same line as the conditional statement. The closing brace is always written on its own line. Any content within the braces must be indented using four spaces.

```
if ($a != 2) {
    $a = 2;
}
```

You are strongly encouraged to always use curly braces even in situations where they are technically optional. Having them increases readability and decreases the likelihood of logic errors being introduced when new lines are added.

Within the conditional statements between the parentheses, operators must be separated by spaces for readability. Inner parentheses are encouraged to improve logical grouping for larger conditional expressions.

```
while ($a != 2 && ($a % 2 == 0 || $a % 5 == 0) && $a > 0) {
```

###Split Long Conditional Statements

Long conditional statement with several clauses may be broken down to multiple lines. In such a case, break the line prior to a logic operator, and pad the line to align under the first character of the conditional clause. The closing parenthesis and the opening brace will then be placed on a line at an indentation level equivalent to the opening control statement.

```
if (($a == $b)
    && ($b == $c)
    || (Foo::CONST == $d)
) {
    $a = $d;
}
```

Keeping the operators at the beginning of the line has two advantages: It is trivial to comment out a particular line during development while keeping syntactically correct code. Furthermore the logic is kept at the front where it's not forgotten.

The best case is of course when the line does not need to be split. It might be better to simplify the clause long enough to be split. You could express condition as variables and compare them in the condition. This has the benefit of "naming" and splitting the condition sets into smaller, better understandable chunks:

```
<?php

$is_foo = ($condition1 || $condition2);
$is_bar = ($condition3 && $condtion4);
if ($is_foo && $is_bar) {
    // ....
}
?>
```

###If/Else/Elseif 

For `if` statements that include `elseif` or `else`, the formatting conventions are similar to the `if` construct. The following examples demonstrate proper formatting for `if` statements with `else` and/or `elseif` constructs:

```
if ($a != 2) {
    $a = 2;
} else {
    $a = 7;
}
 
if ($a != 2) {
    $a = 2;
} elseif ($a == 3) {
    $a = 4;
} else {
    $a = 7;
}
 
if (($a == $b)
    && ($b == $c)
    || (Foo::CONST == $d)
) {
    $a = $d;
} elseif (($a != $b)
          || ($b != $c)
) {
    $a = $c;
} else {
    $a = $b;
}
```

###Switch

All content within the `switch` statement must be indented using four spaces. Content under each `case` statement must be indented using an additional four spaces.

```
switch ($numPeople) {
    case 1:
        break;
 
    case 2:
        break;
 
    default:
        break;
}
```

It is recommended not to omit the construct `default` from a switch statement.

**Note:** It is sometimes useful to write a `case` statement which falls through to the next `case` by not including a `break` or `return` within that `case`. To distinguish these cases from bugs, any `case` statement where `break` or `return` are omitted should contain a comment indicating that the `break` was intentionally omitted.

###Ternary operators

The same rule as for `if` clauses also applies for the ternary operator: It may be split onto several lines, keeping the question mark and the colon at the front.

```
<?php

$a = $condition1 && $condition2
    ? $foo : $bar;

$b = $condition3 && $condition4
    ? $foo_man_this_is_too_long_what_should_i_do
    : $bar;
?>
```

##Classes

###Class Declaration

The brace should always be written on the line underneath the class name. All code in a class must be indented with four spaces.

It is recommended to define only one class in each PHP file. Placing additional code in class files is discouraged. In such files, two blank lines must separate the class from any additional PHP code in the class file.

The following is an example of an acceptable class declaration:

```
/**
* Documentation Block
*/
class SampleClass
{
    // all contents of class
    // must be indented four spaces
}
```

Classes that extend other classes or which implement interfaces should declare their dependencies on the same line when possible.

```
class SampleClass extends FooAbstract implements BarInterface
{
}
```

If the line length exceeds the maximum line length, break the line before the `extends` and/or `implements` keywords, and pad those lines by one indentation level.

```
class SampleClass
    extends FooAbstract
    implements BarInterface
{
}
```

If the class implements multiple interfaces and the declaration exceeds the maximum line length, break after each comma separating the interfaces, and indent the interface names such that they align.

```
class SampleClass
    implements BarInterface,
               BazInterface
{
}
```

###Class Member Variables

Any variables declared in a class must be listed at the top of the class, above the declaration of any methods.

The `var` construct is discouraged. Member variables always declare their visibility by using one of the `private`, `protected`, or `public` modifiers. Giving access to member variables directly by declaring them as `public` is permitted but discouraged in favor of accessor methods (set & get).

##Function Definitions

The brace should always be written on the line underneath the function name. Space between the function name and the opening parenthesis for the arguments is not permitted.

```
<?php
function fooFunction($arg1, $arg2 = '')
{
    if (condition) {
        statement;
    }
    return $val;
}
?>
```

Arguments with default values go at the end of the argument list. Always attempt to return a meaningful value from a function if one is appropriate. Here is a slightly longer example:

```
<?php
function connect(&$dsn, $persistent = false)
{
    if (is_array($dsn)) {
        $dsninfo = &$dsn;
    } else {
        $dsninfo = DB::parseDSN($dsn);
    }

    if (!$dsninfo || !$dsninfo['phptype']) {
        return $this->raiseError();
    }

    return true;
}
?>
```

**Note:** Pass-by-reference is only permitted in a method declaration. Call-time pass-by-reference is strictly prohibited. The return value must not be enclosed in parentheses. This can hinder readability, in additional to breaking code if a method is later changed to return by reference.

```
/**
 * WRONG
 */
function bar()
{
    return($bar);
}

/**
 * RIGHT
 */
function bar()
{
    return $bar;
}
```

###Class Method Declaration

Methods inside classes must always declare their visibility by using one of the `private`, `protected`, or `public` modifiers.

The following is an example of an acceptable method declaration in a class:

```
/**
* Documentation Block Here
*/
class Foo
{
    /**
     * Documentation Block Here
     */
    public function bar()
    {
        // all contents of function
        // must be indented four spaces
    }
}
```

###Split Function Definitions

Functions with many parameters may need to be split onto several. The first parameters may be put onto the same line as the function name if there is enough space. Subsequent parameters on following lines are to be indented 4 spaces. The closing parenthesis and the opening brace are to be put onto the next line, on the same indentation level as the `function` keyword.

```
<?php

function someFunctionWithAVeryLongName($first, $secondParam,
    $third = null, $fourth = false, $fifthParameter = 123.12,
    $sixthParam = true
) {
    //....
}
?>
```

###Function and Method Usage

Function arguments should be separated by a single trailing space after the comma delimiter. The following is an example of an acceptable invocation of a function that takes three arguments:

```
threeArguments(1, 2, 3);
```

In passing arrays as arguments to a function, the function call may include the `array` construct and may be split into multiple lines to improve readability. In such cases, the normal guidelines for writing arrays still apply:

```
threeArguments(array(1, 2, 3), 2, 3);

threeArguments(array(1, 2, 3, 'Zend', 'Studio',
                     $a, $b, $c,
                     56.44, $d, 500), 2, 3);

threeArguments(array(
    1, 2, 3, 'Zend', 'Studio',
    $a, $b, $c,
    56.44, $d, 500
), 2, 3);
```

##Function Calls

Functions should be called with no spaces between the function name, the opening parenthesis, and the first parameter; spaces between each comma and next parameter, and no space between the last parameter, the closing parenthesis, and the semicolon. Here's an example:

There should be one space on either side of an equals sign used to assign the return value of a function to a variable.

```
<?php
$var = foo($bar, $baz, $quux);
?>
```

In the case of a block of related assignments, more space may (optionally) be inserted to promote readability:

```
<?php
$short         = foo($bar);
$long_variable = foo($baz);
?> 
```

The rule may be ignored when the length of the variable name is at least 8 characters longer/shorter than the previous one:

```
<?php
$short = foo($bar);
$thisVariableNameIsVeeeeeeeeeeryLong = foo($baz);
?>
```

To support readability, parameters in subsequent calls to the same function/method may (optionally) be aligned by parameter name:

```
<?php

$this->callSomeFunction('param1',     'second',        true);
$this->callSomeFunction('parameter2', 'third',         false);
$this->callSomeFunction('3',          'verrrrrrylong', true);
?> 
```

###Split Function Call

When calling functions or methods with many parameters, it is allowed to split parameters in function calls onto several lines.

```
<?php

$this->someObject->subObject->callThisFunctionWithALongName(
    $parameterOne, $parameterTwo,
    $aVeryLongParameterThree
);
?> 
```

Several parameters per line are allowed. Parameters need to be indented 4 spaces compared to the level of the function call. The opening parenthesis is to be put at the end of the function call line; the closing parenthesis gets its own line at the end of the parameters. This shows a visual end to the parameter indentations and follows the opening/closing brace rules for functions and conditionals.

The same applies not only for parameter variables, but also for nested function calls and arrays.

```
<?php

$this->someObject->subObject->callThisFunctionWithALongName(
    $this->someOtherFunc(
        $this->someEvenOtherFunc(
            'Help me!',
            array(
                'foo'  => 'bar',
                'spam' => 'eggs',
            ),
            23, NULL, FALSE
        ),
        $this->someEvenOtherFunc()
    ),
    $this->wowowowowow(12)
);
?> 
```

Nesting those function parameters is allowed if it helps to make the code more readable, even if the characters per line limit is not reached.

Concatenated function calls may be split onto several lines. When doing this, all subsequent lines are indented by 4 spaces and begin with the `->` arrow.

```
<?php

$someObject->someFunction("some", "parameter")
    ->someOtherFunc(23, 42)
    ->andAThirdFunction();
?>
```

###Split long assignments onto several lines

Assignments may be split onto several lines when the character/line limit is exceeded. The equal sign has to be positioned onto the following line, and indented by 4 characters.

```
<?php

$GLOBALS['TSFE']->additionalHeaderData[$this->strApplicationName]
    = $this->xajax->getJavascript(t3lib_extMgm::siteRelPath('nr_xajax'));
?>
```

##Comments

Comments are strongly encouraged. A general rule of thumb is that if you look at a section of code and think "Wow, I don't want to try and describe that", you need to comment it before you forget how it works.

C style comments (/* */) and standard C++ comments (//) are both fine. Use of Perl/shell style comments (#) is discouraged.

It is encouraged to provide complete inline documentation comment blocks (docblocks). Please read the [Inline Documentation](#inline-documentation) sections to learn the specifics of writing docblocks.

##Including Code

When unconditionally including a file, use `require_once`. When conditionally including a file, use `include_once`. Either of these will ensure that class files are included only once. They share the same file list, so you don't need to worry about mixing them - a file included with `require_once` will not be included again by `include_once`.

`include_once` and `require_once` are statements, not functions. Parentheses should not surround the subject filename.

##Example URLs

Use `example.com`, `example.org` and `example.net` for all example URLs and email addresses, per RFC 2606.

##Naming Conventions

###Global Variables and Functions

If your code needs to define global variables, their names should start with a single underscore followed by the file/class/function name and another underscore to avoid conflicts. For example, the `ExampleClass` class should define the global variable `example_global` as `$_ExampleClass_example_global`.

Global functions should be named using the "studly caps" style (also referred to as "bumpy case" or "camel caps"). If there are chances of collision between function names of different files, then they should have the file/package name as a prefix. The initial letter of the name (after the prefix) is lowercase, and each letter that starts a new "word" is capitalized. For example:

`ExampleFile_exampleTestFunction()`

###Classes

Classes should be given descriptive names. Avoid using abbreviations where possible. Class names should always begin with an uppercase letter. The class hierarchy may also be reflected in the class name, each level of the hierarchy separated with a single underscore. Examples of good class names are:

ListHelper

`My_Class_HelperClass_ListHelper` (in my/classes/helperclasses/ListHelper.php)

`My_Classes_HelperClasses_ListHelper` (in my/classes/helperclasses/ListHelper.php)

###Class Variables and Methods

Class variables (a.k.a properties) and methods should be named using the "studly caps" style (also referred to as "bumpy case" or "camel caps"). Some examples (these would be "public" members):

`$counter`, `$exampleProperty`, `connect()`, `getData()`, `updateStatusById()`

Private class members are preceded by a single underscore. For example:

`$_status`, `$_examplePrivate`, `_sort()`, `_getConnection()`

Protected class members are not preceded by a single underscore. For example:

`protected $somevar`, `protected function initTree()`

###Constants

Constants should always be all-uppercase, with underscores to separate words. To avoid conflicts, prefix constants with global scope with the uppercased name of the file/package they are used in. Some examples:

`DB_DATASOURCENAME`, `SERVICES_FACEBOOK_APPID`

##File Formats

All files must use ISO-8859-1 or UTF-8 character encoding. It is important that the database connection, PHP files, template files, and included files all should have the same encoding. If not, then necessary encoding conversions must be applied.

##`E_STRICT`-compatible code

The code must be `E_STRICT`-compatible. This means that it must not produce any notices, warnings or errors when PHP's error reporting level is set to `E_ALL | E_STRICT`.

##Best practices

There are things which are mostly subject of personal preference and not strictly defined as standards. There may be no reasons to use one way in preference to another. Such best practices are only recommended to keep consistency within code.

###Readability of code blocks

Related lines of code should be grouped into blocks, separated from each other to keep readability as high as possible. The definition of "related" depends on the code.

For example:

```
<?php

if ($foo) {
    $bar = 1;
}
if ($spam) {
    $ham = 1;
} elseif ($pinky) {
    $brain = 1;
}
$myClass = new MyClass();
$myData = $myClass->getMyData();
return $myData;
?> 
```

is a lot easier to read when separated:

```
<?php

if ($foo) {
    $bar = 1;
}

if ($spam) {
    $ham = 1;
} elseif ($pinky) {
    $brain = 1;
}

$myClass = new MyClass();
$myData = $myClass->getMyData();

return $myData;
?> 
```

###Return early

To keep readability in functions and methods, it is wise to return early if simple conditions apply that can be checked at the beginning of a method. For example:

```
<?php

function foo($bar, $baz)
{
    if ($foo) {
        //assume
        //that
        //here
        //is
        //the
        //whole
        //logic
        //of
        //this
        //method
        return $calculated_value;
    } else {
        return null;
    }
}
?> 
```

It's better to return early, keeping indentation and brain power needed to follow the code low.

```
<?php

function foo($bar, $baz)
{
    if (!$foo) {
        return null;
    }

    //assume
    //that
    //here
    //is
    //the
    //whole
    //logic
    //of
    //this
    //method
    return $calculated_value;
}
?> 
```

###Ternary Operator

To keep readability and simplicity, it is preferred to use ternary operator instead of `if`/`else` for single line statements wherever possible. For example:

```
<div class="<?php if($a == $b && $c == $d){ echo 'even'; } else { echo 'odd'; } ?>">
    ...
    ...
</div>
```

Using a ternary operator instead will make a better understanding:

```
<div class="<?php echo (($a == $b && $c == $d) 'even' : 'odd'); ?>">
    ...
    ...
</div>
```

**Note:** It is recommended to wrap the ternary operator within a set of parenthesis to avoid logical errors. For example:

```
//Wrong
echo '<div ' . count($photos) > 1 ? "class='slider'" : "class='image'" . '>';

//PHP will interpret the above statement as
//echo '<div ' . count($photos) > 1 ? ("class='slider'") : ("class='image'" . '>');

//Right
echo '<div ' . (count($photos) > 1 ? "class='slider'" : "class='image'") . '>';
```

While stacking ternary operators, use parenthesis to avoid misinterpretation of your code. For example:

```
$b = 'a';
$c = 'd';

//Wrong
echo $b == 'a' ? 2 : $c == 'a' ? 1 : 0; //outputs 1 instead of 2

//PHP will interpret the above statement as
//echo ($b == 'a' ? 2 : $c == 'a') ? 1 : 0;
//The expression in parenthesis returns 2 which evaluates to boolean TRUE

//Right
echo $b == 'a' ? 2 : ($c == 'a' ? 1 : 0);

```

##Inline Documentation

The following section describes the inline documentation according to documentation block (docblock) standards.

These standards are not being strictly imposed but it is encouraged that you adapt these standards as much as possible. It is strongly recommended to write documentation blocks for at least functions and methods.

###Documentation Format

Following are the basic standards compatible with the phpDocumentor format. Describing the phpDocumentor format is beyond the scope of this document. For more information, visit: [http://phpdoc.org/](http://phpdoc.org/).

All class files should contain a "file-level" docblock at the top of each file and a "class-level" docblock immediately above each class. Examples of such docblocks can be found below.

###Files

Every file that contains PHP code should have a docblock at the top of the file that contains these phpDocumentor tags:

```
/**
* Short description for file
*
* Long description for file (if any)...
*
* LICENSE: Some license information
*
* @category   Category
* @package    Package
* @subpackage Subpackage
* @copyright  Copyright Text and hyperlink (if any)
* @license    License hyperlink and type
* @version    Version
* @link       Hyperlink to file/package
* @since      File available since Release
*/
```

###Classes

Every class should  have a docblock that contains these phpDocumentor tags:

```
/**
* Short description for class
*
* Long description for class (if any)...
*
* @category   Category
* @package    Package
* @subpackage Subpackage
* @copyright  Copyright Text and hyperlink (if any)
* @license    License hyperlink and type
* @version    Version
* @link       Hyperlink to file/package
* @since      Class available since Release
* @deprecated Class deprecated in Release
*/
```

###Functions

Every function, including object methods, should have a docblock that contains at a minimum:



- A description of the function
- All of the arguments
- All of the possible return values

It is not necessary to use the `@access` tag because the access level is already known from the `public`, `private`, or `protected` modifier used to declare the function.

If a function or method may throw an exception, use `@throws` for all known exception classes:

```
@throws exceptionclass [description]
```

**Note:** Although these standards are not compulsory to follow (as stated above), yet it is advised that you write a document block for functions and methods containing the minimum elements described in bullets above.

####Example

```
/**
 * Quotes arg2 into arg1
 *
 * This method quotes the integer carried by arg2 into the string
 * carried by arg1. This method uses the PHP function sprintf
 * and returns the resulting string. FALSE if the integer was 0.
 *
 * @param string $arg1 the string to quote
 * @param int    $arg2 an integer containing some value to quote.
 *                     Indent to the description's starting point
 *                     if it exceeds single line.
 *
 * @return string the string returning some value. FALSE if the
 *                operation was unsuccessful.
 *
 * @throws Exception the std exception containing message that the
 *                   input arguments are not valid. Thrown if the
 *                   arg1 is empty or null or not a string.
 *
 * @access public
 * @static
 * @since Method available since Release
 * @deprecated Method deprecated in Release
 */
public static function myStaticFunction($arg1, $arg2){
    //...
}
```
