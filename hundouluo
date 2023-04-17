import pygame
import random

# 初始化Pygame
pygame.init()

# 设置游戏窗口尺寸
window_width = 640
window_height = 480
screen = pygame.display.set_mode((window_width, window_height))

# 加载游戏资源
player_image = pygame.image.load("player.png").convert_alpha()
enemy_image = pygame.image.load("enemy.png").convert_alpha()
bullet_image = pygame.image.load("bullet.png").convert_alpha()

# 设置游戏时钟
clock = pygame.time.Clock()

# 定义游戏对象类
class GameObject:
    def __init__(self, x, y, image):
        self.x = x
        self.y = y
        self.image = image

    def draw(self):
        screen.blit(self.image, (self.x, self.y))

# 定义玩家类
class Player(GameObject):
    def __init__(self, x, y, image):
        super().__init__(x, y, image)
        self.speed = 5
        self.bullets = []

    def move_left(self):
        self.x -= self.speed

    def move_right(self):
        self.x += self.speed

    def shoot(self):
        bullet = Bullet(self.x + 16, self.y, bullet_image)
        self.bullets.append(bullet)

    def update(self):
        for bullet in self.bullets:
            bullet.update()

        self.bullets = [bullet for bullet in self.bullets if bullet.y > 0]

    def draw(self):
        super().draw()

        for bullet in self.bullets:
            bullet.draw()

# 定义敌人类
class Enemy(GameObject):
    def __init__(self, x, y, image):
        super().__init__(x, y, image)
        self.speed = 2

    def update(self):
        self.y += self.speed

# 定义子弹类
class Bullet(GameObject):
    def __init__(self, x, y, image):
        super().__init__(x, y, image)
        self.speed = 10

    def update(self):
        self.y -= self.speed

# 创建游戏对象
player = Player(window_width // 2 - 16, window_height - 64, player_image)
enemies = []

# 游戏循环
while True:
    # 处理事件
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            quit()
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                player.move_left()
            elif event.key == pygame.K_RIGHT:
                player.move_right()
            elif event.key == pygame.K_SPACE:
                player.shoot()

    # 更新游戏对象
    player.update()

    for enemy in enemies:
        enemy.update()

    if random.randint(0, 100) < 2:
        enemy = Enemy(random.randint(0, window_width - 32), 0, enemy_image)
        enemies.append(enemy)

    # 绘制游戏画面
    screen.fill((0, 0, 0))

    player.draw()

    for enemy in enemies:
        enemy.draw()

    pygame.display.update()

    # 控制游戏帧率
    clock.tick(60)
