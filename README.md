import pygame
import random

# Inicializar Pygame
pygame.init()

# Colores
BLACK = (0, 0, 0)
GREEN = (0, 255, 0)

# Tamaño de la pantalla
SCREEN_WIDTH = 640
SCREEN_HEIGHT = 480

# Crear pantalla
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))

# Crear titulo de la ventana
pygame.display.set_caption("Juego de Ranas")

# Crear una fuente
font = pygame.font.Font(None, 36)

# Variables del juego
clock = pygame.time.Clock()
saltos = 0
game_over = False

# Función para actualizar el texto
def draw_text(surf, text, size, x, y):
    font_name = pygame.font.match_font('arial')
    font = pygame.font.Font(font_name, size)
    text_surface = font.render(text, True, (255, 255, 255))
    rect = text_surface.get_rect()
    rect.midtop = (x, y)
    surf.blit(text_surface, rect)

# Bucle principal del juego
while not game_over:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            game_over = True

        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE:
                saltos += 1
                y = random.randint(50, 350)
                velocidad = random.randint(5, 15)

    screen.fill(BLACK)

    if saltos > 0:
        pygame.draw.rect(screen, GREEN, (100, y, 100, 100))
        pygame.draw.circle(screen, GREEN, (150, y + 50), 40)
        pygame.draw.polygon(screen, GREEN, [(120, y + 100), (150, y + 70), (180, y + 100)], 0)

    draw_text(screen, "Puntos: " + str(saltos), 24, 50, 50)

    if saltos >= 10:
        draw_text(screen, "¡Ganaste!", 48, 250, 100)

    pygame.display.flip()
    clock.tick(30)

pygame.quit()
