# CS447-Zombies-Game
Pac-Man type game using MARS MIPS simulator (written in MIPS assembly language)
Nicole Dash CS0447 Project 1

The program first checks for the b button to be pressed to begin the game. It then sets the zombies into set positions for the beginning of the game and puts each Zombie's x
and y into registers that are not used for anything else in the code other than that specific zombie's x or y. I also declared bytes that are loaded with the zombie's
previous x positions and y positions throughout the game. Lastly I made a tempx and tempy that are used in the moveZombieRandom method. 
Then the maze is set. I used a loop that went through the maze given and set any leds in the positions where there was an x to yellow and left all the 
others off. I looped though it row by row until the x value hit 63 then reset x to 0 and continued until the y value hit 63 and the maze was complete.
The game then starts by getting the initial time and setting the moves counter to zero. Next the game loop begins and checks for what key is pressed. 
Depending on what key is pressed it branches to the method that adds or subtracts from the players x argument or y argument depending on the indicated direction.
Each key method jump and links to a movement method which moves the player based on the arguments passed in and adds one to the moves counter every time a successful
move is made by the player. The gameloop then continues and the current time is recorded. The current time is subtracted from the initial time to check if 500ms has passed.
If it has been 500ms the program jumps and links to the moveZombies method, otherwise it jumps back to the start of the gameloop. The moveZombie method then determines what 
quadrant the player is in and depending on what quadrant the player is in it calls the methods MoveZombieInQuadrant or MoveZombieRandom. If the player is in the first 
quadrant then then the arguments for zombie 1's x and y position ($t4 and $t5) are passed into MoveZombieInQuadrant and the x and y for zombie 2 ($t6 and $t7) , 
zombie 3 ($t8 and $t9), and zombie 4 ($s6 and $s7) are passed into the MoveZombieRandom method. The MoveZombieInQuadrant method compares the player's position to the zombie's 
position It first checks if the zombie is in the same x or y as the player If the zombie is in the same x as the player it branches to move the zombie in the y position.
If the zombie is in the same y as the player it branches to move the zombie in the x position, If the player's x is less than the zombie's x it moves the zombie left, 
otherwise moves right. For y position if the player's y is less than the zombie's y position the zombie moves up otherwise moves down. Before making each move though the 
zombie checks if it is going to try to move into a wall if so it tries a different direction. If the zombie is going to move onto the player, it branches to a method called 
dead which prints out the captured message and ends the program. The MoveZombieRandom method generates a random number 0-3 that correlate with a direction. There is a method 
for each direction that move the zombie in that direction by adding or subtracting to the y value. Each method though first checks if the zombie is trying to move towards a 
wall, if it is trying to backtrack, or if it is trying to escape its quadrant. If it is any of these situations a new random direction is chosen. If all directions result 
in one of these situations the zombie is allowed to backtrack and jumps to backtrack which sets the zombie back to its previous position and allows it to move in the 
direction it came from. These methods also check if the zombie moves into the coordinate where the player is and will jump to dead if the player is captured by a zombie. 
Once the player reached (63,63) the game ends and the success message is printed with the number of moves that the user made. 

Known issues: The zombie that is following the player doesn't have reverse direction as lowest priority and therefore can sometimes get stuck in a corner as it tries to move
toward the player. The zombie will chase the player again if the player moves back in line with the zombie. This only causes a it to be difficult to see the zombie is 
following the player in certain cases where the zombie is in a corner inside the maze. 
