## 요구사항

- 실습 코드

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />

        <title>Document</title>
        <style>
        body {
            width: 100vw;
            height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        button {
            margin-bottom: 10px;
        }
        img {
            // border-radius가 2초간 변하도록 애니메이션을 주세요.
        }
        .round {
            // 해당 클래스명을 가지면 모서리 둥글기가 50% 가 됩니다.
        }
        </style>
    </head>
    <body>
        <h2>만두 사진을 클릭하세요</h2>

        <button class="red">red</button>
        <button class="blue">blue</button>
        <button class="remove">remove border</button>

        <img src="./mandoo-hooray.jpg" alt="만두 사진" width="300" />

        <script>
            // mandoo 라는 변수명으로 img 태그를 선택해주세요
        
        // red 라는 변수명으로 red 라는 class 명을 가진 태그를 선택해주세요
        
        // blue 라는 변수명으로 blue 라는 class 명을 가진 태그를 선택해주세요
        
            // remove 라는 변수명으로 remove 라는 class 명을 가진 태그를 선택해주세요
        

                // mandoo 요소를 클릭하면 round 라는 클래스명이 붙고, 만약 이미 클래스명이 있다면 삭제됩니다

                // red 요소를 클릭하면 mandoo 요소의 테두리가 5px 실선 red 가 추가됩니다.
        
                // blue 요소를 클릭하면 mandoo 요소의 테두리가 5px 실선 blue 가 추가됩니다.
        
                // remove 요소를 클릭하면 mandoo 요소의 테두리가 사라집니다.
        
        </script>
    </body>
    </html>

    ```