# EE 322
**Engineering Design VI**

*Nathan Taco Bravo*
---
**Fun Facts About Me:**
1. I'm Ecuadorian
2. Favorite sport is soccer
3. I can move my ears at will
---
**Hobbies:**
- Playing soccer and videogames
- Playing/practicing the drums
- Going to the gym
---
**Code (2 Player Pong Game):**

```
#include <iostream>
#include <time.h>
#include <conio.h>
#include <Windows.h>
using namespace std;
enum eDir { STOP = 0, LEFT = 1, UPLEFT = 2, DOWNLEFT = 3, RIGHT = 4, UPRIGHT = 5,
DOWNRIGHT = 6 };
class Ball
{
private:
int x, y;
int startX, startY;
eDir direction;
public:
Ball(int posX, int posY)
{
startX = posX;
startY = posY;
x = posX; y = posY;
direction = STOP;
}
void Reset()
{
x = startX; y = startY;
direction = STOP;
}
void changeDirection(eDir d)
{
direction = d;
}
void randomDirection()
{
direction = (eDir)((rand() % 6) + 1);
}
inline int getX() { return x; }
inline int getY() { return y; }
inline eDir getDirection() { return direction; }
void Move()
{
switch (direction)
{
case STOP:
break;
case LEFT:
x--;
break;
case RIGHT:
x++;
break;
case UPLEFT:
x--; y--;
break;
case DOWNLEFT:
x--; y++;
break;
case UPRIGHT:
x++; y--;
break;
case DOWNRIGHT:
x++; y++;
break;
default:
break;
}
}
friend ostream & operator<<(ostream & o, Ball c)
{
o << "Ball [" << c.x << "," << c.y << "][" << c.direction << "]";
return o;
}
};
class Paddle
{
private:
int x, y;
int startX, startY;
public:
Paddle()
{
x = y = 0;
}
Paddle(int posX, int posY) : Paddle()
{
startX = posX;
startY = posY;
x = posX;
y = posY;
}
inline void Reset() { x = startX; y = startY; }
inline int getX() { return x; }
inline int getY() { return y; }
inline void moveUp() { y--; }
inline void moveDown() { y++; }
friend ostream & operator<<(ostream & o, Paddle c)
{
o << "Paddle [" << c.x << "," << c.y << "]";
return o;
}
};
class gameManger
{
private:
int width, height;
int score1, score2;
char up1, down1, up2, down2;
bool quit;
Ball* ball;
Paddle* player1;
Paddle* player2;
public:
gameManger(int w, int h)
{
srand(time(NULL));
quit = false;
up1 = 'w'; up2 = 'i';
down1 = 's'; down2 = 'k';
score1 = score2 = 0;
width = w; height = h;
ball = new Ball(w / 2, h / 2);
player1 = new Paddle(1, h / 2 - 3);
player2 = new Paddle(w - 2, h / 2 - 3);
}
~gameManger()
{
delete ball, player1, player2;
}
void scoreUp(Paddle* player)
{
if (player == player1)
score1++;
else if (player == player2)
score2++;
ball->Reset();
player1->Reset();
player2->Reset();
}
void Draw()
{
system("cls");
for (int i = 0; i < width + 2; i++)
cout << "\xB2";
cout << endl;
for (int i = 0; i < height; i++)
{
for (int j = 0; j < width; j++)
{
int ballx = ball->getX();
int bally = ball->getY();
int player1x = player1->getX();
int player2x = player2->getX();
int player1y = player1->getY();
int player2y = player2->getY();
if (j == 0)
cout << "\xB2";
if (ballx == j && bally == i)//ball
cout << "O";
else if (player1x == j && player1y == i)//player1
cout << "\xDB";
else if (player1x == j && player1y + 1 == i)
cout << "\xDB";
else if (player1x == j && player1y + 2 == i)
cout << "\xDB";
else if (player1x == j && player1y + 3 == i)
cout << "\xDB";
else if (player2x == j && player2y == i)//player2
cout << "\xDB";
else if (player2x == j && player2y + 1 == i)
cout << "\xDB";
else if (player2x == j && player2y + 2 == i)
cout << "\xDB";
else if (player2x == j && player2y + 3 == i)
cout << "\xDB";
else
cout << " ";
if (j == width - 1)
cout << "\xB2";
}
cout << endl;
}
for (int i = 0; i < width + 2; i++)
cout << "\xB2";
cout << endl;
cout << "Pong Game (2 Players)" << endl;
cout << "Player 1 controls: UP = W and DOWN = S" << endl;
cout << "Player 2 controls: UP = I and DOWN = K" << endl;
cout << "Score Player 1: " << score1 << endl;
cout << "Score Player 2: " << score2 << endl;
}
void Input()
{
ball->Move();
int ballx = ball->getX();
int bally = ball->getY();
int player1x = player1->getX();
int player2x = player2->getX();
int player1y = player1->getY();
int player2y = player2->getY();
if (_kbhit())
{
char current = _getch();
if (current == up1)
if (player1y > 0)
player1->moveUp();
if (current == up2)
if (player2y > 0)
player2->moveUp();
if (current == down1)
if (player1y + 4 < height)
player1->moveDown();
if (current == down2)
if (player2y + 4 < height)
player2->moveDown();
if (ball->getDirection() == STOP)
ball->randomDirection();
if (current == 'q')
quit = true;
}
}
void Logic()
{
int ballx = ball->getX();
int bally = ball->getY();
int player1x = player1->getX();
int player2x = player2->getX();
int player1y = player1->getY();
int player2y = player2->getY();
for (int i = 0; i < 4; i++)//left paddle
if (ballx == player1x + 1)
if (bally == player1y + i)
ball->changeDirection((eDir)((rand() % 3) + 4));
for (int i = 0; i < 4; i++)//right paddle
if (ballx == player2x - 1)
if (bally == player2y + i)
ball->changeDirection((eDir)((rand() % 3) + 1));
if (bally == height - 1)//bottom wall
ball->changeDirection(ball->getDirection() == DOWNRIGHT ? UPRIGHT
: UPLEFT);
if (bally == 0)//top wall
ball->changeDirection(ball->getDirection() == UPRIGHT ? DOWNRIGHT
: DOWNLEFT);
if (ballx == width - 1)//right wall
scoreUp(player1);
if (ballx == 0)//left wall
scoreUp(player2);
}
void Run()
{
while (!quit)
{
Draw();
Input();
Logic();
Sleep(20);
}
}
};
int main()
{
gameManger c(60, 20);//dimensions of the rectangle of the Pong Game
c.Run();
return 0;
}
```
---
[Funny Cat](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTVSCQ1sd9Q8MQicoOdnbUY8UT9ps2t1LgUxgTMyC-0gZRm8zE1qaGcAYrCSDP3y-kFoic&usqp=CAU)
---
![Engineering Design](https://github.com/NathanTacoBravo/EE-322-S-2024/assets/116911160/e247f265-c5a6-4f16-8603-4b6452970a7d)
---
