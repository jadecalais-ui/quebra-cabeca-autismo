# cbtea-jogo-inclusao
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Quebra-Cabeça da Inclusão</title>

<style>
body{
    font-family: Arial, sans-serif;
    text-align:center;
    background:#f5f7fa;
    margin:0;
    padding:20px;
}

h1{
    color:#2c3e50;
}

#board{
    width:320px;
    height:320px;
    margin:20px auto;
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:2px;
    background:#ddd;
}

.tile{
    width:106px;
    height:106px;
    background:#4a90e2;
    color:white;
    font-size:32px;
    display:flex;
    justify-content:center;
    align-items:center;
    cursor:pointer;
    user-select:none;
    transition:0.2s;
}

.tile:hover{
    opacity:.9;
}

.empty{
    background:white;
    cursor:default;
}

#message{
    display:none;
    max-width:700px;
    margin:30px auto;
    padding:20px;
    background:white;
    border-radius:10px;
    box-shadow:0 0 10px rgba(0,0,0,.1);
}

button{
    padding:10px 20px;
    border:none;
    border-radius:5px;
    cursor:pointer;
    background:#4a90e2;
    color:white;
}
</style>
</head>
<body>

<h1>Monte o Quebra-Cabeça</h1>
<p>Organize as peças na ordem correta.</p>

<div id="board"></div>

<div id="message">
    <h2>Você percebeu algo?</h2>

    <p>
        Algumas peças parecem não se encaixar.
    </p>

    <p>
        Na vida, nem tudo precisa se encaixar perfeitamente para ter valor.
        Pessoas com Transtorno do Espectro Autista possuem características,
        formas de pensar e maneiras de se relacionar únicas.
    </p>

    <p>
        Inclusão não significa forçar todas as peças a serem iguais.
        Significa compreender que cada peça tem seu lugar e sua importância.
    </p>

    <button onclick="location.reload()">Jogar Novamente</button>
</div>

<script>

const board = document.getElementById('board');

let puzzle = [
    1,2,3,
    4,5,6,
    7,0,8
];

let attempts = 0;

function render(){

    board.innerHTML='';

    puzzle.forEach((value,index)=>{

        const tile=document.createElement('div');

        if(value===0){
            tile.className='tile empty';
        }else{
            tile.className='tile';
            tile.textContent=value;
            tile.onclick=()=>move(index);
        }

        board.appendChild(tile);
    });

    checkEnd();
}

function move(index){

    const emptyIndex=puzzle.indexOf(0);

    const validMoves=[
        emptyIndex-1,
        emptyIndex+1,
        emptyIndex-3,
        emptyIndex+3
    ];

    if(validMoves.includes(index)){

        [puzzle[index],puzzle[emptyIndex]] =
        [puzzle[emptyIndex],puzzle[index]];

        attempts++;

        render();
    }
}

function checkEnd(){

    const almostSolved =
    puzzle.join(',') === '1,2,3,4,5,6,7,8,0';

    if(almostSolved){

        setTimeout(()=>{
            alert(
              "Estranho... A última peça não parece pertencer a este quebra-cabeça."
            );

            document.getElementById('message').style.display='block';
            board.style.opacity='0.4';

        },300);
    }
}

render();

</script>

</body>
</html>
