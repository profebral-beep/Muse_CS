# Muse_CS logic — the whole spec fits on this page

## Permissions
Actions: read, execute_method, execute_shell, create, edit, move, network.

1. A module's header *requests*. Only $GRANTS in __init__.md *grants*.
2. execute_shell and network are denied unless named in $GRANTS.
3. File header beats folder header. Denied beats Allowed at the same level.
   Nothing named is denied.
4. Moving a file into MISSED, or out of the workspace, counts as edit.
   Moving inside the workspace counts as move.

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
