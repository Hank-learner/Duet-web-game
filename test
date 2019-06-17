function background() {
    context.clearRect(0, 0, canvaswidth, canvasheight);
    context.imageSmoothingEnabled = false;
    context.drawImage(background2, 0, 0, canvaswidth, canvasheight);
}


var canvas = document.getElementById('canvas');
var context = canvas.getContext('2d');
var canvasheight = 550;
var canvaswidth = 800;
var gamestate = false;
var gameplaying = false;
background1 = document.getElementById("background1");
background2 = document.getElementById("background2");

var roundcenter = {
    x: canvaswidth / 2,
    y: 430
};
var roundradius = 70;

class Circle {
    constructor() {
        context.beginPath();
        context.arc(roundcenter.x, roundcenter.y, roundradius, 0, 2 * Math.PI);
        context.strokeStyle = "#FFFFFF";
        context.stroke();
        context.closePath();
    }
}

var ballsangle = 0;

var cosangle = Math.cos(ballsangle);
var sinangle = Math.sin(ballsangle);
var ball1 = {
    x: roundcenter.x - roundradius * cosangle,
    y: roundcenter.y - roundradius * sinangle
};
var ball2 = {
    x: roundcenter.x + roundradius * cosangle,
    y: roundcenter.y + roundradius * sinangle
};

var ballsradius = 12;
class Balls {
    constructor() {
    }
    draw() {
        cosangle = Math.cos(ballsangle);
        sinangle = Math.sin(ballsangle);
        ball1 = {
            x: roundcenter.x - roundradius * cosangle,
            y: roundcenter.y - roundradius * sinangle
        };
        ball2 = {
            x: roundcenter.x + roundradius * cosangle,
            y: roundcenter.y + roundradius * sinangle
        };
        context.beginPath();
        context.arc(ball1.x, ball1.y, ballsradius, 0, 2 * Math.PI);
        context.fillStyle = "#FF0830";
        context.closePath();
        context.fill();
        context.beginPath();
        context.arc(ball2.x, ball2.y, ballsradius, 0, 2 * Math.PI);
        context.fillStyle = "#20AEFF";
        context.closePath();
        context.fill();
    }

}


var obstacles = [];
var obstacle;
var barspeed = 0.5;
var barheight = 30;

class Obstacle {
    constructor() {
        this.random = Math.random();
        if (this.random < 0.33) {
            this.obstaclenumber = 1;
            this.barlength = 150;
            this.x = roundcenter.x - this.barlength;
        }
        else if (this.random < 0.66) {
            this.obstaclenumber = 2;
            this.barlength = 100;
            this.x = roundcenter.x - this.barlength / 2;

        }
        else {
            this.obstaclenumber = 3;
            this.barlength = 150;
            this.x = roundcenter.x;
        }
        this.y = -barheight;
        obstacles.push(this);

    }
    draw() {

        context.fillStyle = "white";
        context.fillRect(this.x, this.y, this.barlength, barheight);
        this.y += barspeed;
        if (this.y > canvasheight * 2) {
            obstacles.splice(obstacles.indexOf(this), 1);
        }

    }

    get obstaclex() {
        return this.x;
    }
    get obstacley() {
        return this.y;
    }
    get obstaclelength() {
        return this.barlength;
    }
}


