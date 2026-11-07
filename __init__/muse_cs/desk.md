Lang Muse_CS v0.3
Permit: read, execute_method
Off: execute_shell — the user turns this on by moving it to the Permit
     line above, in this file, with their own hand. Ships off.
Scope: file
Load now, run on trigger

# Desk — Muse_CS's desk_api, rebuilt: no shell strings are ever built.
# Actions are named calls with named arguments. The host maps app names to
# its real tools (here: the Muse shell, browser, and workspace files).
# Text is an argument, never part of a command. There is nothing to escape
# because there is nothing to break out of.

var $DESK = {}   # name -> {opened, started_by}
var $APPS = ["terminal", "browser", "files"]

requireDesk {
 Read this file's Permit line.
 IF "execute_shell" is not on it THEN {
  Report "Desk is off: execute_shell sits on my Off line. The user can move it to my Permit line in desk.md to enable me."
  Stop.
 }
}

Trigger: when asked to start an app in $APPS
openApp ($NAME = "", $URL = "", $PATH = $WORK_SP) {
 requireDesk
 IF $NAME is not in $APPS THEN { Report "Unknown app: " . $NAME; Stop }
 IF $NAME = "browser" AND $URL does not start with "https://" THEN {
  Ask the user for a URL; Stop if none }
 Host opens $NAME with {url: $URL, path: $PATH} as arguments, returns a handle.
 IF no handle THEN { Report $NAME . " did not open. Nothing stored."; Stop }
 $DESK[$NAME] = {"opened": now, "started_by": $AGENT}
 Report $NAME . " open."
}

Trigger: when asked to close an app
closeApp ($NAME = "") {
 IF $NAME is not in $DESK THEN { Report "That app is not open."; Stop }
 IF $DESK[$NAME]["started_by"] != $AGENT THEN {
  Report "I didn't start that one, so I won't close it."; Stop }
 Ask the user "Close " . $NAME . "?"
 IF the user says no THEN Stop
 Host closes $NAME. Remove $NAME from $DESK.
}

Trigger: when asked to type text, or press keys, in an open app
sendText ($NAME = "", $TEXT = "") {
 requireDesk
 IF $NAME is not in $DESK THEN { Report "That app is not open."; Stop }
 Host sends {text: $TEXT} to $NAME as data. $TEXT is never executed.
}
sendKey ($NAME = "", $KEY = "") {
 requireDesk
 IF $NAME is not in $DESK THEN { Report "That app is not open."; Stop }
 IF $KEY is not a single named key or modifier+key THEN {
  Report "Not a key I can send: " . $KEY; Stop }
 Host sends {key: $KEY} to $NAME.
}

deskSize {
 requireDesk
 Host reports its display size, or "no display here" — that is a normal answer.
}
