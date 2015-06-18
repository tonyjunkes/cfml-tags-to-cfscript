# CFML Tag to Script Conversions
#####A collection of examples demonstrating the conversion of CFML code blocks written in tags to CFScript.

**Currently a work in progress!**

> This is not the CFScript syntax documentation you're (possibly) looking for. That awesome piece of work, by Adam Cameron, can be found [here](https://github.com/adamcameron/cfscript) and is highly recommended as a reference to the content you'll find here.

The examples in this document are an attempt to demonstrate conversions of CFML tag-based code to script-based code as a way of learning / migrating to CFScript. It is assumed that you already have a relatively firm understanding of the ColdFusion Markup Language (at least on a tag-based level). For the sake of modernity, the converted examples will be written to comply (from an agnostic approach) with the most current versions of the various CFML engines at the time of writing - (ColdFusion 11, Railo 4.2 & Lucee 4.5).

## Table of Contents
1. [Comments](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#comments)
2.  [Variables](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#variables)
3. [Operators](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#operators)
 - [Decision](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#decision)
 - [Increment / Decrement](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#increment--decrement)
 - [Inline Assignment](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#inline-assignment)
 - [Boolean](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#boolean)
 - [Ternary & Null-Coalescing](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#ternary--null-coalescing)
4. [Conditionals](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#conditionals)
 - [if / else if / else](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#if--else-if--else)
 - [Switch](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#switch)
 - [Try / Catch / Finally](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#try--catch--finally)
5. [Iterations](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#iterations)
 - [Index Loop](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#index-loop)
 - [Array Loop](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#array-loop)
 - [Struct Loop](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#struct-loop)
 - [List Loop](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#list-loop)
 - [Query Loop](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#query-loop)


### Comments

_**Tags:**_
```coldfusion
<!--- I'm a single-line comment. --->

<!---
I'm a multi-
line comment.
--->
```

_**Script:**_
```coldfusion
<cfscript>

// I'm a single-line comment.
// Notice that CFScript code within a ".cfm" file must be wrapped in <cfscript> tags.

/*
I'm a multi-
line comment.
*/

</cfscript>
```

### Variables

_**Tags:**_
```coldfusion
<!--- Some simple variable statements in tags --->

<!--- Default variable declarations --->
<cfparam name="title" default="">
<cfparam name="views" type="numeric" default=0>

<!--- Regular assignment --->
<cfset title = "Tags";
<cfset views = 1;
<cfset page = "Title: #title#, Number: #views#">
```

_**Script:**_
```coldfusion
<cfscript>

// Some simple variable statements in script

// Default variable declarations
param name="title" default="";
param name="views" type="numeric" default=0;

// Regular assignment
title = "Script";
views = 2;
page = "Title: #title#, Number: #views#";
// or
page = "Title: " & title & ", " & "Number: " & views;

</cfscript>
```

### Operators

#### Decision

_**Tags:**_
```coldfusion
<cfset x = 1>
<cfset y = x EQ 1>
<cfset y = x NEQ 1>
<cfset y = x LT 1>
<cfset y = x GT 1>
<cfset y = x LTE 1>
<cfset y = x GTE 1>
```

_**Script:**_
```coldfusion
<cfscript>

// All tag based operators still work in script
// There are also these equivalents

x = 1;
y = x == 1;
y = x != 1;
y = x < 1;
y = x > 1;
y = x <= 1;
y = x >= 1;

</cfscript>
```

#### Increment / Decrement

_**Tags:**_
```coldfusion
<cfset x = x + 1>
<cfset x = x - 1>
```

_**Script:**_
```coldfusion
<cfscript>

x = x++; // x = x + 1;
x = x--; // x = x - 1;

</cfscript>
```

#### Inline Assignment

_**Tags:**_
```coldfusion
<cfset x = x + 3>
<cfset x = x - 3>
<cfset x = x / 3>
<cfset x = x * 3>
<cfset x = x % 1>
<!--- or --->
<cfset x = x MOD 1>
```

_**Script:**_
```coldfusion
<cfscript>

// x = x + 3;
x += 3;
// x = x - 3;
x -= 3;
// x = x / 3;
x /= 3;
// x = x * 3;
x *= 3;
//x = x % 3;
x % 3;

</cfscript>
```

#### Boolean

_**Tags:**_
```coldfusion
<cfset NOT x>
<cfset x EQ 1 AND y EQ 2>
<cfset x EQ 1 OR y EQ 2>
```

_**Script:**_
```coldfusion
<cfscript>

!x;
x == 1 && y == 2;
x == 1 || y == 1;

</cfscript>
```

#### Ternary & Null-Coalescing

_**Tags:**_
```coldfusion
<!--- Ternary --->
<cfset x = "">
<cfset y = len(x) ? x : "something else">

<!--- Null-Coalescing --->
<cfset y = z ?: "something else">
```

_**Script:**_
```coldfusion
<cfscript>

// Ternary
x = "";
y = len(x) ? x : "something else";

// Null-Coalescing
y = z ?: "something else";

</cfscript>
```

### Conditionals

#### if / else if / else

_**Tags:**_
```coldfusion
<cfset count = 10>
<cfif count GT 20>
	<cfoutput>#count#</cfoutput>
<cfelseif count EQ 8>
	<cfoutput>#count#</cfoutput>
<cfelse>
	<cfoutput>#count#</cfoutput>
</cfif>
```

_**Script:**_
```coldfusion
<cfscript>

count = 10;
if (count > 20) {
	writeOutput(count);
} else if (count == 8) {
	writeOutput(count);
} else {
	writeOutput(count);
}

</cfscript>
```

#### Switch

_**Tags:**_
```coldfusion
<cfset fruit = "">
<cfswitch expression="#fruit#">
    <cfcase value="Apple">
        <!--- Some apple stuff --->
    </cfcase>
    <cfcase value="Orange">
        <!--- Some orange stuff --->
    </cfcase>
    <cfcase value="Kiwi">
        <!--- Some kiwi stuff --->
    </cfcase>
    <cfdefaultcase>
        <!--- Some default stuff --->
    </cfdefaultcase>
</cfswitch>
```

_**Script:**_
```coldfusion
<cfscript>

fruit = "";
switch (fruit) {
	case "Apple":
		// Do apple stuff
	break;
	case "Orange":
		// Do apple stuff
	break;
	case "Kiwi":
		// Do kiwi stuff
	break;
	default:
		// Do default stuff
	break;
}

</cfscript>
```

#### Try / Catch / Finally

_**Tags:**_
```coldfusion
<cftry>
	<cfset x = y + z>
	<cfcatch type="any">
		<cfdump var="#cfcatch#">
	</cfcatch>
	<cffinally>
		<cfoutput>Finally at the end.</cfoutput>
	</cffinally>
</cftry>
```

_**Script:**_
```coldfusion
<cfscript>

try {
	x = y + z;
}
catch(any e) {
	writeDump(e);
}
finally {
	writeOutput("Finally at the end");
}

</cfscript>
```

### Iterations

#### Index Loop

_**Tags:**_
```coldfusion
<cfloop index="i" from="1" to="10">
	<cfoutput>#i#</cfoutput>
</cfloop>
```

_**Script:**_
```coldfusion
<cfscript>

for (i = 1; i <= 10; i++) {
	writeOutput(i);
}

</cfscript>
```

#### Array Loop

_**Tags:**_
```coldfusion
<!--- Define our array --->
<cfset myArray = ["a", "b", "c"]>

<!--- By index --->
<cfloop index="i" from="1" to="#arrayLen(myArray)#">
	<cfoutput>#myArray[i]#</cfoutput>
</cfloop>

<!--- By array --->
<cfloop index="currentIndex" array="#myArray#">
	<cfoutput>#currentIndex#</cfoutput>
</cfloop>

<!--- By arrayEach() --->
<cfset arrayEach(myArray, function(element, index) {
	<cfoutput>#element# : #index#</cfoutput>
})>
```

_**Script:**_
```coldfusion
<cfscript>

// Define our array
myArray = ["a", "b", "c"];

// By index
// Note the use of the newer member function syntax for arrayLen()
for (i = 1; i <= myArray.len(); i++) {
	writeOutput(myArray[i]);
}

// By array
for (currentIndex in myArray) {
	writeOutput(currentIndex);
}

// By arrayEach()
myArray.each(function(element, index) {
	writeOuput(element & " : " & index);
});

</cfscript>
```

#### Struct Loop

_**Tags:**_
```coldfusion
<!--- Define our struct --->
<cfset myStruct = {name: "Tony", state: "Florida"}>

<!--- By struct --->
<cfloop item="currentKey" array="#myStruct#">
	<cfoutput><li>#currentKey# : #myStruct[currentKey]#</li></cfoutput>
</cfloop>

<!--- By structEach() --->
<cfset structEach(myStruct, function(key, value) {
	<cfoutput><li>#key# : #value#</li></cfoutput>
})>
```

_**Script:**_
```coldfusion
<cfscript>

// Define our struct
myStruct = {name: "Tony", state: "Florida"};

// By struct
for (currentKey in myStruct) {
	writeOutput("<li>#currentKey# : #myStruct[currentKey]#</li>");
}

// By structEach()
myStruct.each(function(key, value) {
	writeOutput("<li>#key# : #value#</li>");
});

</cfscript>
```

#### List Loop

_**Tags:**_
```coldfusion
<!--- Define our list --->
<cfset myList = "a, b, c">

<!--- By list --->
<cfloop index="item" list="#myList#">
	<cfoutput>#item#</cfoutput>
</cfloop>

<!--- By array --->
<cfloop index="currentIndex" array="#listToArray(myList, ",")#">
	<cfoutput>#currentIndex#</cfoutput>
</cfloop>

<!--- By listEach() --->
<cfset listEach(myList, function(element, index) {
	<cfoutput>#element# : #index#</cfoutput>
}, ",")>
```

_**Script:**_
```coldfusion
<cfscript>

// Define our list
myList = "a, b, c";

// By array
for (item in listToArray(myList, ",")) {
	writeOutput(item);
}

// By listEach()
myList.each(function(element, index) {
	writeOuput(element & " : " & index);
}, ",");

</cfscript>
```

#### Query Loop

_**Tags:**_
```coldfusion
<!--- Define our query --->
<cfset platform = ["Adobe ColdFusion", "Railo", "Lucee"]>
<cfset myQuery = queryNew("")>
<cfset column = queryAddColumn(myQuery, "platform", "CF_SQL_VARCHAR", platform)>

<!--- By row index --->
<cfloop index="i" from="1" to="#myQuery.recordCount#">
	<cfoutput><li>#myQuery["platform"][i]#</li></cfoutput>
</cfloop>

<!--- By group --->
<cfloop query="myQuery" group="platform">
	<cfoutput><li>#platform#</li></cfoutput>
</cfloop>
```

_**Script:**_
```coldfusion
<cfscript>

// Define our query
platform = ["Adobe ColdFusion", "Railo", "Lucee"];
myQuery = queryNew("");
column = queryAddColumn(myQuery, "platform", "CF_SQL_VARCHAR", platform);

// By row index
for (i = 1; i <= myQuery.recordCount; i++) {
    writeOutput("<li>#myQuery["platform"][i]#</li>");
}

// By query
for (row in myQuery) {
    writeOutput("<li>#row.platform#</li>");
}

</cfscript>
```

## LICENSE
> <a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">CFML Tag to Script Conversions</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://tonyjunkes.com/leave-your-tags-at-the-door-cfml-tag-to-script-conversions" property="cc:attributionName" rel="cc:attributionURL">Tony Junkes</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.