function gameover() {
    for (let i = 0; i < obstacles.length; i++) {
        if (obstacles[i].obstaclenumber == 1) {
            if ((ball1.x - ballsradius < obstacles[i].obstaclex + obstacles[i].obstaclelength && ball1.y - ballsradius <= obstacles[i].obstacley + barheight && ball1.y + ballsradius >= obstacles[i].obstacley) || (ball2.x - ballsradius < obstacles[i].obstaclex + obstacles[i].obstaclelength && ball2.y - ballsradius <= obstacles[i].obstacley + barheight && ball2.y + ballsradius >= obstacles[i].obstacley)) { gamestate = false; }
        }
        else if (obstacles[i].obstaclenumber == 2) {
            if ((ball1.x + ballsradius >= obstacles[i].obstaclex && ball1.x - ballsradius <= obstacles[i].obstaclex + obstacles[i].obstaclelength && ball1.y - ballsradius <= obstacles[i].obstacley + barheight && ball1.y + ballsradius >= obstacles[i].obstacley) || (ball2.x + ballsradius >= obstacles[i].obstaclex && ball2.x - ballsradius <= obstacles[i].obstaclex + obstacles[i].obstaclelength && ball2.y - ballsradius <= obstacles[i].obstacley + barheight && ball2.y + ballsradius >= obstacles[i].obstacley)) { gamestate = false; }
        }
        else if (obstacles[i].obstaclenumber == 3) {
            if ((ball1.x + ballsradius > obstacles[i].obstaclex && ball1.y - ballsradius <= obstacles[i].obstacley + barheight && ball1.y + ballsradius >= obstacles[i].obstacley) || (ball2.x + ballsradius > obstacles[i].obstaclex && ball2.y - ballsradius <= obstacles[i].obstacley + barheight && ball2.y + ballsradius >= obstacles[i].obstacley)) { gamestate = false; }
        }
        if (gamestate == false) {
            gamestateimage.src = "play.png";

            if (localStorage.getItem("Highscore")) {
                var Highscore = parseFloat(localStorage.getItem("Highscore"));

                if (Highscore < score) {
                    localStorage.setItem("Highscore", score);
                }
            }
            else {
                localStorage.setItem("Highscore", score);
            }
            var message = "End of game";
            var newLine = "\r\n";
            message += newLine;
            if (playerturn == 1) {
                message += "Player 1 : ";
                player1score = score;
            }
            if (playerturn == 2) {
                message += "Player 2 : ";
                player2score = score;
            }
            message += "Your score : " + score;
            message += newLine;
            message += "Highscore : " + highscore;
            if (playerturn == 2) {
                message += newLine;
                message += newLine;
                message += "Player 1 score = " + player1score;
                message += newLine;
                message += "Player 2 score = " + player2score;
                message += newLine;
                if (player1score > player2score) message += "Player 1 wins";
                else if (player2score > player1score) message += "Player 2 wins";
                else message += "Draw";
            }
            window.alert(message);
            obstacles = [];

            timeperobstacle = 2100;
            barspeed = 0.5;
            ballsspeed = 0.01;
            barspeedchange = 0.003;
            ballspeedchange = 0.0001;
            mousedownccw = false;
            mousedowncw = false;
            score = 0;
            ballsangle = 0;

            cosangle = Math.cos(ballsangle);
            sinangle = Math.sin(ballsangle);
            ball1 = {
                x: roundcenter.x - roundradius * cosangle,
                y: roundcenter.y - roundradius * sinangle
            };
            ball2 = {
                x: roundcenter.x + roundradius * cosangle,
                y: roundcenter.y + roundradius * sinangle
            };
            audio.pause();
            audio.currentTime = 0;
            if (playerturn == 1) {
                playerturn++;
            }
            else {
                gameplaying = false;
                singleplayer.disabled = false;
                doubleplayer.disabled = false;

                if (playerturn == 2) {
                    reset();
                    playerturn = 0;
                }
            }
            startpage();
        }
    }

}
var score = 0;
var player1score = 0;
var player2score = 0;
var highscore = 0;
if (localStorage.getItem("Highscore")) {
    highscore = parseFloat(localStorage.getItem("Highscore"));
}
function gamescore() {
    context.textAlign = "left";
    context.fillStyle = "white";

    context.font = "20px Verdana";
    context.fillText("Score : " + score, 30, 40);
    if (highscore < score)
        highscore = score;
    context.fillText("Highscore : " + highscore, 30, 70);

    context.font = "30px Verdana";
    context.fillStyle = "#B43F75";
    context.fillText("Duet", 620, 60);

}

var players, playerturn;
var singleplayer = document.getElementById("single");
var doubleplayer = document.getElementById("double");
function reset() {
    players = 0;
    playerturn = 0;

    if (singleplayer.checked) {
        players = 1;
        startpage();

    }
    else if (doubleplayer.checked) {
        players = 2;
        console.log(players);
        playerturn = 1;
        context.textAlign = "center";
        context.font = "20px Verdana";
        context.fillStyle = "white";
        context.fillText("Player 1 turn", (canvaswidth / 2), (canvasheight / 3));
    }
    else {
        window.alert("select any player mode on left bottom corner");
    }
}
reset();


var ballsspeed = 0.01;

var mousedowncw = false;
var mousedownccw = false;
var balls = new Balls();
var timeperobstacle = 2100;

