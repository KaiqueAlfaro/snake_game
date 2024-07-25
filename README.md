# Documentação Snake Game
## Introdução
Este projeto é uma implementação simples do jogo da cobrinha (Snake) utilizando a biblioteca Pygame em Python. O objetivo do jogo é controlar a cobra para comer a comida, fazendo com que ela cresça, enquanto evita colidir com as bordas da tela ou com ela mesma.

## Instalação
Para executar este jogo, você precisará ter Python e Pygame instalados em seu sistema.

1. **Instale o Python:** Certifique-se de ter o Python instalado em seu sistema.

2. **Instale o Pygame:** Após instalar o Python, você pode instalar o Pygame utilizando pip.


## Copiar código

        import pygame
        import time
        import random
        
        pygame.init()
        
        DISPLAY_WIDTH = 800
        DISPLAY_HEIGHT = 600
        
        def reset():
            global snake_block, snake_speed, snake_legth, snake_list
            global x, y, x_change, y_change
            global game_close, game_over
            global food_x, food_y
        
            snake_block = 20
            snake_speed = 10
            snake_legth = 1
            snake_list = []
        
            x = DISPLAY_WIDTH / 2
            y = DISPLAY_HEIGHT / 2
        
            x_change = 0
            y_change = 0
        
            game_over = False
            game_close = False
        
            food_x = round(random.randrange(0, DISPLAY_WIDTH - snake_block) / snake_block) * snake_block
            food_y = round(random.randrange(0, DISPLAY_HEIGHT - snake_block) / snake_block) * snake_block
        
        reset()
        
        white = (255, 255, 255)
        black = (0, 0, 0)
        blue = (0, 0, 255)
        red = (255, 0, 0)
        green = (0, 255, 0)
        
        dis = pygame.display.set_mode((DISPLAY_WIDTH, DISPLAY_HEIGHT))
        pygame.display.set_caption('Snake')
        
        clock = pygame.time.Clock()
        
        font_style = pygame.font.SysFont(None, 50)
        
        def message(msg, color):
            msg = font_style.render(msg, True, color)
            dis.blit(msg, [50, DISPLAY_HEIGHT / 2])
        
        def draw_snake(snake_block, snake_list):
            for x in snake_list:
                pygame.draw.rect(dis, blue, [x[0], x[1], snake_block, snake_block])
        
        while not game_close:
            while not game_over:
                for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        game_over = True
                    if event.type == pygame.KEYDOWN:
                        if event.key == pygame.K_w and y_change == 0:
                            y_change = -snake_block
                            x_change = 0
                        elif event.key == pygame.K_s and y_change == 0:
                            y_change = snake_block
                            x_change = 0
                        elif event.key == pygame.K_a and x_change == 0:
                            y_change = 0
                            x_change = -snake_block
                        elif event.key == pygame.K_d and x_change == 0:
                            y_change = 0
                            x_change = snake_block
        
                if x >= DISPLAY_WIDTH or x < 0 or y >= DISPLAY_HEIGHT or y < 0:
                    game_over = True
        
                x += x_change
                y += y_change
                        
                dis.fill(white)
        
                snake_head = [x, y]
                snake_list.append(snake_head)
        
                if len(snake_list) > snake_legth:
                    del snake_list[0]
        
                for i in snake_list[:-1]:
                    if i == snake_head:
                        game_over = True
        
                draw_snake(snake_block, snake_list)
                score = font_style.render("Score: " + str((snake_legth - 1) * 10), True, black)
                dis.blit(score, [0, 0])
                pygame.draw.rect(dis, green, [food_x, food_y, snake_block, snake_block])
                pygame.display.update()
        
                if x == food_x and y == food_y:
                    food_x = round(random.randrange(0, DISPLAY_WIDTH - snake_block) / snake_block) * snake_block
                    food_y = round(random.randrange(0, DISPLAY_HEIGHT - snake_block) / snake_block) * snake_block
                    snake_legth += 1
        
                clock.tick(snake_speed)
        
            dis.fill(black)
            message("You died! Pressione S- Sair J- Jogar de novo", red)
            pygame.display.update()
            
            for event in pygame.event.get():
                if event.type == pygame.QUIT:
                    game_close = True
                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_s:
                        game_close = True
                    elif event.key == pygame.K_j:
                        reset()
        
        pygame.quit()
        quit()
        
## Controles do Jogo
  - **W : Move a cobra para cima.**

  - **S : Move a cobra para baixo.**

  - **A : Move a cobra para a esquerda.**

  - **D : Move a cobra para a direita.**

## Lógica do Jogo
  - A cobra cresce ao comer a comida, que aparece aleatoriamente na tela.
  - O jogo termina se a cobra colidir com as bordas da tela ou consigo mesma.
  - Ao terminar o jogo, você pode pressionar "J" para jogar novamente ou "S" para sair.
## Melhorias Futuras
  - Adicionar níveis de dificuldade.
  - Implementar colisão suave com as bordas (teletransporte).
  - Melhorar o design da interface do usuário.
  - Adicionar efeitos sonoros e músicas.
## Contribuição
Sinta-se à vontade para contribuir com este projeto enviando pull requests ou reportando problemas na seção de issues.
