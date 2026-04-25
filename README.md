<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Quiz Liên Quân - Trắc nghiệm cơ bản</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: Arial, sans-serif;
    }

    body {
      min-height: 100vh;
      background: linear-gradient(135deg, #101728, #1d2b53, #16213e);
      color: #ffffff;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 20px;
    }

    .app {
      width: 100%;
      max-width: 900px;
      background: rgba(255, 255, 255, 0.08);
      border: 1px solid rgba(255, 255, 255, 0.15);
      border-radius: 24px;
      box-shadow: 0 20px 60px rgba(0, 0, 0, 0.35);
      overflow: hidden;
      backdrop-filter: blur(14px);
    }

    .header {
      padding: 28px;
      background: rgba(255, 255, 255, 0.08);
      border-bottom: 1px solid rgba(255, 255, 255, 0.12);
    }

    .header h1 {
      font-size: clamp(28px, 5vw, 44px);
      margin-bottom: 10px;
      color: #ffd166;
    }

    .header p {
      color: #dce6ff;
      line-height: 1.6;
    }

    .content {
      padding: 28px;
    }

    .top-bar {
      display: flex;
      justify-content: space-between;
      gap: 16px;
      flex-wrap: wrap;
      margin-bottom: 20px;
    }

    .badge {
      background: rgba(255, 255, 255, 0.12);
      border: 1px solid rgba(255, 255, 255, 0.15);
      padding: 10px 14px;
      border-radius: 999px;
      font-weight: bold;
      color: #ffffff;
    }

    .progress-wrap {
      width: 100%;
      height: 12px;
      background: rgba(255, 255, 255, 0.16);
      border-radius: 999px;
      overflow: hidden;
      margin-bottom: 26px;
    }

    .progress {
      height: 100%;
      width: 0%;
      background: linear-gradient(90deg, #ffd166, #06d6a0);
      border-radius: 999px;
      transition: width 0.3s ease;
    }

    .card {
      background: rgba(255, 255, 255, 0.1);
      border: 1px solid rgba(255, 255, 255, 0.14);
      border-radius: 20px;
      padding: 24px;
      animation: fadeIn 0.25s ease;
    }

    @keyframes fadeIn {
      from {
        opacity: 0;
        transform: translateY(8px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    .question-title {
      color: #ffd166;
      font-size: 18px;
      margin-bottom: 12px;
      font-weight: bold;
    }

    .question {
      font-size: clamp(20px, 3vw, 28px);
      line-height: 1.4;
      margin-bottom: 22px;
      font-weight: bold;
    }

    .answers {
      display: grid;
      gap: 14px;
    }

    .answer-btn {
      width: 100%;
      text-align: left;
      border: 1px solid rgba(255, 255, 255, 0.16);
      background: rgba(255, 255, 255, 0.12);
      color: #ffffff;
      padding: 16px;
      border-radius: 16px;
      cursor: pointer;
      font-size: 16px;
      line-height: 1.45;
      transition: 0.2s ease;
    }

    .answer-btn:hover:not(:disabled) {
      background: rgba(255, 255, 255, 0.2);
      transform: translateY(-2px);
    }

    .answer-btn:disabled {
      cursor: not-allowed;
    }

    .answer-btn.correct {
      background: rgba(6, 214, 160, 0.28);
      border-color: #06d6a0;
    }

    .answer-btn.wrong {
      background: rgba(239, 71, 111, 0.28);
      border-color: #ef476f;
    }

    .feedback {
      min-height: 32px;
      margin-top: 18px;
      font-weight: bold;
      line-height: 1.5;
    }

    .feedback.correct-text {
      color: #06d6a0;
    }

    .feedback.wrong-text {
      color: #ff9bb2;
    }

    .actions {
      display: flex;
      justify-content: space-between;
      gap: 14px;
      flex-wrap: wrap;
      margin-top: 24px;
    }

    .btn {
      border: none;
      border-radius: 14px;
      padding: 14px 18px;
      font-weight: bold;
      cursor: pointer;
      font-size: 15px;
      transition: 0.2s ease;
    }

    .btn:hover {
      transform: translateY(-2px);
    }

    .btn-primary {
      background: #ffd166;
      color: #18213a;
    }

    .btn-secondary {
      background: rgba(255, 255, 255, 0.14);
      color: #ffffff;
      border: 1px solid rgba(255, 255, 255, 0.18);
    }

    .start-screen,
    .result-screen {
      text-align: center;
    }

    .start-screen h2,
    .result-screen h2 {
      font-size: clamp(26px, 4vw, 40px);
      color: #ffd166;
      margin-bottom: 16px;
    }

    .start-screen p,
    .result-screen p {
      color: #dce6ff;
      line-height: 1.7;
      margin-bottom: 22px;
    }

    .score-big {
      font-size: clamp(48px, 10vw, 84px);
      font-weight: bold;
      color: #06d6a0;
      margin: 18px 0;
    }

    .review {
      margin-top: 24px;
      text-align: left;
      display: grid;
      gap: 12px;
    }

    .review-item {
      background: rgba(255, 255, 255, 0.1);
      border-radius: 14px;
      padding: 14px;
      line-height: 1.5;
      border: 1px solid rgba(255, 255, 255, 0.12);
    }

    .review-item strong {
      color: #ffd166;
    }

    .hidden {
      display: none;
    }

    @media (max-width: 520px) {
      body {
        padding: 12px;
      }

      .header,
      .content {
        padding: 20px;
      }

      .answer-btn,
      .btn {
        font-size: 14px;
      }
    }
  </style>
</head>
<body>
  <main class="app">
    <section class="header">
      <h1>Quiz Liên Quân</h1>
      <p>Trắc nghiệm cơ bản về lane, vai trò, chất tướng, farm, bản đồ nhỏ và mục tiêu trong trận đấu.</p>
    </section>

    <section class="content">
      <div id="startScreen" class="card start-screen">
        <h2>Sẵn sàng kiểm tra kiến thức?</h2>
        <p>Bạn sẽ trả lời 20 câu hỏi trắc nghiệm. Sau mỗi câu, hệ thống sẽ báo đúng hoặc sai ngay lập tức.</p>
        <button class="btn btn-primary" onclick="startGame()">Bắt đầu chơi</button>
      </div>

      <div id="quizScreen" class="hidden">
        <div class="top-bar">
          <div class="badge" id="questionCounter">Câu 1 / 20</div>
          <div class="badge" id="scoreCounter">Điểm: 0</div>
        </div>

        <div class="progress-wrap">
          <div class="progress" id="progressBar"></div>
        </div>

        <div class="card">
          <div class="question-title" id="questionTitle">Câu 1</div>
          <div class="question" id="questionText"></div>
          <div class="answers" id="answersBox"></div>
          <div class="feedback" id="feedback"></div>

          <div class="actions">
            <button class="btn btn-secondary" onclick="restartGame()">Chơi lại</button>
            <button class="btn btn-primary" id="nextBtn" onclick="nextQuestion()" disabled>Câu tiếp theo</button>
          </div>
        </div>
      </div>

      <div id="resultScreen" class="card result-screen hidden">
        <h2>Hoàn thành!</h2>
        <p>Kết quả của bạn là:</p>
        <div class="score-big" id="finalScore">0/20</div>
        <p id="resultMessage"></p>
        <button class="btn btn-primary" onclick="restartGame()">Chơi lại từ đầu</button>
        <div class="review" id="reviewBox"></div>
      </div>
    </section>
  </main>

  <script>
    const questions = [
      {
        type: "multiple",
        question: "Một xạ thủ đang thắng đường nhưng rừng địch biến mất, Mid địch cũng không còn trên bản đồ. Cách xử lý chuyên nghiệp nhất là gì?",
        answers: [
          "Đẩy lính thật cao để phá trụ thật nhanh",
          "Lùi về vị trí an toàn và chờ tầm nhìn",
          "Đi vào bụi sông để kiểm tra vị trí địch",
          "Bỏ lính sang rừng địch để tìm giao tranh"
        ],
        correct: 1
      },
      {
        type: "multiple",
        question: "Sau khi đội bạn thắng giao tranh và hạ được 3 người bên địch, quyết định nào có giá trị chiến thuật cao nhất?",
        answers: [
          "Về nhà ngay để mua trang bị nhỏ",
          "Tận dụng lợi thế để lấy mục tiêu lớn",
          "Đuổi theo đỡ đòn địch còn đầy máu",
          "Chia nhau đi farm rừng riêng lẻ"
        ],
        correct: 1
      },
      {
        type: "multiple",
        question: "Một đội hình có nhiều sát thương nhưng thiếu chống chịu sẽ gặp vấn đề gì lớn nhất?",
        answers: [
          "Khó đứng giao tranh lâu và dễ bị ép góc",
          "Không thể farm lính ở bất kỳ lane nào",
          "Không thể mua trang bị trong trận đấu",
          "Luôn thắng giao tranh nếu đánh nhanh"
        ],
        correct: 0
      },
      {
        type: "multiple",
        question: "Khi chơi sát thủ đi rừng, mục tiêu ưu tiên trong giao tranh thường là ai?",
        answers: [
          "Đỡ đòn địch đứng đầu đội hình",
          "Lính xe đang đẩy vào trụ mình",
          "Xạ thủ hoặc pháp sư chủ lực địch",
          "Trụ ngoài cùng ở đường Caesar"
        ],
        correct: 2
      },
      {
        type: "multiple",
        question: "Nếu xạ thủ đội bạn bị hạ trước giao tranh lớn, đội nên xử lý thế nào?",
        answers: [
          "Vẫn lao vào giao tranh vì thiếu người không quan trọng",
          "Hạn chế giao tranh và chờ chủ lực hồi sinh",
          "Đẩy cao cả 3 đường để gây áp lực ngay",
          "Chia nhau đi vào bụi để kiểm tra tầm nhìn"
        ],
        correct: 1
      },
      {
        type: "multiple",
        question: "Một người chơi pháp sư dọn xong lính Mid nhưng không nhìn bản đồ và không đảo đường. Lỗi chính là gì?",
        answers: [
          "Không tận dụng vị trí trung tâm để hỗ trợ đội",
          "Không tranh lính với xạ thủ ở Đường Rồng",
          "Không đứng lại Mid cả trận để farm thêm",
          "Không đi một mình vào rừng địch đủ sâu"
        ],
        correct: 0
      },
      {
        type: "multiple",
        question: "Trong giao tranh tổng, xạ thủ chuyên nghiệp thường ưu tiên điều gì nhất?",
        answers: [
          "Sống sót và gây sát thương liên tục",
          "Lao lên trước để mở giao tranh",
          "Đi vòng sau để bắt sát thủ địch",
          "Bỏ giao tranh để farm quái rừng"
        ],
        correct: 0
      },
      {
        type: "multiple",
        question: "Nếu đội bạn đang hơn người và lính đã đẩy cao, mục tiêu nên ưu tiên là gì?",
        answers: [
          "Tìm thêm giao tranh nhỏ không cần mục tiêu",
          "Đẩy trụ hoặc ép mục tiêu lớn",
          "Về nhà dù chưa cần hồi phục",
          "Đứng chờ địch ra để đánh lại từ đầu"
        ],
        correct: 1
      },
      {
        type: "multiple",
        question: "Một Trợ Thủ tốt khi kiểm soát bụi cần làm gì?",
        answers: [
          "Đi một mình vào bụi sâu bất kể đồng đội ở đâu",
          "Kiểm tra bụi an toàn, có đồng đội gần hỗ trợ",
          "Đứng sau xạ thủ và để xạ thủ kiểm tra bụi",
          "Bỏ mặc tầm nhìn để tập trung farm lính"
        ],
        correct: 1
      },
      {
        type: "multiple",
        question: "Khi chơi Tel’Annas, điều nguy hiểm nhất ở giữa và cuối trận là gì?",
        answers: [
          "Đi lẻ khi không có tầm nhìn và không có bảo kê",
          "Đứng sau đội hình để bắn từ xa",
          "Farm lính để có thêm trang bị",
          "Đi cùng Trợ Thủ khi tranh mục tiêu"
        ],
        correct: 0
      },
      {
        type: "multiple",
        question: "Một đội thua giao tranh liên tục nhưng vẫn cố đánh 5v5 ở giữa bản đồ. Lỗi tư duy chính là gì?",
        answers: [
          "Không biết thay đổi nhịp trận để farm và thủ",
          "Không biết chọn trang phục phù hợp",
          "Không biết đứng gần nhà chính địch",
          "Không biết bỏ toàn bộ trụ để giao tranh"
        ],
        correct: 0
      },
      {
        type: "multiple",
        question: "Khi đội đang yếu hơn, cách chơi hợp lý nhất thường là gì?",
        answers: [
          "Farm an toàn, thủ trụ, chờ sai lầm đối thủ",
          "Lao vào giao tranh liên tục để thử vận may",
          "Bỏ lính để đi tìm mạng hạ gục",
          "Đi lẻ sâu để kiểm tra bản đồ"
        ],
        correct: 0
      },
      {
        type: "multiple",
        question: "Một người chơi Violet lăn lên để bắn rồi bị sát thủ bắt. Lỗi chính nằm ở đâu?",
        answers: [
          "Dùng kỹ năng cơ động sai mục đích",
          "Farm lính quá đều ở đầu trận",
          "Đứng sau Trợ Thủ trong giao tranh",
          "Không tranh lính với pháp sư Mid"
        ],
        correct: 0
      },
      {
        type: "multiple",
        question: "Trong đội hình, Trợ Thủ đỡ đòn quan trọng nhất khi nào?",
        answers: [
          "Khi đội cần người mở giao tranh và che chắn",
          "Khi đội cần người tranh farm với xạ thủ",
          "Khi đội cần nguồn sát thương chính tầm xa",
          "Khi đội cần người đứng im ở nhà chính"
        ],
        correct: 0
      },
      {
        type: "multiple",
        question: "Một đội thắng giao tranh nhưng không lấy trụ, Rồng hay Caesar. Đây là lỗi gì?",
        answers: [
          "Không chuyển lợi thế giao tranh thành mục tiêu",
          "Không biết chọn tướng xạ thủ dễ chơi",
          "Không biết đứng trong bụi đủ lâu",
          "Không biết đổi đường sau khi hồi sinh"
        ],
        correct: 0
      },
      {
        type: "multiple",
        question: "Khi chơi xạ thủ, vì sao không nên đứng quá gần bụi không có tầm nhìn?",
        answers: [
          "Vì có thể bị phục kích và mất chủ lực trước giao tranh",
          "Vì bụi làm xạ thủ không thể đánh thường",
          "Vì vào gần bụi sẽ mất toàn bộ vàng",
          "Vì bụi làm trụ đồng minh mất máu"
        ],
        correct: 0
      },
      {
        type: "multiple",
        question: "Trong giai đoạn cuối trận, một lần bị bắt lẻ có thể dẫn đến điều gì?",
        answers: [
          "Mất giao tranh, mất Caesar hoặc thua trận",
          "Nhận thêm vàng bù từ hệ thống",
          "Làm lính đội mình mạnh hơn ngay lập tức",
          "Khiến đối phương không thể phá trụ"
        ],
        correct: 0
      },
      {
        type: "multiple",
        question: "Một đội hình có xạ thủ mạnh nhưng không ai bảo kê sẽ gặp rủi ro gì?",
        answers: [
          "Xạ thủ dễ bị bắt và đội thiếu sát thương",
          "Xạ thủ sẽ tự động chống chịu tốt hơn",
          "Trợ Thủ sẽ nhận thêm sát thương miễn phí",
          "Đội không cần kiểm soát bản đồ nữa"
        ],
        correct: 0
      },
      {
        type: "multiple",
        question: "Khi đội bạn chuẩn bị ăn Caesar, xạ thủ nên đứng ở đâu?",
        answers: [
          "Vị trí an toàn phía sau, có đồng đội che chắn",
          "Một mình trong bụi sâu để tìm sát thủ địch",
          "Tuyến trước để nhận sát thương thay đội",
          "Bỏ Caesar để đi đẩy lẻ không có tầm nhìn"
        ],
        correct: 0
      },
      {
        type: "multiple",
        question: "Tư duy chuyên nghiệp trong Liên Quân thể hiện rõ nhất ở điều nào?",
        answers: [
          "Biết biến farm, giao tranh và tầm nhìn thành mục tiêu",
          "Luôn đánh nhau dù thiếu người và thiếu tầm nhìn",
          "Chỉ quan tâm số mạng hạ gục của bản thân",
          "Chọn tướng theo cảm xúc và bỏ qua đội hình"
        ],
        correct: 0
      },
      {
        type: "truefalse",
        question: "Ghi Đ hoặc S cho từng nhận định sau:",
        statements: [
          "Xạ thủ càng về cuối trận càng cần đi cùng đồng đội và tránh bị bắt lẻ.",
          "Nếu đội vừa thắng giao tranh, việc lấy mục tiêu thường quan trọng hơn đi lang thang tìm thêm mạng.",
          "Trợ Thủ nên để xạ thủ tự kiểm tra bụi vì xạ thủ có sát thương cao hơn.",
          "Khi không thấy rừng địch trên bản đồ, người chơi đi đường nên cẩn thận hơn."
        ],
        correct: [true, true, false, true]
      },
      {
        type: "truefalse",
        question: "Ghi Đ hoặc S cho từng nhận định sau:",
        statements: [
          "Đỡ đòn không nhất thiết phải đi đường Caesar, nhiều tướng đỡ đòn thường chơi Trợ Thủ.",
          "Sát thủ nên ưu tiên lao vào đỡ đòn địch vì đó là mục tiêu nhiều máu nhất.",
          "Farm tốt giúp người chơi có vàng, kinh nghiệm và trang bị nhanh hơn.",
          "Một đội đang thiếu người vẫn nên giao tranh lớn nếu chưa có tầm nhìn và chủ lực chưa tới."
        ],
        correct: [true, false, true, false]
      }
    ];

    let currentQuestion = 0;
    let score = 0;
    let answered = false;
    let userAnswers = [];
    let trueFalseSelected = [];

    const startScreen = document.getElementById("startScreen");
    const quizScreen = document.getElementById("quizScreen");
    const resultScreen = document.getElementById("resultScreen");
    const questionCounter = document.getElementById("questionCounter");
    const scoreCounter = document.getElementById("scoreCounter");
    const progressBar = document.getElementById("progressBar");
    const questionTitle = document.getElementById("questionTitle");
    const questionText = document.getElementById("questionText");
    const answersBox = document.getElementById("answersBox");
    const feedback = document.getElementById("feedback");
    const nextBtn = document.getElementById("nextBtn");
    const finalScore = document.getElementById("finalScore");
    const resultMessage = document.getElementById("resultMessage");
    const reviewBox = document.getElementById("reviewBox");

    function startGame() {
      startScreen.classList.add("hidden");
      resultScreen.classList.add("hidden");
      quizScreen.classList.remove("hidden");
      currentQuestion = 0;
      score = 0;
      userAnswers = [];
      loadQuestion();
    }

    function loadQuestion() {
      answered = false;
      trueFalseSelected = [];
      nextBtn.disabled = true;
      feedback.textContent = "";
      feedback.className = "feedback";
      answersBox.innerHTML = "";

      const item = questions[currentQuestion];
      questionCounter.textContent = `Câu ${currentQuestion + 1} / ${questions.length}`;
      scoreCounter.textContent = `Điểm: ${score}`;
      progressBar.style.width = `${(currentQuestion / questions.length) * 100}%`;
      questionTitle.textContent = `Câu ${currentQuestion + 1}`;
      questionText.textContent = item.question;

      if (item.type === "multiple") {
        renderMultipleChoice(item);
      } else {
        renderTrueFalse(item);
      }
    }

    function renderMultipleChoice(item) {
      item.answers.forEach((answer, index) => {
        const button = document.createElement("button");
        button.className = "answer-btn";
        button.textContent = `${String.fromCharCode(65 + index)}. ${answer}`;
        button.onclick = () => chooseAnswer(index, button);
        answersBox.appendChild(button);
      });
    }

    function renderTrueFalse(item) {
      item.statements.forEach((statement, index) => {
        trueFalseSelected[index] = null;

        const row = document.createElement("div");
        row.className = "answer-btn";
        row.style.cursor = "default";

        const label = document.createElement("div");
        label.style.marginBottom = "12px";
        label.textContent = `${String.fromCharCode(97 + index)}. ${statement}`;

        const trueBtn = document.createElement("button");
        trueBtn.className = "btn btn-secondary";
        trueBtn.textContent = "Đúng";
        trueBtn.style.marginRight = "10px";
        trueBtn.onclick = () => selectTrueFalse(index, true, trueBtn, falseBtn);

        const falseBtn = document.createElement("button");
        falseBtn.className = "btn btn-secondary";
        falseBtn.textContent = "Sai";
        falseBtn.onclick = () => selectTrueFalse(index, false, falseBtn, trueBtn);

        row.appendChild(label);
        row.appendChild(trueBtn);
        row.appendChild(falseBtn);
        answersBox.appendChild(row);
      });

      const submitBtn = document.createElement("button");
      submitBtn.className = "btn btn-primary";
      submitBtn.textContent = "Nộp câu trả lời";
      submitBtn.style.marginTop = "12px";
      submitBtn.onclick = submitTrueFalse;
      answersBox.appendChild(submitBtn);
    }

    function selectTrueFalse(index, value, selectedBtn, otherBtn) {
      if (answered) return;
      trueFalseSelected[index] = value;
      selectedBtn.style.background = "#ffd166";
      selectedBtn.style.color = "#18213a";
      otherBtn.style.background = "rgba(255, 255, 255, 0.14)";
      otherBtn.style.color = "#ffffff";
    }

    function chooseAnswer(selectedIndex, selectedButton) {
      if (answered) return;
      answered = true;
      nextBtn.disabled = false;

      const item = questions[currentQuestion];
      const allButtons = document.querySelectorAll(".answer-btn");
      const isCorrect = selectedIndex === item.correct;

      userAnswers.push({
        type: "multiple",
        question: item.question,
        selected: selectedIndex,
        correct: item.correct,
        answers: item.answers,
        isCorrect
      });

      allButtons.forEach((button, index) => {
        button.disabled = true;
        if (index === item.correct) {
          button.classList.add("correct");
        }
      });

      if (isCorrect) {
        score++;
        selectedButton.classList.add("correct");
        feedback.textContent = "Chính xác! Bạn đã chọn đúng.";
        feedback.classList.add("correct-text");
      } else {
        selectedButton.classList.add("wrong");
        feedback.textContent = `Chưa đúng. Đáp án đúng là ${String.fromCharCode(65 + item.correct)}.`;
        feedback.classList.add("wrong-text");
      }

      scoreCounter.textContent = `Điểm: ${score}`;
    }

    function submitTrueFalse() {
      if (answered) return;

      const item = questions[currentQuestion];
      const hasEmptyAnswer = trueFalseSelected.some(answer => answer === null);

      if (hasEmptyAnswer) {
        feedback.textContent = "Bạn cần chọn Đúng hoặc Sai cho đủ 4 ý.";
        feedback.classList.add("wrong-text");
        return;
      }

      answered = true;
      nextBtn.disabled = false;

      const result = trueFalseSelected.map((answer, index) => answer === item.correct[index]);
      const correctCount = result.filter(Boolean).length;
      const isCorrect = correctCount === item.correct.length;

      if (isCorrect) {
        score++;
        feedback.textContent = "Chính xác! Bạn đã làm đúng toàn bộ câu này.";
        feedback.classList.add("correct-text");
      } else {
        feedback.textContent = `Bạn đúng ${correctCount}/4 ý. Đáp án đúng: ${item.correct.map(value => value ? "Đ" : "S").join(", ")}.`;
        feedback.classList.add("wrong-text");
      }

      userAnswers.push({
        type: "truefalse",
        question: item.question,
        statements: item.statements,
        selected: [...trueFalseSelected],
        correct: item.correct,
        isCorrect,
        correctCount
      });

      document.querySelectorAll("#answersBox button").forEach(button => {
        button.disabled = true;
      });

      scoreCounter.textContent = `Điểm: ${score}`;
    }

    function nextQuestion() {
      currentQuestion++;

      if (currentQuestion < questions.length) {
        loadQuestion();
      } else {
        showResult();
      }
    }

    function showResult() {
      quizScreen.classList.add("hidden");
      resultScreen.classList.remove("hidden");
      progressBar.style.width = "100%";
      finalScore.textContent = `${score}/${questions.length}`;

      const percent = Math.round((score / questions.length) * 100);

      if (percent >= 90) {
        resultMessage.textContent = "Xuất sắc! Bạn nắm kiến thức rất chắc.";
      } else if (percent >= 70) {
        resultMessage.textContent = "Tốt lắm! Bạn đã hiểu phần lớn kiến thức cơ bản.";
      } else if (percent >= 50) {
        resultMessage.textContent = "Ổn rồi, nhưng bạn nên ôn lại một số phần.";
      } else {
        resultMessage.textContent = "Bạn nên học lại bài và chơi lại để nhớ lâu hơn.";
      }

      renderReview();
    }

    function renderReview() {
      reviewBox.innerHTML = "";

      userAnswers.forEach((item, index) => {
        const div = document.createElement("div");
        div.className = "review-item";

        if (item.type === "multiple") {
          const selectedText = item.selected === null
            ? "Chưa chọn"
            : `${String.fromCharCode(65 + item.selected)}. ${item.answers[item.selected]}`;

          const correctText = `${String.fromCharCode(65 + item.correct)}. ${item.answers[item.correct]}`;

          div.innerHTML = `
            <strong>Câu ${index + 1}: ${item.isCorrect ? "Đúng" : "Sai"}</strong><br>
            ${item.question}<br>
            Bạn chọn: ${selectedText}<br>
            Đáp án đúng: ${correctText}
          `;
        } else {
          const lines = item.statements.map((statement, statementIndex) => {
            const selected = item.selected[statementIndex] ? "Đ" : "S";
            const correct = item.correct[statementIndex] ? "Đ" : "S";
            return `${String.fromCharCode(97 + statementIndex)}. ${statement}<br>Bạn chọn: ${selected} | Đáp án: ${correct}`;
          }).join("<br><br>");

          div.innerHTML = `
            <strong>Câu ${index + 1}: ${item.isCorrect ? "Đúng toàn bộ" : `Đúng ${item.correctCount}/4 ý`}</strong><br>
            ${item.question}<br><br>
            ${lines}
          `;
        }

        reviewBox.appendChild(div);
      });
    }

    function restartGame() {
      startGame();
    }
  </script>
</body>
</html>
