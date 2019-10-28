# SnowDay_JSChallenge

"Write a program that checks if a Sudoku board is completed correctly. The input of the board will be provided in an array matrix, your output should be a Boolean."

https://sudoku.com/how-to-play/sudoku-rules-for-complete-beginners/

`const input = [`
  `[ , , ],[ , , ],[ , , ],`
  `[ , , ],[ , , ],[ , , ],`
  `[ , , ],[ , , ],[ , , ],`
  `[ , , ],[ , , ],[ , , ],`
  `[ , , ],[ , , ],[ , , ],`
  `[ , , ],[ , , ],[ , , ],`
  `[ , , ],[ , , ],[ , , ],`
  `[ , , ],[ , , ],[ , , ],`
  `[ , , ],[ , , ],[ , , ],`
`]`

I have barely played Sudoku, so this is a tough challenge!

The first pattern I see is that the board is an array, containing three arrays across, each with three numbers inside. The board is nine rows tall. 

From the rule site, each of the nine clusters of arrays (the squares) needs to have the numbers 1-9 inside. 


There also can't be duplicates in the entire column or entire row (of 9 spaces)

The first step is to look at one square's numbers and determine which are missing.

If and only if you can determine that any empty spaces can be filled with a square's missing number, without creating verical or horizontal dupes, the number can go in.

I think there's opportunity for recursion here, with the following steps taken:
  * Iterate through squares one by one
  * If one has empty spaces... (any of the three lengths is <3?)
  * Determine the missing numbers in the square (Have to iterate over three arrays. Maybe push all existing nums into one together and check length < 9.)
  * Iterate through the nine spaces in each square. If empty... (These are three arrays, so you could map over each so the length remains intact)
  * Check vertically first: Can you put any of the numbers in without creating a duplicate? All passing/in play numbers are returned. (Given one square, and one of the remaining numbers, iterate over the other clusters of three arrays, look at the matching index position's column, and run .includes() to get Boolean returned)
  * Are any of the passing numbers duplicates of a vertical neighboring square's spaces? Return those that still pass. (Does this actually help? I think this is a strategy for starting with a missing number, not an empty square.*)
  * Check horizontally with those numbers. Return all that still do not create duplicates. (Given the same square, and same missing number, check the entire row, and run .includes() to get Bool returned)
  * Check the number against the horizontal neighboring square's spaces. Return all that still pass. (*See above)
  * If only one fits in a space without creating a duplicate, that is a certain number for that spot.
  * If more than one passes all checks, you can't place a number in, and have to move to the next square.
  * Move on to next space, and eventually the next square
* Base case is that all spaces are filled. Return the completed input.
