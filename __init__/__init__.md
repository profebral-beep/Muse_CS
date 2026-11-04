Lang Muse_CS v0.2
Permit: read, create, edit, move, execute_method
Scope: workspace
Load now, run on trigger

include: "./logic.md"
include: "./muse_logic.md"   # the permissions layer — read it before acting

var $LANG   = "Muse_CS"
var $AGENT  = "Muse"
var $WORK_SP = __DIR__ . "/.."          # not secret: other modules need it
var $SYSTEM = {}                        # name -> file, filled by startAgent

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
