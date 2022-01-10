# CHANGELOG

* v1.1.0 [2021-01-20]:  
  Bug fix 1: A missing parenthesis in players.py  
  Bug fix 2: In switch.py, two missing parentheses; run_game() is a function and not an object.  
  Bug fix 3: "TypeError: ‘dict’ object is not callable". In switch.py, we call dictionaries with squared brackets, not
  parentheses.  
  Bug fix 4: "AttributeError : type object 'Player' has no attribute 'hand'
              AttributeError : type object 'SimpleAI' has no attribute 'hand' ". Added missing attribute.  
  Bug fix 5: In cards.py, the deck had two "2" cards for each suit, which isn't correct. In reality, decks of card have
  each number appear only once for every suit, unlike in the case of this bug.  
  Bug fix 6: Added a missing inside a "for" loop used for counting.  
  Bug fix 7: Assigning a simple or smart AI for each computer strategy wasn't random. It is now.  
  Bug fix 8: Self.draw4 was set to True where it was supposed to be False. Revealed by pytest : 
  
      ___________________________________________________________________________________________________ test_setup_round__resets_flags ____________________________________________________________________________________________________
      def test_setup_round__resets_flags():
      """setup_round sets all flags to initial value"""
      game = switch.Switch()
      game.players = [MockPlayer([]), MockPlayer([])]
      game.setup_round()
      assert game.skip is False
      assert game.draw2 is False
      >       assert game.draw4 is False
      E       assert True is False
      E        +  where True = <switch.Switch object at 0x00000200674DFA90>.draw4
      test_switch.py:54: AssertionError
  Bug fix 9 :Replaced bug fix 4 with a better and more efficient one. Self.players was a list of all players and their 
  attributes, but it did not instantiate their classes when adding them to the list, causing them to not 
  have their object attributes loaded at that time. Hence, the attributes 'hand' and 'name' missing when trying to play the game.
  "AttributeError : type object 'Player' has no attribute 'hand'
  AttributeError : type object 'Player' has no attribute 'name'
  AttributeError : type object 'SimpleAI' has no attribute 'hand'"  
  Bug fix 10 : In a Switch game, a Queen or an Ace can always be discarded. The function can_discard(card) returns
  True or False depending on the card (i.e., if the card is a Queen, an Ace, or/and is the same value/suit of the top.card).
  Knowing the rules of the games we can assert that the function must return True if the card is a Queen or an Ace. 
  However, we've seen that it is not the case as the function was returning mistakenly False when the card is a Queen or
  an Ace and was supposed to return True. Error fixed by replacing a 'False' by a 'True' in switch.py.  
  Bug fix 11 : In user_interface, in select_player, the "for" loop iterates in enumerate(players). 
  Enumerate adds a counter, idx to the variable in the following format : (idx, var). However, the for loop was 
  erroneously set to iterate the index in the value and the value with the index, which isn't right. I fixed it by 
  putting idx before the value in the "for" loop.   
  Bug fix 12 : test_can_discard__allows_queen was set to test kings not queens. I replaced all the K for the suits 
  tested by Q so that it tests for Queens to be discarded.   
  Bug fix 13 : When discarding a Q (Queen) valued card, the next player would not draw 4 cards when he is supposed to, 
  according to the rules. Fixed it by adding an if statement when the card gets discarded to be check if 
  it is a Queen thus setting self.draw4 to True, causing the next player to draw 4 cards.   
  Bug fix 14: The list of cards the player could choose from to discard was displaying the same card in a 
  loop. Fixed by added a variable i who serves as a counter for the displayed cards, thus preventing them from being 
  the same card displayed in a loop.   
  Bug fix 15: The game was displaying the wrong winner. It was displaying another player than the winner. Corrected 
  by putting in the correct index for the print_winner_of_function().   
  Bug fix 16: The game would let only play the same first player in a loop, not letting the others play their turn. 
  Fixed by changing the way the games moves to the next player and thus in a loop. Changed an "elif" to an "else" and 
  simplifying how the code reads hence looking more "pythonic".     
  Bug fix 17: The game is supposed to be played by two, or three, or four players. This bug allowed for a player to play
  alone which is not the correct way to play the game. Fixed by changed the minimal number ai players to 1 instead of 0,
  when the player is alone, thus preventing the player from playing alone.    

* v1.1.0 [2019-11-08]: Added a SmartAI computer opponent.
  Added strategy players.SmartAI.
  None of the bugs have been fixed.
    
* v1.1.0 [2019-10-25]: First major release.
  This version is known to contain some bugs.
