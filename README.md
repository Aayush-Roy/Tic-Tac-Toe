<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<style>
    *{
        margin: 0;
        padding: 0;
    }
    body{
        background-color: #548687;
        text-align: center;
    }
    .container{
        display: flex;
        justify-content:center;
        align-items: center;
        height: 70vh;
    }
    .game{
        height:60vmin;
        width: 60vmin;
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;
        gap:1.5vmin;
    }
    .box{
        height:18vmin;
        width: 18vmin;
        border-radius: 10px;
        border: 0;
        font-size: 8vmin;
        background-color: #ffffc7;
        color: #b0413e;
        box-shadow: 0 0 1rem rgba(0,0,0,0.4);
    }
    #reset-btn{
        padding: 1rem;
        font-size: 1.24rem;
        background-color: #191913;
        color: #fff;
        border-radius: 1rem;
        border: 0;
    }
    #new-btn{
        padding: 1rem;
        font-size: 1.24rem;
        background-color: #191913;
        color: #fff;
        border-radius: 1rem;
        border: 0;
    }
    #msg{
        color: #ffffc7;
        font-size: 8vmin;
    }
    .message-container{
        height: 30vmin;
    }
    .hide{
        display: none;
    }
</style>
<body>
    <div class="message-container hide">
        <p id="msg">Winner</p>
        <button id="new-btn">New Game</button>
    </div>
    <main>
        <h1>Tic Tac Toe</h1>
        <div class="container">
        <div class="game">
            <button class="box"></button>
            <button class="box"></button>
            <button class="box"></button>
            <button class="box"></button>
            <button class="box"></button>
            <button class="box"></button>
            <button class="box"></button>
            <button class="box"></button>
            <button class="box"></button>
        </div>
        </div>
        <button id="reset-btn">Reste Game</button>
    </main>

    <script>
        let boxes = document.querySelectorAll(".box");
        let resetBtn = document.querySelector("#reset-btn");
        let newGameBtn = document.querySelector("#new-btn");
        let msgContainer = document.querySelector(".message-container");
        let msg = document.querySelector("#msg");

        let turnO = true;
        const winPatterns = [
            [0,1,2],
            [0,3,6],
            [0,4,8],
            [1,4,7],
            [2,5,8],
            [2,4,6],
            [3,4,5],
            [6,7,8],
        ];
        boxes.forEach((box)=>{
            box.addEventListener("click",()=>{
                // console.log("clicked");
                box.innerText = "0";
                if(turnO)
                {
                    box.innerText = "O";
                    turnO = false;
                }
                else{
                    box.innerText = "X";
                    turnO = true;
                }
                box.disabled = true;
                checkWinner();
            });
        });

        const disableBoxes= () =>{
            for(let box of boxes)
            {
                box.disabled = true;
            }
        }

        const enableBoxes= () =>{
            for(let box of boxes)
            {
                box.disabled = false;
                box.innerText = "";
            }
        }


        const showWinner = (winner) =>{
            msg.innerText = `Congratulations, winner is ${winner}`
            msgContainer.classList.remove("hide");
            disableBoxes();
        }
        const checkWinner = ()=>{
            for(let pattern of winPatterns)
            {
                // console.log(pattern[0],pattern[1],pattern[2]);
                // console.log(boxes[pattern[0]].innerText,
                //             boxes[pattern[1]].innerText,
                //             boxes[pattern[2]].innerText);
            let pos1Val = boxes[pattern[0]].innerText;
            let pos2Val = boxes[pattern[1]].innerText;
            let pos3Val = boxes[pattern[2]].innerText;
            if(pos1Val !="" && pos2Val !="" && pos3Val !="")
            {
                if(pos1Val===pos2Val && pos2Val===pos3Val)
                {
                    // console.log("winner",pos1Val);
                    showWinner(pos1Val);
                }
            }
            }
            
        };
        const resetGame = () =>{
            turnO = true;
            enableBoxes();
            msgContainer.classList.add("hide");

        }

        newGameBtn.addEventListener("click", resetGame);
        resetBtn.addEventListener("click", resetGame);
    </script>
</body>
</html>
