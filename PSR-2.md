#PSR-2

The PSR-2 Coding Style Guide is an extension of PSR-1, which I reviewed in my last post.  The PSR standards were created and agreed to by a diverse group of PHP framework and library developers, so that all frameworks and libraries will be able to be used together with the same syntax.

PSR-1 laid out basically three naming conventions: 1. Classes should be named using StudlyCaps or upper Camel case, like so: class BlueMoon{}, 2. methods in the classes should be named in lower camel case, like so: public function setTime(), and 3. constants should be named with caps in snake case, like so: const VERSION_NUMBER =.

Let's expand this with PSR-2 which delves into how to style PHP code. This standard has been much needed to make all code easier to read and understand, and to let PHP developers know how their code should be styled. Here we go:

1. INDENT - Indent 4 spaces, not tabs.  The problem with tabs is when you go from developer to developer, tabs are different, and the code doesn't line up properly.  In most modern IDEs, you can set tabs to convert to spaces automatically. The 4 spaces is curious, since I've mostly used 3, but from my perspective I'm glad we finally put a stake in the ground.

2. LINE LENGTH - No hard limit on line length, the soft limit is 120 characters, however you should try to keep your lines under 80 characters for easier reading.  Don't leave a blank space at the end of the line after the semicolon, and of course, only one statement per line.

3. NAMESPACE - Use one blank line after a namespace declaration, and a blank line after a single or group of USE declarations.  The namespace must be the first line in the file after the PHP tag.  This makes developers more easily aware that the code is within a particular namespace or is using a particular alias for that namespace.  Here's an example:

#Example:
	namespace Vendor\Package;
	 
	use PrintInterface;
	use TextClass as TC;
	use Vendor2\ORM3\OrmHandler;
	 
	class SetUpPrint extends TC implements PrintInterface
	{
	    ...Do something
	}

4. CLASS - Opening braces for classes MUST go on the next line, and the closing brace must be on a line of its own at the end.   YEA!, I've been fighting Kerrigan for years, and since I code this way, I'm a happy camper.  After the closing brace of the class leave one blank line.

The class keyword should be in lower case.

Extends and implements keywords must be declared on the same line as the class.  If there is a list of implements you can put them each on a line below the class indented.

Omit the closing PHP tag if the file contains all PHP code.  This one has tripped up many a developer with blank lines after the closing PHP tag throwing an error.

#Here's two examples:
	class SetUpPrint extends TC implements PrintInterface
	{
	    ...Do something
	}
	 
	class SetUpPrint extends TextClass implements
	    \PrintInterface
	    \FontInterface
	    \Internationlization
	{
	    ... Do something
	}

5. METHOD - Opening braces for methods must go on the next line, and a separate line for the closing brace. Yea! again.

Parenthesis should butt up against the method name with no spaces, and there should be not be a space after the open parenthesis or before the closing parenthesis.

Visibility or scope, like public, protected, and private must be declared on all methods.  The order of declaration should be abstract and final, visibility, and last static before the function keyword.

Method names must not start with an _ .  This can cause some confusion with __contruct type or other PHP magic constants.

Method arguments: commas should have a space after the comma, but none before the comma.  Arguments can be put on multiple lines but they must be indented. If multiple lines are used for arguments, the opening parenthesis is on the method line, and closing parenthesis and the opening method brace are on the same line.

Here's the example:
	class SetUpPrint extends TC implements PrintInterface
	{
	    final public static function cannedText($arg1, $arg2, $arg3)
	    {
	        private $count = 0;
	        public  $team_id = null;
	 
	        ... Do something
	    }
	 
	    private function calculateRate(
	        $arg1,
	        $arg2,
	        $arg3
	    ) {
	 
	        ... Do Something
	 
	    }
	}

The second method is harder to read, but every once and awhile is needed.

6. CLOSURE - For the most part closures have the same styling as methods with these differences:

Closures must have a space after the function keyword.

When used with the use keyword, there should be a space before and after the use keyword.

#Here's the example:
	$closureRouting = function ($arg1, $arg2) {
	    ... Do something
	};
	 
	$closureRouting2 = function () use ($var1, $var2) {
	    ... Do something
	};

7. PROPERTY - Declare a visibility on all properties.

Never use the var keyword, this is used with  JavaScript and would cause some confusion.

Use one property per statement instead of chaining properties on one line.

No underscores before the property name, like $_income, instead use $income.  The underscore was used in some frameworks and can be confused with PHP magic variables.

Not this:
1	private $count = $_items = 0;
2	public  $_guide_id = $team_id = '';

Instead, like this:
1	private $count = 0;
2	private $items = 0;
3	public  $guide_id = null;
4	public  $team_id = '';

6. CONTROL - Control structures, like IF, WHICH, FOR, and FOREACH must have one space before the condition parenthesis.

The parenthesis should not have a space after the opening parenthesis or a space before the closing parenthesis.

The opening brace should have one space after the closing parenthesis and go on the same line, oh well I can't win them all.

The structured body should be indented.

The closing brace should have a line of its own.

#Here are some examples of several control structures:
	if ($i == 1) {
	    Do something;
	} elseif ($i == 2) {
	    Do something else;
	} else {
	    Do a third thing;
	{
	 
	for ($i = 0; $i < 10, $i++) {
	    ... Do something;
	}
	 
	foreach ($condition as $key => $value) {
	    ... Do something
	}
	 
	try {
	    ...Do something, and throw some errors
	} catch (firstError $e) {
	    ... Do something with the error
	} catch (secondError $e) {
	    ... Do something else with an error
	}

8. SWITCH - The case keywords should be indented from the switch keyword. There should be a line between each case block with the exception of the first case.

Inside the case, the break keyword should be indented with the rest of the code in the case body.

There must be a comment, such as "// No break" when a fall-through is intentional in a non-empty case, like so:
	switch ($condition) {
	    case 0:
	        echo 'The condition is 0';
	        break;
	 
	    case 1:
	        echo 'The condition is 1. ';
	        // No break
	 
	    case 2:
	 
	    case 3:
	 
	    case 4:
	        echo 'The condition has been set';
	        return;
	 
	    default:
	        echo 'No condition was set';
	        break;
}

#
9. KEYWORD - Here's one that I'm guilty of.  Keywords, like true, false, and null show be in lower case.  I've always put them in upper case for visibility, not anymore.  They should be set up like so:
	if ($turn == true) {
	    Do something;
	} elseif ($turn == false) {
	    Do something else;
	else {
	    Do a third thing;
	{

That's it for PSR-2.  It is interesting to note that this style guide isn't just one developer's view of the world, which has been the problem with all the other style guides. The way this standard was developed was to poll all the members of FIG as to each coding style to determine the preference of a majority of the members, considering that the members of FIG cover a broad spectrum of PHP development, these coding styles should be considered not only a standard, but what the PHP community wants to see when reading code.  Thus a developer should strive to code with this style, knowing it is what other developers are expecting.  Thus a standard is born.

As an aside, in both NetBeans and Eclipse you can set up this style in the editor, and then hit a key sequence, and your selected code will be formatted to this style, nice.

To configure the format in NetBeans, go to Tools->Options->Editor->Formatting. You can set the indents for all languages. To set the rest of the style, click the PHP drop down under "Language:" and then in "Category:" drop down you can set the rest of the styles. Once formatting is set in NetBeans, all you have to do is select the code you want to format, and do an Alt-Shift-F and presto your code is formatted. I find I use this a lot while coding to keep my code looking good.


([Visit For details to] http://www.geekgumbo.com/2013/05/19/psr-2-coding-style-guide/)
