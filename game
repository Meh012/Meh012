import <link>pygame</link>
import random

# Initialize the game

pygame.init()

# Set up the game window

window_width = 800
window_height = 600
window = pygame.display.set_mode((window_width, window_height))
pygame.display.set_caption("Shooting Game")

# Set up the player

player_width = 50
player_height = 50
player_x = window_width // 2 - player_width // 2
player_y = window_height - player_height - 10
player_speed = 5
player = pygame.Rect(player_x, player_y, player_width, player_height)

# Set up the bullet

bullet_width = 10
bullet_height = 30
bullet_speed = 10
bullet = pygame.Rect(0, 0, bullet_width, bullet_height)
bullet_state = "ready"  # ready - bullet is not currently fired, fire - bullet is currently moving

# Set up the enemy

enemy_width = 50
enemy_height = 50
enemy_speed = 2
enemy = pygame.Rect(random.randint(0, window_width - enemy_width), 0, enemy_width, enemy_height)

# Set up the game loop

running = True
clock = pygame.time.Clock()

while running:
    # Handle events

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

        # Handle player movement

        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                player.x -= player_speed
            elif event.key == pygame.K_RIGHT:
                player.x += player_speed

        # Handle bullet firing

        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE and bullet_state == "ready":
                bullet.x = player.x + player_width // 2 - bullet_width // 2
                bullet.y = player.y
                bullet_state = "fire"

    # Update bullet position

    if bullet_state == "fire":
        bullet.y -= bullet_speed
        if bullet.y <= 0:
            bullet_state = "ready"

    # Update enemy position

    enemy.y += enemy_speed
    if enemy.y > window_height:
        enemy.x = random.randint(0, window_width - enemy_width)
        enemy.y = 0

    # Check for collision between bullet and enemy

    if bullet.colliderect(enemy):
        bullet_state = "ready"
        enemy.x = random.randint(0, window_width - enemy_width)
        enemy.y = 0

    # Check for collision between player and enemy

    if player.colliderect(enemy):
        running = False

    # Clear the screen

    window.fill((0, 0, 0))

    # Draw the player, bullet, and enemy

    pygame.draw.rect(window, (255, 0, 0), player)
    pygame.draw.rect(window, (0, 255, 0), bullet)
    pygame.draw.rect(window, (0, 0, 255), enemy)

    # Update the display

    pygame.display.update()

    # Limit the frame rate

    clock.tick(60)

# Quit the game

pygame.quit()
