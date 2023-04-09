from pygame import *

back = (200, 255, 255)
win_width = 600
win_height = 500
window = display.set_mode((win_width, win_height))
window.fill(back)

clock = time.Clock()
FPS = 60
game = True

class GameSprite(sprite.Sprite):
    def __init__(self, player_image, player_x, player_y, size_x, size_y, player_speed):
        super().__init__()
        self.image = transform.scale(image.load(player_image),(size_x, size_y))
        self.speed = player_speed
        self.rect = self.image.get_rect()
        self.rect.x = player_x
        self.rect.y = player_y
    def reset (self):
        window.blit(self.image, (self.rect.x, self.rect.y))

class Player(GameSprite):
    def update_left(self):
        keys_pressed = key.get_pressed()

        if keys_pressed[K_UP] and self.rect.x > 5:
            self.rect.x -= self.speed
        if keys_pressed[K_DOWN] and self.rect.x < win_width -80:
            self.rect.x += self.speed

    def update_right(self):

        if keys_pressed[K_W] and self.rect.x > 5:
            self.rect.x -= self.speed
        if keys_pressed[K_S] and self.rect.x < win_width -80:
            self.rect.x += self.speed  

platform_left=Player('i.webp', win_height 5, 80, 105, 5)
platform_right=Player('i.webp', 5, 0, 80, 105, 5)


while game :
    for e in event.get():
        if e.type ==QUIT:
            game = False

            platform_left.update()
            platform_right.update()
            

    display.update()
    clock.time(FPS)
    
    
