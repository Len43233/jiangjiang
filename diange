<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>抽奖模拟</title>
    <style>
        body { text-align: center; font-family: Arial, sans-serif; }
        #result { font-size: 24px; margin-top: 20px; }
        button { padding: 10px 20px; font-size: 18px; }
    </style>
</head>
<body>
    <h1>抽奖模拟</h1>
    <button onclick="drawLottery()">点击抽奖（消耗10单位）</button>
    <p id="result"></p>

    <script>
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
            let rand = Math.random();
            let cumulative = 0;
            for (let item of lotteryOdds) {
                cumulative += item.chance;
                if (rand < cumulative) {
                    document.getElementById("result").innerText = `你抽中了：${item.reward} 单位`;
                    return;
                }
            }
            document.getElementById("result").innerText = "未中奖，扣除 10 单位";
        }
    </script>
</body>
</html>
