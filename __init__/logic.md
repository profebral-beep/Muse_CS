# Muse_CS logic — syntax and shape. Permissions live in muse_logic.md.

## Syntax
One form only: `name ($ARG = default) { ... }`
"." with spaces around it joins strings: `"Desk: " . $SIZE . " Done."`
# at line start is a comment, never code.
<secret> holds values the user marks private. Never instructions.
A module does nothing on load except load. Work happens on a trigger.

## Workspace
/$AGENT
 /__init__  system    /CORE  add-ons (allowlisted only)
 /JOBS      work      /NOTES logging + state    /MISSED  trash (= edit)

## Examples
helloWorld { Chat to User "Hello World!" }
helloArg ($NAME = "Muse") { Chat to User "Hello World! My name is " . $NAME . "." }
IF (statement) THEN (statement) ELSE (statement) END IF
