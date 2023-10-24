#  <!DOCTYPE html>

<html lang="en"> 
<head> 
    <meta charset="UTF-8"> 
    <meta name="viewport" content="width=device-width, initial-scale=1.0"> 
    <title>trafficlight</title> 
    <style> 
        .traffic-light { 
            width: 150px; 
            height: 320px; 
            background: black; 
            border: 1px
            solid #333;
            border-radius: 30px; 
            margin: 0 auto; 
            position: relative; 

    .light {
        width: 80px;
        height: 80px;
        background: gray;
        border-radius: 50%;
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
    }

    .light.red.active {
        background: red;
    }

    .light.yellow.active {
        background: yellow;
    }

    .light.green.active {
        background: green;
    }

    .light.red {
        top: 20px;
    }

    .light.yellow {
        top: 120px;
    }

    .light.green {
        top: 220px;
    }
    .countdown{
        font-family: 'Courier New', Courier, monospace;
       padding: 15px 5px;
        color: white;
        font-size: 100px;
        text-align: center;
        width: 100px;
        height: 100px;
        background: black;
        border: 5px solid #333;
        border-radius: 10px;
        margin: 0 auto;
       
    }
    
</style>
</head> 
<body> 
    <div class="traffic-light"> 
        <div class="light red">
                </div>
    <div class="light yellow">

    </div>
    <div class="light green">

    </div>
    
</div>
<div class="countdown"><span id="countdown"></span>
</div>


<script>
    const colors = ["Red", "Yellow", "Green","Yellow"];
    let index = 0;
    let timer;

    function countdown() {
        const currentColor = colors[index];
        const duration = getColorDuration(currentColor);
        updateTrafficLight(currentColor);

        let countdownValue = duration / 1000;
        updateCountdown(countdownValue);

        timer = setInterval(function () {
            countdownValue -= 1;
            if (countdownValue <= 0) {
                index = (index + 1) % colors.length;
                clearInterval(timer);
                countdown();
            } else {
                updateCountdown(countdownValue);
            }
        }, 1000);
    }

    function updateTrafficLight(currentColor) {
        const lights = document.querySelectorAll('.light');
        lights.forEach(light => light.classList.remove('active'));
        document.querySelector('.' + currentColor.toLowerCase()).classList.add('active');
    }

    function getColorDuration(color) {
        switch (color) {
            case "Red":
                return 60000;
            case "Yellow":
                return 20000; 
            case "Green":
                return 60000; 
            default:
                return 0;
        }
    }

    function updateCountdown(time) {
        document.getElementById('countdown').textContent = ` ${time}`;
    }

    countdown();
</script>
</body>
</html>
