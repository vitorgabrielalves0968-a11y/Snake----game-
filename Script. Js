// 1. CONECTAR COM O HTML, VOU USAR VARIÁVEIS CONSTANTES, OQUE SIGNIFICA QUE ELAS NÃO PODEM SER REATRIBUÍDAS (PARTE 1)
const canvas = document.querySelector('canvas')
const ctx = canvas.getContext('2d')
const size = 20 

// COMO A COBRA FOI FEITA 001 (ME ACOMPANHE...)
// A cabeça da cobra é o ÚLTIMO elemento do array (index: snake.length - 1) SÃO COORDENADAS NA TELA/CANVAS, ENTÃO O X É A POSIÇÃO HORIZONTAL E O Y É A POSIÇÃO VERTICAL
let snake = [
    {x: 200, y: 200},
    {x: 220, y: 200},
    {x: 240, y: 200} // Cabeça inicial, ESSE QUADRADO É DIFERENCIADO, VIQUE VENDO.
] 
let direction; // Variável para armazenar a direção atual da cobra (inicialmente indefinida)
let loopId; // Variável para armazenar o ID do loop do jogo (usado para controlar o setTimeout) que é o ciclo que redesenha a tela dentro do intervalo definido (50ms nesse caso)
            // oque cria uma ilusão de movimento 

            // --- REGRAS DA MAÇÃ ---//
            //Ficou bonito o titulo né? kkkkkkkk
// Função para gerar um número aleatório múltiplo de 20 (dentro do grid/canvas) 001 

const randomNum = (min, max) => {
    return Math.round(Math.random() * (max - min) + min) // Gera um número aleatório entre min e max, arredondado para o inteiro mais próximo, garantindo que seja um múltiplo de 20 para se alinhar com o grid do jogo.
}

// Função para gerar uma posição aleatória para a maçã, garantindo que seja um múltiplo de 20 (tamanho do grid) 002
const randomPosition = () => {
    const number = randomNum(0, canvas.width - size)
    return Math.round(number / size) * size // Garante que a posição seja um múltiplo de 20, alinhando a maçã ao grid
}

// Posição inicial da maçã
let food = { // Objeto para representar a maçã, com propriedades x, y e color
    x: randomPosition(),
    y: randomPosition(),
    color: "red"
}

const drawFood = () => {
    ctx.fillStyle = food.color
    ctx.fillRect(food.x, food.y, size, size)
}

// Como a cobra foi feita 002 (tá mais pra cubo né? kkkkkkk)
const drawSnake = () => {
    snake.forEach((position, index) => {
        // Define a cor do corpo
        ctx.fillStyle = "#00aeff" // Cor da cobra (azul claro)
        ctx.strokeStyle = "black" // Define a cor da borda para destacar os gomos
        ctx.lineWidth = 2 // Define a largura da borda para destacar os gomos
        ctx.strokeRect(position.x, position.y, size, size)
        

        // Se for o último elemento, que é a cabeça, então muda a cor para Cyan
        if (index === snake.length - 1) {
            ctx.fillStyle = "cyan"
        }

        ctx.fillRect(position.x, position.y, size, size)
    })
}

const moveSnake = () => {
    const head = snake[snake.length - 1]
    if (!direction) return

    let newHead = { x: head.x, y: head.y }

    // Correção da string "right"
    if (direction === "right") {
        newHead.x += size
    }
    if (direction === "left") {
        newHead.x -= size
    }
    if (direction === "down") {
        newHead.y += size
    }
    if (direction === "up") {
        newHead.y -= size
    }

    snake.push(newHead)

    // Se a cabeça comer a maçã
    if (newHead.x === food.x && newHead.y === food.y) {
        // Cria uma nova maçã em lugar aleatório
        food.x = randomPosition()
        food.y = randomPosition()
        // Não remove o último gomo (a cobra cresce)
    } else {
        // Remove o último gomo da cauda para dar o efeito de movimento normal
        snake.shift()
    }
}
// função para desenhar o grid do jogo, para ajudar a visualizar melhor o movimento da cobra e a posição da maçã, além de dar um toque mais retrô ao jogo
const drawGrid = () => {
    ctx.lineWidth = 1
    ctx.strokeStyle = "#191919"
    for (let x = 0; x < canvas.width; x += size) {
        ctx.beginPath() // Inicia um novo caminho para cada linha, garantindo que as linhas sejam desenhadas corretamente sem se sobrepor
        ctx.moveTo(x, 0) // Move o ponto de início para a posição (x, 0), ou seja, o topo do canvas na coordenada x atual
        ctx.lineTo(x, canvas.height) // Desenha uma linha vertical da posição (x, 0) até (x, canvas.height), ou seja, do topo até o fundo do canvas na coordenada x atual
        ctx.stroke() // Desenha a linha no canvas usando as configurações de estilo definidas (cor e largura da linha)
    }
    for (let y = 0; y < canvas.height; y += size) {
        ctx.beginPath()
        ctx.moveTo(0, y)
        ctx.lineTo(canvas.width, y)
        ctx.stroke()
    }
}

// --- REGRA DO GAME OVER ---
const checkCollision = () => {
    const head = snake[snake.length - 1] // Pegando a cabeça da cobra, que é o último elemento do array snake
    
    // Se bater nas paredes do canvas (0 até 600)

    if (head.x < 0 || head.x >= canvas.width || head.y < 0 || head.y >= canvas.height) {
        gameOver() // Chama a função de game over, que para o jogo e reinicia a posição da cobra e da maçã
    }
}

const gameOver = () => {
    direction = undefined // Para o movimento do canvas, ja que a direção é indefinida, a cobra para de se mover, pois a mesma colidiu com a parede, ou seja, perdeu o jogo
    alert("Game Over! Tente novamente se tiver coragem....")
    
    // Reinicia a cobra para a posição inicial
    snake = [
        {x: 200, y: 200},
        {x: 220, y: 200},
        {x: 240, y: 200}
    ]
    food.x = randomPosition() // Gera uma nova posição aleatória para a maçã, referente a coordenada x
    food.y = randomPosition() // Gera uma nova posição aleatória para a maçã, referente a coordenada y
}

const gameLoop = () => {
    clearTimeout(loopId) //Se usa setTimeout, limpamos com clearTimeout

    ctx.clearRect(0, 0, canvas.width, canvas.height) 
    drawGrid() // Desenha o grid antes de desenhar a comida e a cobra, para que o grid fique atrás deles
    drawFood() // Desenha a maçã
    drawSnake() // Desenha a cobra
    moveSnake() //move a cobra, atualizando sua posição com base na direção atual
    checkCollision() // Verifica se perdeu
    
    loopId = setTimeout(() => {
        gameLoop()
    }, 50) // A cada 50ms, o jogo é atualizado, criando a ilusão de movimento
}

gameLoop()

// Capturando os movimentos do teclado corretamente (VULGO "DOR DE CABEÇA....") 
document.addEventListener("keydown", (event) => {
    const key = event.key // Pegando a propriedade key do evento

    if (key === "ArrowRight" && direction !== "left") {
        direction = "right"
    }
    if (key === "ArrowLeft" && direction !== "right") {
        direction = "left"
    }
    if (key === "ArrowUp" && direction !== "down") {
        direction = "up"
    }
    if (key === "ArrowDown" && direction !== "up") {
        direction = "down"
    }
})
