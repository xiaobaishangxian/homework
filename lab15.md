# 字符版本贪吃蛇游戏设计及算法、或创新玩法
## 1,解决思想：自顶向下，逐步求精
## 2,地图
```
char BLANK_CHAR = ’ ‘; 
char WALL_CHAR = ‘*’; 
char map[12][13] = { 
“**”, 
“* *”, 
“* *”, 
“* *”, 
“* *”, 
“* *”, 
“* *”, 
“* *”, 
“* *”, 
“* *”, 
“* *”, 
“**”, 
}; 
```
## 3,食物的随机生成及被吃 
```
void spawnFood() { 
// Random food position 
foodX = rand() % 10 + 1; 
foodY = rand() % 10 + 1; 
while (map[foodX][foodY] != BLANK_CHAR) { 
foodX = rand() % 10 + 1; 
foodY = rand() % 10 + 1; 
} 
map[foodX][foodY] = FOOD_CHAR; 
} 
检查食物是否被吃 
if (snakeHeadX == foodX && snakeHeadY == foodY) { 
willBeLonger = 1; 
spawnFood(); 
} 
蛇身加长 
if (willBeLonger) { 
willBeLonger = 0; 
moved = 1; 
// make space 
for (int i = snakeBodyLen - 1; i > snakeTailIndex; –i) { 
snakeBodyX[i + 1] = snakeBodyX[i]; 
snakeBodyY[i + 1] = snakeBodyY[i]; 
} 
snakeBodyX[snakeTailIndex + 1] = prevSnakeHeadX; 
snakeBodyY[snakeTailIndex + 1] = prevSnakeHeadY; 
if (snakeTailIndex < 0) snakeTailIndex = 0; 
map[prevSnakeHeadX][prevSnakeHeadY] = SNAKE_BODY_CHAR; 
snakeBodyLen++; 
} 
```
## 4,蛇的移动
```
void snakeMove(char control) { 
map[snakeHeadX][snakeHeadY] = BLANK_CHAR; 
// record the previous snake head position 
int prevSnakeHeadX = snakeHeadX; 
int prevSnakeHeadY = snakeHeadY; 
switch (control) { 
case ‘w’: 
snakeHeadX–; 
break; 
case ‘a’: 
snakeHeadY–; 
break; 
case ‘s’: 
snakeHeadX++; 
break; 
case ‘d’: 
snakeHeadY++; 
break; 
default: 
return; 
} 
```
## 5,蛇的死亡
```
void gameOver() { 
printf(“GAME OVER!!\n”); 
gameRunning = 0; 
} 
判定蛇是否死亡 
if (map[snakeHeadX][snakeHeadY] != BLANK_CHAR && map[snakeHeadX][snakeHeadY] != FOOD_CHAR) { 
// DIED 
gameOver(); 
} 
```
![]()