function startpage() {
    if (!gamestate)
        context.clearRect(0, 0, canvaswidth, canvasheight);
    context.textAlign = "center";
    context.font = "30px Verdana";
    context.rect(0, 0, canvas.width, canvas.height);
    context.fillStyle = "rgba(0,0,0,0.1)";
    context.fill();

    context.font = "20px Verdana";
    context.fillStyle = "white";
    if (playerturn == 1) {
        context.fillText("Player 1 turn", (canvaswidth / 2), (canvasheight / 3));
    }
    else if (playerturn == 2) {
        context.fillText("Player 2 turn", (canvaswidth / 2), (canvasheight / 3));
    }
    context.font = "30px Verdana";
    if (gamestate) {
        context.fillText("Press SPACE or PLAY button to resume ", (canvaswidth / 2), (canvasheight / 2));
    } else {
        context.fillStyle = "#B43F75";
        context.fillText("DUET", (canvaswidth / 2), (canvasheight / 5));
        context.fillStyle = "white";
        context.textAlign = "left";
        context.font = "20px Verdana";
        context.fillText("Highscore : " + highscore, 30, 70);
        context.textAlign = "center";
        context.font = "30px Verdana";
        context.fillText("Press SPACE or PLAY button to start ", (canvaswidth / 2), (canvasheight / 2) - 50);
        context.font = "15px Verdana";
        context.fillText("Press SPACE or PLAY button to Pause during game ", (canvaswidth / 2), (canvasheight / 2));
    }
    context.textAlign = "left";
    context.font = "15px Verdana";
    context.fillStyle = "#3c54c2";
    context.fillText("Controls:", (canvaswidth / 8), (canvasheight / 1.3));
    context.fillText("A [or] < arrow [or] COUNTERCLOCKWISE button   ---counterclockwise movement", (canvaswidth / 8), (canvasheight / 1.2));
    context.fillText("D [or] > arrow [or] CLOCKWISE button          ---clockwise movement", (canvaswidth / 8), (canvasheight / 1.1));
}
startpage();


var newobs = 300;
var newobsmax = 300;

//gameframe handling
var barspeedchange = 0.003;
var ballspeedchange = 0.0001;
function gameloop() {
    if (gamestate == true) {
        window.requestAnimationFrame(gameloop);
        if (!gameplaying) {
            gameplaying = true;
            singleplayer.disabled = true;
            doubleplayer.disabled = true;
        }

        background();
        new Circle();

        if (mousedownccw) ballsangle -= ballsspeed;
        if (mousedowncw) ballsangle += ballsspeed;

        balls.draw();

        for (let i = 0; i < obstacles.length; i++) {
            obstacles[i].draw();
        }

        newobsmax = 300 * 0.5 / barspeed;
        if (newobs >= newobsmax) {
            new Obstacle();
            barspeed += barspeedchange;
            ballsspeed += ballspeedchange;
            newobs = 0;
        }
        newobs++;

        gamescore();
        gameover();

    }
    else {
        mousedownccw = false;
        mousedowncw = false;
    }
}

var scoreincrement = setInterval(function () {
    if (gamestate == true)
        score++;

}, 200);
//

//input handling
var counterclockwisebtn = document.getElementById("btnleft");
var clockwisebtn = document.getElementById("btnright");
var gamestatebtn = document.getElementById("gamestate");
var gamestateimage = document.getElementById('gamestateimg');

counterclockwisebtn.addEventListener("mousedown", function () {
    mousedownccw = true;
});
clockwisebtn.addEventListener("mousedown", function () {
    mousedowncw = true;
});
document.addEventListener("mouseup", function () {
    mousedownccw = false;
    mousedowncw = false;
});

singleplayer.addEventListener("click", reset);
doubleplayer.addEventListener("click", reset);

function gamestatechange() {
    if (gamestate) {
        gamestateimage.src = "play.png";
        audio.pause();
        startpage();
        gamestate = false;

    }
    else {
        gamestateimage.src = "pause.png";
        gamestate = true;
        window.requestAnimationFrame(gameloop);
        if (musicstate)
            audio.play();
    }
}
gamestatebtn.addEventListener("mouseup", function () {
    gamestatechange();
});

document.addEventListener("keydown", event => {
    switch (event.keyCode) {
        case 37:
        case 65:
            mousedownccw = true;
            break;
        case 39:
        case 68:
            mousedowncw = true;
            break;
        case 32:
            gamestatechange();
            break;
        default: break;
    }
});
document.addEventListener("keyup", event => {
    switch (event.keyCode) {
        case 37:
        case 65:
            mousedownccw = false;
            break;
        case 39:
        case 68:
            mousedowncw = false;
            break;
        default: break;
    }
});


var audiobtn = document.getElementById("audiobtn");
var audio = document.getElementById("myaudio");
var audioimage = document.getElementById('audioimg');
var musicstate = true;
audio.volume = 0.1;
audiobtn.addEventListener("mouseup", music);
function music() {
    if (musicstate) {
        musicstate = false;
        audio.pause();
        audioimage.src = "soundout.png";
    }
    else {
        audio.play();
        musicstate = true;
        audioimage.src = "soundin.png";
    }
}
//