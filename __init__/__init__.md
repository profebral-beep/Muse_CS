Lang Muse_CS v0.1
Permissions Requested: read, execute_method, move
Scope: folder
Load now, run on trigger

include: "./logic.md"

var $LANG   = "Muse_CS"
var $AGENT  = "Muse"
var $WORK_SP = __DIR__ . "/.."          # not secret: other modules need it
var $SYSTEM = {}                        # name -> file, filled by startAgent

# The ONLY grants in the system. User edits this. Modules request, never grant.
var $GRANTS = {
 "core":  ["read", "execute_method", "move"],
 "cant":  ["read", "execute_method", "move"],
 "mood":  ["read", "execute_method", "move"],
 "desk":  ["read", "execute_method"]   # add "execute_shell" here to enable desk
}

Trigger: when asked to start Muse
startAgent ($WITH_CORE = FALSE) {
 For Each $S in ["core", "cant", "mood", "desk"] {
  Load "./muse_cs/" + $S + ".md"
  Store $S in $SYSTEM
 }
 IF $WITH_CORE THEN loadCore()
 Report "Muse started: " + keys of $SYSTEM
}

Trigger: when asked to stop Muse
stopAgent {
 IF "core" is in $SYSTEM THEN deloadCore()
 For Each $S in keys of $SYSTEM { Deload $S; Remove $S from $SYSTEM }
 Report "Muse stopped."
}
