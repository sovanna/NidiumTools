# Nidum Tools

Several tools that were specially crafted for the nidium project

Contents:

 * Konstructor: tool to manage dependencies and build configurations
 * Styleguidor: tool to rate the c/c++ code
 * Documentor:	tool to keep the documentation, examples and code in sync.

## Konstructor

Very, and effective way for the developer to keep the dependencies and the build 
configuration in sync with the gyp settings of the nidium project.
This uses the :
 * `deps.py` : module internally to dependenies
 * `release.py` to create a release
 * `installer/*` to create installation package

## Show me the code

Every project has a `configure` python script, that uses this.

```
PYTHONPATH=~/NativeTools/src/&&./configure --third-party=../../third-party/
```

Basically you pass --third-party the thirdparty path and PYTHONPATH to the path 
where `konstruktor.py` is

## Styleguidor

Simple, but effective way for the developer to check if the code is more or less
compliant with the project's styleguide. This is simply a set of regexes, that 
`rate` and print each line.
Tool is by no way ideal, but better then nothing.

### Show me the code

You could write a styleguide rule like this:

```
    'if-(':         {'pattern': '\bif\(', 
                     #Essential keyword
                     'text': 'Whitespace needed between if and parenthesis', 
                     'weight': 0.25},
```

And by pointing `src/styleguidor.py` to the file's directory it could create:

```
...
src/NativeASCII.h:6	Whitespace must follow a comma
...
The code got a score of 4.5.
```
 
## Dokumentor

Simple, but effective way to for the developer to keep the documentation and 
the code in sync without to much hassle.

While programming C/C++ to expose Javascript, you write *currently python code*
(later probably jsdoc) inside '/*$ comments $*/'. These comments will be extracted 
and transformed with `documentor.py` into `markdown`

Note: *This tool is will undergo drastic changes in the _near_ future*.

### Show me the code

In the c/c++ code you can write comments like:

```
/*$
FunctionDoc( "HTTPRequest.write", "Respond to a client that made a request to the webserver",
	[ SeeDoc( "HTTPListener" ), SeeDoc( "HTTPRequest.write"), SeeDoc( "HTTPRequest.end" ), SeeDoc( "HTTPRequest.writeHead" ) ],
	NO_Examples,
	IS_Dynamic, IS_Public, IS_Fast,
	[ ParamDoc( "data", "The data to send out", "string|ArrayBuffer", IS_Obligated ) ],
	NO_Returns
);
$*/
```

And by pointing `src/dokumentor.py` to the file's direcory it could create:

```
_HTTPRequest.write__

Respond to a client that made a request to the webserver.

__Public__: true

__Static__: false

__Sees__:

__HTTPListener__
__HTTPRequest.end__
__HTTPRequest.writeHead__

__Parameters__:

data	'string', 'ArrayBuffer'	false	The data to send out.

```