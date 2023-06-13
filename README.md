# Game
#EBE_Game


<!DOCTYPE html>
<html>
<head>
    <title>เกมสุ่มคำถามเกี่ยวกับความรู้รอบตัว</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f5f5f5;
            text-align: center;
        }

        h1 {
            color: #333333;
        }

        #container {
            background-color: #ffffff;
            width: 400px;
            margin: 0 auto;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        #question {
            font-weight: bold;
            margin-bottom: 10px;
        }

        button {
            display: block;
            width: 100%;
            padding: 10px;
            margin-bottom: 10px;
            font-size: 16px;
            background-color: #4CAF50;
            color: #ffffff;
            border: none;
            border-radius: 3px;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        button:hover {
            background-color: #45a049;
        }

        #score {
            margin-top: 20px;
        }

        #score span {
            font-weight: bold;
            font-size: 18px;
        }

        #answerKey {
            text-align: left;
            margin-top: 20px;
            font-weight: bold;
        }

        #answerKey ul {
            list-style-type: none;
            padding: 0;
        }

        #answerKey li {
            margin-bottom: 5px;
        }

        #answerKey li.correct {
            color: green;
        }

        #answerKey li.incorrect {
            color: red;
        }
    </style>
</head>
<body>
    <h1>เกมสุ่มคำถามเกี่ยวกับความรู้รอบตัว</h1>
    <div id="container">
        <p id="question"></p>
        <div id="choices"></div>
        <div id="score">คะแนน: <span id="scoreValue">0</span>/10</div>
        <div id="answerKey"></div>
    </div>

    <script>
        // รายการคำถาม
        var questions = [
            
            //1
            {
                question: "ทุก ๆ กี่ปีดาวศุกร์จะโคจรเข้าใกล้โลกมากที่สุด",
                choices: ["7", "8", "9", "10"],
                correctAnswer: 1
            },
            //2
            {
                question: "นักฟิสิกส์คนแรกของโลกคือใคร",
                choices: ["สตีเฟน ฮอว์กิง", "ไอแซก นิวตัน", "อัลเบิร์ต ไอน์สไตน์", "อคิมีดีส"],
                correctAnswer: 3
            },
            //3
            {
                question: "ประเทศใดผลิตทองแดงมากที่สุด",
                choices: ["ญี่ปุ่น", "จีน", "สหรัฐอเมริกา", "ไทย"],
                correctAnswer: 2
            },
            //4
            {
                question: "ชาติใดเป็นชาติแรกที่เดินเรือ",
                choices: ["โปรตุเกส", "จีน", "อียิปต์โบราณ", "รัสเซีย"],
                correctAnswer: 2
            },
            //5
            {
                question: "เทือกเขาแห่งใดยาวที่สุดในโลก",
                choices: ["เทือกเขาแอนดีส", " เทือกเขาหิมาลัย", "เทือกเขาอาร์กติกคอร์ดิลเลอรา", "เขาเอเวอเรสต์"],
                correctAnswer: 0
            },
            //6
            {
                question: "เทือกเขาที่มียอดเขาที่สูงสุดในโลก",
                choices: ["เทือกเขาแอนดีส", " เทือกเขาหิมาลัย", "เทือกเขาอาร์กติกคอร์ดิลเลอรา", "เขาเอเวอเรสต์"],
                correctAnswer: 3
            },
            //7
            {
                question: "แหล่งอารยธรรมที่เก่าแก่ที่สุดของจีนอยู่ในลุ่มแม่น้ำใด",
                choices: ["เแม่น้ำเจียง", "แม่น้ำยางเสือ", "แม่น้ำฮวงโห", "แม่น้ำชิน"],
                correctAnswer: 2
            },
            //8
            {
                question: "ในระบบสุริยคราส โลกเคลื่อนที่รอบอะไร?",
                choices: ["รอบดวงอาทิตย์", "รอบดาวเสาร์", "รอบดาวฤกษ์", "รอบดาวพฤหัสบดี"],
                correctAnswer: 0
            },
            //9
            {
                question: "เครื่องบินแรกที่บินขึ้นสู่อวกาศคือเครื่องบินชื่ออะไร?",
                choices: ["ไพโรชชั่นวัน", "อพอลโล 11", "ไพโรชชั่นมูน", "เชอร์รี่ ไลน์"],
                correctAnswer: 1
            },
            //11
            {
                question: "ผลไม้อะไรมีวิตามินซีสูงสุด",
                choices: ["มะขามป้อม", " มะขามเทศ", "ฝรั่ง", "กีวี"],
                correctAnswer: 2
            },
            //12
            {
                question: "หมีกรีซลี หมีตัวใหญ่ที่สุดในโลกอยู่ในดินแดนใด",
                choices: ["ทวีปยุโรป", "ทวีปอเมริกาใต้", "ทวีปเอเชีย", "ทวีปอเมริกาเหนือ"],
                correctAnswer: 3
            },
            //13
            {
                question: "ไทยเข้าเป็นสมาชิกองค์การสหประชาชาติในรัชสมัยใด",
                choices: ["รัชกาลที่9", "รัชกาลที่10", "รัชกาลที่8", "รัชกาลที่7"],
                correctAnswer: 0
            },
            //14
            {
                question: "ร่างกายของมนุษช่วงแรกเกิดมีกระดูกกี่ชิ้น",
                choices: ["320ชิ้น", "300ชิ้น", "280ชิ้น", "260ชิ้น"],
                correctAnswer: 1
            },
            //15
            {
                question: "ปลาน้ำจืดขนาดใหญ่ที่สุดในประเทศไทย และใหญ่ที่สุดในโลก คือปลาอะไร",
                choices: [" ปลาฉลาม", "ปลาบึก", "กระเบนแม่โขง", "ปลาอัลลิเกเตอร์"],
                correctAnswer: 2
            },
            //16
            {
                question: "โรคโลหิตจางเกิดจากการขาดธาตุอะไร",
                choices: ["วิตามินบี", "วิตามินซี", "เหล็ก", "กรดโฟลิก"],
                correctAnswer: 2
            },
            //17
            {
                question: "หน่วยแสดงความเร็วของเรือและลมเรียกว่าอะไร",
                choices: ["นอต", "เคลวิน", "เมตร", "กิโลเมตร"],
                correctAnswer: 0
            },
            //18
            {
                question: "ประเทศประชาธิปไตยใหญ่ที่สุดของโลกคือประเทศใด",
                choices: ["ประเทศไอซ์แลนด์", "ประเทศนอร์เวย์", "ประเทศไทย", "ประเทศอินเดีย"],
                correctAnswer: 3
            },
            //19
            {
                question: "โรเบิร์ต อี. เพียรี่ เดินทางไปพบอะไร",
                choices: ["เกาะนิวกินี", "เกาะกรีนแลนด์", "ขั้วโลกใต้", "ขั้วโลกเหนือ"],
                correctAnswer: 3
            },
            //20
            {
                question: "การเต้นรำฮูลาฮูละ นุ่งกระโปรงทำด้วยฟางเป็นของใคร",
                choices: ["ชาวมอแกน", "ชาวฮาวาย", "ชาวเซนติเนล", "ชาวกะเหรี่ยง"],
                correctAnswer: 1
            },
            //21
            {
                question: "เชื้อชาติในหมู่เกาะของอินโดนีเซีย กลุ่มเชื้อชาติใดมีมากที่สุด",
                choices: ["ชาวมาดูรา", "ชาวมลายู", "ชาวชวา", "ชาวซุนดา"],
                correctAnswer: 2
            },
            //22
            {
                question: "ทะเลแห่งใดในโลก เค็มน้อยที่สุด",
                choices: ["ทะเลบอลติก", "ทะเลเดดซี", "ทะเลแดง", "ทะเลเมดิเตอร์เรเนียน"],
                correctAnswer: 0
            },
            //23
            {
                question: "ดอกซากุระบานเดือนไหนในญี่ปุ่น",
                choices: ["เดือนสิงหาคม", "เดือนกันยายน", "เดือนมีนาคม", "เดือนเมษายน"],
                correctAnswer: 3
            },
            //24
            {
                question: " ชาวอียิปต์โบราณนับถือสัตว์เลี้ยงตัวใดดุจเทพเจ้า",
                choices: ["แมว", "หมา", "วัว", "ไก่"],
                correctAnswer: 0
            },
            //25
            {
                question: "ปะการังเป็นพืชหรือเป็นสัตว์ทะเล",
                choices: ["สัตว์ทะเล", "พืชทะเล"],
                correctAnswer: 0
            },
            //26
            {
                question: "กีฬารักบี้ใช้ผู้เล่นข้างละกี่คน",
                choices: ["13คน", "14คน", "15คน", "16คน"],
                correctAnswer: 2
            },
            //27
            {
                question: "เอฟ.บี.ไอ. เป็นหน่วยตำรวจสืบสวนของประเทศใด",
                choices: ["ออสเตรเลีย", "เม็กซิโก", "แคนาดา", "สหรัฐอมเริกา"],
                correctAnswer: 3
            },
            //28
            {
                question: "หมู่เลือดที่มีน้อยที่สุดของคนไทยคือหมู่ใด",
                choices: ["AB", "A", "B", "O"],
                correctAnswer: 0
            },
            //29
            {
                question: "สิ่งมีชีวิตที่อุบัติขึ้นเป็นสิ่งแรกในโลกคืออะไร",
                choices: ["ไดโนเสาร์", "มนุษย์", "จุลินทรีย์", "ลิง"],
                correctAnswer: 2
            },
            //30
            {
                question: "เมืองหลวงของญี่ปุ่นคือเมืองใด",
                choices: ["โอซากา", "โตเกียว", "เกียวโต", "ฟุกุโอกะ"],
                correctAnswer: 1
            },
            //31
            {
                question: "ชนชาติใดริเริ่มทอผ้าไหมเป็นชาติแรก",
                choices: ["จีน", "ไทย", "พม่า", "กัมพูชา"],
                correctAnswer: 0
            },
            //32
            {
                question: "ไม้ตัดดอกเขตหนาวที่ได้รับความนิยมสูงสุดของไทยคืออะไร",
                choices: ["เบญจมาศ", "บัวดิน", "เดซี่", "ดอกกุหลาบ"],
                correctAnswer: 3
            },
            //33
            {
                question: "กีฬากอล์ฟมีกี่หลุม",
                choices: ["16หลุม", "17หลุม", "18หลุม", "20หลุม"],
                correctAnswer: 2
            },
            //34
            {
                question: " คนไทยใช้บัตรประชาชนครั้งแรกเมื่อใด",
                choices: ["รัชกาลที่5", "รัชกาลที่6", "รัชกาลที่7", "รัชกาลที่8"],
                correctAnswer: 0
            },
            //35
            {
                question: "อักษรตัวแรกและตัวสุดท้ายของทุกทวีป คืออักษรตัวใด",
                choices: ["อักษร U", "อักษร E", "อักษร A", "อักษร S"],
                correctAnswer: 2
            },
            //36
            {
                question: "ดาวเคราะห์ดวงใดในระบบสุริยะมีขนาดเล็กที่สุด",
                choices: ["ดาวพลูโต", "ดาวอังคาร", "ดาวศุกร์", "ดาวพุธ"],
                correctAnswer: 3
            },
            //37
            {
                question: "เสียงเพลงแบบไหนทำให้แก้วแตก",
                choices: ["เสียงแบบคลื่นความถี่สูง", "เสียงแบบคลื่นความถี่ต่ำ"],
                correctAnswer: 0
            },
            //38
            {
                question: "เลขของโรมัน M เท่ากับจำนวนเลขอะไร",
                choices: ["1", "10", "100", "1000"],
                correctAnswer: 3
            },
            //39
            {
                question: "อวัยวะส่วนใดที่ใช้ในการรับรสอาหาร",
                choices: ["ปาก", "จมูก", "ฟัน", "ไม่มีข้อถูก"],
                correctAnswer: 3
            },
            //40
            {
                question: "โลกมีรูปร่างอย่างไร",
                choices: ["เกือบจะกลม", "เกือบจะแบน", "หัวใจ", "แล้วแต่จะเปลี่ยน"],
                correctAnswer: 0
            },
            // เพิ่มคำถามเพิ่มเติมที่นี่...
        ];

        var currentQuestion = 0;
        var score = 0;

        var questionElement = document.getElementById("question");
        var choicesElement = document.getElementById("choices");
        var scoreValueElement = document.getElementById("scoreValue");
        var answerKeyElement = document.getElementById("answerKey");

        // สุ่มคำถามที่ใช้ในเกม
        function shuffleQuestions() {
            for (var i = questions.length - 1; i > 0; i--) {
                var j = Math.floor(Math.random() * (i + 1));
                var temp = questions[i];
                questions[i] = questions[j];
                questions[j] = temp;
            }
        }

        // แสดงคำถามและตัวเลือก
        function displayQuestion() {
            var question = questions[currentQuestion];

            questionElement.textContent = question.question;

            choicesElement.innerHTML = "";

            for (var i = 0; i < question.choices.length; i++) {
                var choice = question.choices[i];
                var button = document.createElement("button");
                button.textContent = choice;
                button.value = i;
                button.onclick = checkAnswer;
                choicesElement.appendChild(button);
            }
        }

        // ตรวจสอบคำตอบที่ผู้เล่นเลือก
        function checkAnswer() {
            var selectedValue = parseInt(this.value);
            var question = questions[currentQuestion];

            if (selectedValue === question.correctAnswer) {
                score++;
                scoreValueElement.textContent = score;
            }

            currentQuestion++;

            if (currentQuestion === 10) {
                endGame();
            } else {
                displayQuestion();
            }
        }

        // สิ้นสุดเกมและแสดงเฉลยคำถาม
        function endGame() {
            var container = document.getElementById("container");
            container.innerHTML = "<h2>คุณจบเกมแล้ว!</h2>" +
                "<p>คะแนนที่คุณได้คือ " + score + " จาก 10 คำถาม</p>";

            displayAnswerKey();
        }

        // แสดงเฉลยคำถาม
        function displayAnswerKey() {
            answerKeyElement.innerHTML = "<h3>เฉลยคำถาม:</h3><ul>";

            for (var i = 0; i < questions.length; i++) {
                var question = questions[i];
                var listItem = document.createElement("li");
                listItem.textContent = question.question;

                if (i < 10) {
                    if (i === question.correctAnswer) {
                        listItem.className = "correct";
                    } else {
                        listItem.className = "incorrect";
                    }
                } else {
                    listItem.className = "hidden";
                }

                answerKeyElement.appendChild(listItem);
            }

            answerKeyElement.innerHTML += "</ul>";
        }

        // เริ่มเกม
        function startGame() {
            shuffleQuestions();
            displayQuestion();
        }

        startGame();
    </script>
</body>
</html>
