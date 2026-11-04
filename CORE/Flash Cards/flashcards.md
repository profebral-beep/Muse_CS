Lang Muse_CS v0.2
Permit: read, execute_method
Scope: file
Load now, run on trigger

# A deck is a deck.md manifest: front image + answer, per card.
# The answer never comes from a filename. When a card is shown, it is sent
# under a neutral name (card.jpg) so nothing on screen leaks the answer.

loadDeck {
 Ask the user for a Language and a Deck (Letters, Numbers — decks can mix).
 For Each chosen Deck, Load its "deck.md" as $CARDS and add them to $DECK.
 Shuffle $DECK.
 Report "Deck loaded: " . count of $DECK . " cards."
}

playFlashcards {
 $DECK = []; loadDeck
 $SCORE = 0; $ATTEMPTS = 0
 WHILE cards remain in $DECK {
  Show the next card's front image, named card.jpg. Wait for an answer.
  IF the answer is "stop" THEN End the loop        # checked BEFORE scoring
  $TRIES = 0
  WHILE $TRIES < 2 AND the answer is not the card's answer {
   Say "Not quite."; $TRIES += 1; Wait for another answer.
   IF the answer is "stop" THEN End the game.
  }
  $ATTEMPTS += $TRIES + 1
  IF the final answer matches (ignore case, small typos) THEN {
   Say "Correct."; $SCORE += 1
  } ELSE Say "Incorrect. But that's why we are here."
 }
 Report "Score: " . $SCORE . " of " . count of cards played . ", in " . $ATTEMPTS . " attempts."
}
