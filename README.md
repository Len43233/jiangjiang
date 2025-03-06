<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>抽奖模拟</title>
    <style>
        body { text-align: center; font-family: Arial, sans-serif; }
        #result { font-size: 24px; margin-top: 20px; }
        #history { margin-top: 20px; }
        button { padding: 10px 20px; font-size: 18px; transition: transform 0.1s; }
        .shake { transform: scale(1.1); }
        .firework { position: absolute; width: 10px; height: 10px; background: red; border-radius: 50%; opacity: 0.8; }
    </style>
</head>
<body>
    <h1>抽奖模拟</h1>
    <button id="drawButton" onclick="drawLottery()">点击抽奖（消耗10单位）</button>
    <p id="result"></p>
    <p>净利润: <span id="netProfit">0</span> 单位</p>
    <div id="history"></div>

    <script>
        let netProfit = 0;
        const lotteryOdds = [
            { chance: 0.19, reward: 3 },
            { chance: 0.23, reward: 5 },
            { chance: 0.2344, reward: 25 },
            { chance: 0.20, reward: 20 },
            { chance: 0.103, reward: 25 },
            { chance: 0.02, reward: 40 },
            { chance: 0.02, reward: -25 },
            { chance: 0.0025, reward: 120 },
            { chance: 0.0001, reward: 300 }
        ];

        function drawLottery() {
            let button = document.getElementById("drawButton");
            button.classList.add("shake");
            setTimeout(() => button.classList.remove("shake"), 100);
            
            let rand = Math.random();
            let cumulative = 0;
            let reward = -10;
            for (let item of lotteryOdds) {
                cumulative += item.chance;
                if (rand < cumulative) {
                    reward += item.reward;
                    document.getElementById("result").innerText = `你抽中了：${item.reward} 单位`;
                    break;
                }
            }
            if (reward === -10) document.getElementById("result").innerText = "未中奖，扣除 10 单位";
            
            netProfit += reward;
            document.getElementById("netProfit").innerText = netProfit;
            
            let historyDiv = document.getElementById("history");
            let entry = document.createElement("p");
            entry.innerText = `抽奖结果: ${reward} 单位`;
            historyDiv.prepend(entry);
            
            if (reward > 0) triggerFireworks(reward);
        }

        function triggerFireworks(count) {
            for (let i = 0; i < count / 10; i++) {
                let firework = document.createElement("div");
                firework.classList.add("firework");
                document.body.appendChild(firework);
                
                let x = Math.random() * window.innerWidth;
                let y = Math.random() * window.innerHeight;
                firework.style.left = `${x}px`;
                firework.style.top = `${y}px`;
                
                setTimeout(() => firework.remove(), 1000);
            }
        }
    </script>
</body>
</html>
