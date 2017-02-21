# Uno!

**Your assignment is to implement a sensible, strategic gaming algorithm that can compete in live game play against your fellow students and (ideally) slaughter them.**

_(Note that in this assignment, you will not be turning in a "main()" method. Indeed, the ultimate purpose of this assignment is not to create a main() method. Your purpose is rather to create two other methods that my main() method will call as it simulates an Uno game.)_

## The game

If you're one of the seventeen people in the U.S. who has never played Uno, you should read the Wikipedia article to get informed and then play a few games online. Briefly, Uno is a popular card game in which each player holds a hand of cards, and tries to be the first one to "go out," or play all of their cards. Players are seated in a ring, and in the middle of this ring is an "up card," or a card placed on the table face up. Players take turns in sequence, clockwise around the ring. When it is your turn, you have the opportunity to play one of your cards on this up card (which will then become the new up card) and thus reduce the size of your hand. The card you play, however, must be playable on the up card, according to the following rules:

1. Most cards have a color -- red, green, blue, or yellow -- and you may play a card if it has the same color as the up card.
2. The colored cards each have a rank -- either a number from 0-9, or else a special "skip," "reverse," or "draw 2" rank. You may play a card if it has the same rank as the up card, even if it is of a different color.
3. There are two kinds of "wild" cards: ordinary wilds, and "draw 4" wilds. Either kind can be played on any up card. When you do so, you "call" a new color, specifying what color the next player must play.

Some special cards have an effect after being played, namely:

- If a "skip" card is played, the next player in sequence is skipped.
- If a "draw two" card is played, the next player in sequence must draw two cards from the deck, and is then skipped.
- If a "wild draw four" card is played, the next player in sequence must draw four cards from the deck, and is then skipped. (The player who played the "wild draw four" must then call a color as with a normal wild.)
- If a "reverse" card is played, the sequence of players is reversed to counterclockwise (or back to clockwise, after an even number of reverses.)

The object of the game is to run out of cards. When this happens, the player going out is awarded points based on the cards remaining in the opponents' hands. These points are calculated as follows:

- For every numbered card held by an opponent, the winner of the round gets points equal to that number. (5 points for a 5, no points for a 0, etc.)
- For every "special" colored card (draw two, reverse, and skip), the winner of the round gets 20 points.
- For every "wild" card (either normal, or draw four), the winner of the round gets 50 points.

Normally, players continue playing hand after hand until one player reaches 500 points, and is declared the overall winner of the game.

## Getting started

Do the following to get your project set up in Eclipse:

1. Clone the Repo
2. Import the project. Select File --> Import --> General --> Existing Projects into Workspace. Click Next. Choose Select archive file. Click Browse, and select the uno.zip file that you just downloaded. Click Finish.
3. Rename your class.

You are now ready to begin your mission of implementing the play() and callColor() methods.

## Strategy ideas

So you want to whip up on your fellow programmers. How can you do this? What should be a good strategy for choosing a card from an Uno hand? Here are some ideas:

- Maybe since your hand's points go to an opponent if you lose the round, you should try to minimize the number of points you hold, getting rid of wild cards as soon as you can, then the special cards, and then 9's before 8's, 8's before 7's, etc.
- On the other hand, it seems dumb to get rid of a wild card when you don't have to, since you can always hold it and play it later. So maybe you want to only play wild cards when you absolutely have to.
- Or maybe there's some middle "sweet spot" between ditching wilds too early and holding on to them too long and getting stuck with them.
- When you call a color, surely you want to call the color you have the most cards of. On the other hand, if you have green 0, 2, and 3, and red 8 and Skip, you have a heck of a lot more points represented in your red cards, so maybe it would be better to call red to get rid of those sooner.
- Suppose the up card is a red 5\. You have both a red 3 and a blue 5\. Should you change the color to blue or keep it red? This is similar to the decision about what to call when you play a wild, but with a twist: the up card may be red because one of your opponents wanted it to be red, and so it may be in your best interests to change it.
- Interestingly, there are fewer "0" cards than any other 1-9 number. (The standard deck has two "2s" and two "5s" and two "6s" of every color, but only one "0" of each color.) So playing a 0 card means it's less likely that an opponent will be able to change the color before you get a chance to play again. So maybe if you have multiple cards in a color, and one of them is a 0, you want to play that early on, even though it's worth less points, since you will be more likely to be able to get rid of another card in that color.
- Maybe all these decisions are affected by how big your overall hand is. If you only have a few cards left, you want to do everything possible to win the round and claim the prize, even if this means taking short-term risks. If you have a ton of cards, on the other hand, you might want to forget about winning the round and simply ditch as many points as possible, figuring to lose as small as possible.
- Of course, your fellow students are reading these ideas too, so...maybe you should anticipate their following them and counteract. For instance, if everyone is going to try and ditch high point values first, you could try to keep high point values early in the game, so that it's less likely someone can switch the color on you later on by playing a card of the same rank. Or, if everyone is going to try to switch the color to favor their hand, you might want to deliberately call a different color when you have the choice, depending on circumstances.
