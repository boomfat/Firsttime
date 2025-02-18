# Firsttime
import pygame
import random

# Initialize Pygame
pygame.init()

# Screen dimensions
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Interactive Bouncing Balls")

# Colors
WHITE = (255, 255, 255)

# Ball class
class Ball:
    def __init__(self):
        self.radius = random.randint(15, 40)
        self.x = random.randint(self.radius, WIDTH - self.radius)
        self.y = random.randint(self.radius, HEIGHT - self.radius)
        self.color = (random.randint(50, 255), random.randint(50, 255), random.randint(50, 255))
        self.speed_x = random.choice([-5, 5])
        self.speed_y = random.choice([-5, 5])

    def move(self):
        self.x += self.speed_x
        self.y += self.speed_y

        # Bounce off walls
        if self.x - self.radius <= 0 or self.x + self.radius >= WIDTH:
            self.speed_x = -self.speed_x
        if self.y - self.radius <= 0 or self.y + self.radius >= HEIGHT:
            self.speed_y = -self.speed_y

    def draw(self):
        pygame.draw.circle(screen, self.color, (self.x, self.y), self.radius)

# List of balls
balls = [Ball() for _ in range(5)]  # Start with 5 balls

# Game loop
running = True
clock = pygame.time.Clock()

while running:
    screen.fill(WHITE)  # Clear screen

    # Move and draw all balls
    for ball in balls:
        ball.move()
        ball.draw()

    # Event handling
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        elif event.type == pygame.MOUSEBUTTONDOWN:  # Add new ball on click
            balls.append(Ball())

    pygame.display.flip()
    clock.tick(60)  # Limit to 60 FPS

pygame.quit()

