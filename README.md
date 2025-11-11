# I-look-forward-to-our-meeting
I look forward to our meeting
font-size: 1.5rem;
            }
            
            .countdown {
                gap: 1rem;
            }
            
            .time-unit {
                min-width: 80px;
                padding: 0.8rem 0.3rem;
            }
            
            .time-value {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Обратный отсчет</h1>
        
        <div class="countdown">
            <div class="time-unit">
                <div class="time-value" id="days">0</div>
                <div class="time-label">дней</div>
            </div>
            <div class="time-unit">
                <div class="time-value" id="hours">0</div>
                <div class="time-label">часов</div>
            </div>
            <div class="time-unit">
                <div class="time-value" id="minutes">0</div>
                <div class="time-label">минут</div>
            </div>
            <div class="time-unit">
                <div class="time-value" id="seconds">0</div>
                <div class="time-label">секунд</div>
            </div>
        </div>
        
        <div class="target-date" id="target-date">До 28 ноября</div>
        
        <div class="quote">
            "Время не ждет. Каждый миг приближает нас к судьбоносному дню."
        </div>
    </div>

    <script>
        function updateCountdown() {
            // Получаем текущую дату
            const now = new Date();
            
            // Устанавливаем целевую дату (28 ноября текущего года)
            const currentYear = now.getFullYear();
            const targetDate = new Date(currentYear, 10, 28); // 10 = ноябрь (месяцы с 0)
            
            // Если 28 ноября уже прошло в этом году, устанавливаем на следующий год
            if (now > targetDate) {
                targetDate.setFullYear(currentYear + 1);
            }
            
            // Вычисляем разницу во времени
            const timeDifference = targetDate - now;
            
            // Вычисляем дни, часы, минуты и секунды
            const days = Math.floor(timeDifference / (1000 * 60 * 60 * 24));
            const hours = Math.floor((timeDifference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((timeDifference % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((timeDifference % (1000 * 60)) / 1000);
            
            // Обновляем отображение
            updateDisplay('days', days);
            updateDisplay('hours', hours.toString().padStart(2, '0'));
            updateDisplay('minutes', minutes.toString().padStart(2, '0'));
            updateDisplay('seconds', seconds.toString().padStart(2, '0'));
            
            // Обновляем текст с целевой датой
            document.getElementById('target-date').textContent = До 28 ноября ${targetDate.getFullYear()} года;
        }
        
        function updateDisplay(elementId, value) {
            const element = document.getElementById(elementId);
            if (element.textContent !== value.toString()) {
                element.classList.remove('changed');
                void element.offsetWidth; // Перезапуск анимации
                element.textContent = value;
                element.classList.add('changed');
            }
        }
        
        // Запускаем обратный отсчет сразу и каждую секунду
        updateCountdown();
        setInterval(updateCountdown, 1000);
    </script>
</body>
</html>
