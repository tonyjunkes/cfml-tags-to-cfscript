# CFML Tag to Script Conversions
#####A collection of examples demonstrating the conversion of CFML code blocks written in tags to CFScript.

**Currently a work in progress!**

> This is not a CFScript syntax documentation you're (possibly) looking for. That awesome piece of work, by Adam Cameron, can be found [here](https://github.com/adamcameron/cfscript) and is highly recommended as a reference to the content you'll find here.

The examples in this document are an attempt to demonstrate conversions of CFML tag-based code to script-based code as a way of learning / migrating to CFScript. It is assumed that you already have a relatively firm understanding of the ColdFusion Markup Language (at least on a tag-based level). For the sake of modernity, the converted examples will be written to comply (from an agnostic approach) with the most current versions of the various CFML engines at the time of writing - (ColdFusion 11, Railo 4.2 & Lucee 4.5).

### Variables

_**Tags:**_
```coldfusion
<!--- Some simple variable statements in tags --->

<!--- Default variable declarations --->

<cfparam name="pageTitle" default="Tags">
<cfparam name="pageNumber" type="numeric" default=1>

<!--- Regular assignment --->

<cfset page = "#pageTitle# - #pageNumber#">

<cfoutput>#pageTitle# - #pageNumber# : #page#</cfoutput>

<!--- Arrays --->

<cfset jvmLangs = arrayNew(1)>
<cfset jvmLangs[1] = "CFML">
<cfset jvmLangs[2] = "Groovy">
<cfset arrayApend(jvmLangs, "Clojure")>
<cfoutput>#arrayLen(jvmLangs)#</cfoutput>

<cfdump var="#jvmLangs#">

<!--- Structures --->

<cfset states = structNew()>
<cfset states.florida = "FL">
<cfset states["california"] = "CA">
<cfset structInsert(states, "New York", "NY")>

<cfdump var="#states#">
```

_**Script:**_
```coldfusion
<cfscript>

// Some simple variable statements in script
// CFScript code included in a ".cfm" must be wrapped in <cfscript> tags

// Default variable declarations

param name="pageTitle" default="Tags";
param name="pageNumber" type="numeric" default=1;

// Regular assignment

page = "#pageTitle# - #pageNumber#";
// or
// page = pageTitle & " - " & pageNumber;

writeOutput("#pageTitle# - #pageNumber# : #page#");
// or
// writeOutput(pageTitle & " - " & pageNumber & " : " & page);

// Arrays

// Instead of jvmLangs = arrayNew(1);
// We can use a implicit array
jvmLangs = [];
jvmLangs[1] = "CFML">
jvmLangs[2] = "Groovy">
// Many modern CFML functions are now also member functions
// So arrayAppend(jvmLangs, "Clojure"); is now
jvmLangs.append("Clojure");

writeDump(jvmLangs);

// Structures

// Instead of states = structNew();
// We can use a implicit struct
states = {};
states.florida = "FL";
states["california"] = "CA";
// structInsert(states, "New York", "NY");
states.insert("New York", "NY");

writeDump(states);

</cfscript>
```

### Operators

_**Tags:**_
```coldfusion
<!--- Decision --->

<cfset x = 1>
<cfset x = x EQ 1>
<cfset x = x NEQ 1>
<cfset x = x LT 1>
<cfset x = x GT 1>
<cfset x = x LTE 1>
<cfset x = x GTE 1>

<!--- Increment / decrement --->

<cfset x = x + 1>
<cfset x = x - 1>

<!--- Inline assignment --->

<cfset x = x + 3>
<cfset x = x - 3>
<cfset x = x / 3>
<cfset x = x * 3>
<cfset x = x MOD 1>


<!--- Boolean --->

<cfset x = 1>
<cfset y = 2>

<cfset NOT x>
<cfset x EQ 1 AND y EQ 2>
<cfif x EQ 1 OR y EQ 2>

<!--- Ternary --->

<cfset x = (1 + 1 EQ 3) ? false : true>
```

_**Script:**_
```coldfusion
<cfscript>

// Decision
x = 1;
x = x == 1;
x = x != 1;
x = x < 1;
x = x > 1;
x = x <= 1;
x = x >= 1;

// Increment / decrement
x = x++;
x = x--;

// Inline assignment
x += 3;
x -= 3;
x /= 3;
x *= 3;
x % 3;

// Boolean
x = 1;
y = 2;

!x;
x == 1 && y == 2;
x == 1 || y == 1;

// Ternary
x = (1 + 1 == 3) ? false : true;

</cfscript>
```

## LICENSE
> <a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">CFML Tag to Script Conversions</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://tonyjunkes.com/leave-your-tags-at-the-door-cfml-tag-to-script-conversions" property="cc:attributionName" rel="cc:attributionURL">Tony Junkes</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.<br />Based on a work at <a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/cfchef/cfml-tag-to-script-conversions" rel="dct:source">https://github.com/cfchef/cfml-tag-to-script-conversions</a>.
