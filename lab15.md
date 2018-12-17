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
做好之后运行是这样的，输入wasd即可控制蛇的移动了

![](https://github.com/xiaobaishangxian/homework/blob/gh-pages/images/20171228232555736.png?raw=true)

## 创新
介绍一种最近比较火的贪吃蛇AI算法，可以吃满全屏~    
![](https://github.com/xiaobaishangxian/homework/blob/gh-pages/images/20171228094733663.gif?raw=true)    

伪代码如下：
```
if 可以吃食物
        if 虚拟蛇沿规则最短路吃食物后能找到尾巴
                真实蛇移动一步
                重新判断
        else if 虚拟蛇沿不规则最短路去吃食物能找到尾巴
                真实蛇移动一步
                重新判断
else if 可知到达自己的尾巴并且移动一步已让可以到达自己尾巴
        选择离食物最远的位置移动
        重新判断
else
        DFS向最深的路径移动一步
```
知道了伪代码后就可以用各种语言来试试啦~

最后安利一个蛇蛇大作战的游戏哦    
效果如下图：    
![](https://zzm99.github.io/homework/images/t1.gif)