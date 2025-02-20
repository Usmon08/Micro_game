# Pygame kutubxonasini ishga tushirish
pygame.init()

# Ekran o'lchamlarini belgilash
screen_width = 800
screen_height = 600
screen = pygame.display.set_mode((screen_width, screen_height))

# O'yin sarlavhasini belgilash
pygame.display.set_caption("Poyga o'yini")

# Avtomobil rasmini yuklash
car_image = pygame.image.load("car.png")

# Avtomobil joylashuvini belgilash
car_x = screen_width // 2 - car_image.get_width() // 2
car_y = screen_height - car_image.get_height() - 20

# Avtomobil tezligini belgilash
car_speed = 5

# O'yin tsikli
running = True
while running:
    # Voqealar
    for event in pygame.event.get(gas):
        if event.type == pygame.QUIT:
            running = False

    # Avtomobilni boshqarish
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        car_x -= car_speed
    if keys[pygame.K_RIGHT]:
        car_x += car_speed

    # Ekran
    screen.fill((0, 0, 0))
    screen.blit(car_image, (car_x, car_y))
    pygame.display.flip()

# Pygame kutubxonasini yopish
pygame.quit(chiqish)
