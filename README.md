import pygame
import sys

# Inicializa o Pygame
pygame.init()

# Configurações da tela
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Raimundo: O Cachorro Supremo")

# Cores
WHITE = (255, 255, 255)
GREEN = (0, 255, 0)
RED = (255, 0, 0)

# Configurações do cachorro
dog_size = 50
dog_color = GREEN
dog_x = SCREEN_WIDTH // 2
dog_y = SCREEN_HEIGHT // 2
dog_speed = 5

# Função para desenhar o cachorro
def draw_dog(x, y):
    pygame.draw.rect(screen, dog_color, [x, y, dog_size, dog_size])

# Função principal do jogo
def game_loop():
    global dog_x, dog_y

    clock = pygame.time.Clock()

    while True:
        # Processa os eventos
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                sys.exit()

        # Movimento do cachorro
        keys = pygame.key.get_pressed()
        if keys[pygame.K_LEFT]:
            dog_x -= dog_speed
        if keys[pygame.K_RIGHT]:
            dog_x += dog_speed
        if keys[pygame.K_UP]:
            dog_y -= dog_speed
        if keys[pygame.K_DOWN]:
            dog_y += dog_speed

        # Mantém o cachorro dentro da tela
        if dog_x < 0:
            dog_x = 0
        if dog_x > SCREEN_WIDTH - dog_size:
            dog_x = SCREEN_WIDTH - dog_size
        if dog_y < 0:
            dog_y = 0
        if dog_y > SCREEN_HEIGHT - dog_size:
            dog_y = SCREEN_HEIGHT - dog_size

        # Atualiza a tela
        screen.fill(WHITE)
        draw_dog(dog_x, dog_y)
        pygame.display.flip()

        # Controla o frame rate
        clock.tick(30)

# Executa o jogo
game_loop()
