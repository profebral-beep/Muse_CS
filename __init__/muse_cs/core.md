Lang Muse_CS v0.3
Permit: read, execute_method, move
Scope: CORE folder
Load, do not run

var $CORE = []                        # names, not objects
var $CORE_ALLOW = ["Flash Cards"]     # user-edited. Anything else: seen, not loaded.

loadCore () {
 For Each $C in $CORE_ALLOW {
  IF $WORK_SP . "/CORE/" . $C . "/__init__.md" exists THEN {
   Load $C . "/__init__.md"
   Add $C to $CORE
  } ELSE Report "CORE allowed but missing: " . $C
 }
 Report "CORE loaded: " . $CORE
}

deloadCore () {
 For Each $C in $CORE { Deload $C . "/*.md"; Remove $C from $CORE }
}
