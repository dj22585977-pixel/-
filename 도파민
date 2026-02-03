<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <title>도파민 서버 전용 협곡내전 밸런스툴</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #0f172a;
      color: #e5e7eb;
      padding: 20px;
    }
    h1 {
      text-align: center;
      color: #38bdf8;
    }
    .container {
      max-width: 900px;
      margin: 0 auto;
      background: #020617;
      padding: 25px;
      border-radius: 14px;
      box-shadow: 0 0 25px rgba(0,0,0,0.6);
    }
    .players {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 10px;
      margin-bottom: 20px;
    }
    input, select {
      padding: 8px;
      border-radius: 6px;
      border: none;
      width: 100%;
    }
    button {
      width: 100%;
      padding: 14px;
      background: #38bdf8;
      color: #020617;
      font-weight: bold;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      margin-top: 15px;
      font-size: 16px;
    }
    button:hover {
      background: #0ea5e9;
    }
    .teams {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 20px;
      margin-top: 25px;
    }
    .team {
      background: #020617;
      padding: 15px;
      border-radius: 10px;
      border: 1px solid #1e293b;
    }
    .team h2 {
      text-align: center;
      color: #facc15;
    }
    ul {
      list-style: none;
      padding: 0;
    }
    li {
      padding: 6px 0;
      border-bottom: 1px solid #1e293b;
    }
    .score {
      text-align: center;
      margin-top: 8px;
      font-weight: bold;
      color: #a5f3fc;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>도파민 서버 전용 협곡내전 밸런스툴</h1>
    <p style="text-align:center;">플레이어 10명을 입력하고 밸런스 팀을 생성하세요!</p>

    <div class="players" id="playerInputs"></div>

    <button onclick="balanceTeams()">팀 밸런스 생성</button>

    <div class="teams">
      <div class="team">
        <h2>팀 A</h2>
        <ul id="teamA"></ul>
        <div class="score" id="scoreA"></div>
      </div>
      <div class="team">
        <h2>팀 B</h2>
        <ul id="teamB"></ul>
        <div class="score" id="scoreB"></div>
      </div>
    </div>
  </div>

  <script>
    const tierScore = {
      "아이언": 1,
      "브론즈": 2,
      "실버": 3,
      "골드": 4,
      "플래티넘": 5,
      "에메랄드": 6,
      "다이아": 7,
      "마스터": 8,
      "그랜드마스터": 9,
      "챌린저": 10
    };

    const tiers = Object.keys(tierScore);

    // 입력칸 자동 생성
    const container = document.getElementById("playerInputs");
    for (let i = 1; i <= 10; i++) {
      const nameInput = document.createElement("input");
      nameInput.placeholder = `플레이어 ${i} (이름)`;

      const tierSelect = document.createElement("select");
      const defaultOption = document.createElement("option");
      defaultOption.textContent = "티어 선택";
      defaultOption.value = "";
      tierSelect.appendChild(defaultOption);

      tiers.forEach(tier => {
        const option = document.createElement("option");
        option.value = tier;
        option.textContent = tier;
        tierSelect.appendChild(option);
      });

      container.appendChild(nameInput);
      container.appendChild(tierSelect);
    }

    function balanceTeams() {
      const inputs = container.querySelectorAll("input, select");
      let players = [];

      for (let i = 0; i < inputs.length; i += 2) {
        const name = inputs[i].value.trim();
        const tier = inputs[i + 1].value.trim();
        if (name && tier) {
          players.push({
            name,
            tier,
            score: tierScore[tier]
          });
        }
      }

      if (players.length !== 10) {
        alert("플레이어 10명 모두 이름과 티어를 입력해주세요!");
        return;
      }

      // 점수 기준 정렬
      players.sort((a, b) => b.score - a.score);

      let teamA = [];
      let teamB = [];
      let scoreA = 0;
      let scoreB = 0;

      // 그리디 방식 팀 배분
      players.forEach(player => {
        if (scoreA <= scoreB) {
          teamA.push(player);
          scoreA += player.score;
        } else {
          teamB.push(player);
          scoreB += player.score;
        }
      });

      // 출력
      const teamAList = document.getElementById("teamA");
      const teamBList = document.getElementById("teamB");
      const scoreAText = document.getElementById("scoreA");
      const scoreBText = document.getElementById("scoreB");

      teamAList.innerHTML = "";
      teamBList.innerHTML = "";

      teamA.forEach(p => {
        const li = document.createElement("li");
        li.textContent = `${p.name} (${p.tier})`;
        teamAList.appendChild(li);
      });

      teamB.forEach(p => {
        const li = document.createElement("li");
        li.textContent = `${p.name} (${p.tier})`;
        teamBList.appendChild(li);
      });

      scoreAText.textContent = `팀 A 총점: ${scoreA}`;
      scoreBText.textContent = `팀 B 총점: ${scoreB}`;
    }
  </script>
</body>
</html>
