- 아래 실습 베이스 코드를 사용해주세요.
    - HTML 코드
        
        ```html
        <!DOCTYPE html>
        <html lang="en">
          <head>
            <meta charset="UTF-8" />
            <meta name="viewport" content="width=device-width, initial-scale=1.0" />
            <link rel="stylesheet" href="./reset.css" />
            <link rel="stylesheet" href="./animation-practice.css" />
            <title>Document</title>
          </head>
          <body>
            <div class="container">
              <div class="box">
                <div class="loader4"></div>
                <p>loader 4</p>
              </div>
            </div>
          </body>
        </html>
        ```
        
    - CSS 코드
        
        `✅ 여기에 코드를 작성하세요` 부분에만 작성해주시면 됩니다.
        
        ```css
        @import url(https://fonts.googleapis.com/css?family=Lato:300);
        
        .container {
          text-align: center;
          background-color: #e74c3c;
          overflow: hidden;
        }
        
        .loader4 {
          position: relative;
          width: 150px;
          height: 20px;
        
          top: 45%;
          top: -webkit-calc(50% - 10px);
          top: calc(50% - 10px);
          left: 25%;
          left: -webkit-calc(50% - 75px);
          left: calc(50% - 75px);
        
          background-color: rgba(255, 255, 255, 0.2);
        }
        
        .loader4:before {
          content: "";
          position: absolute;
          background-color: #fff;
          transform-origin: 100% 0%;
          /* ✅ 여기에 코드를 작성하세요 */
        }
        
        .loader4:after {
          content: "LOADING ...";
          color: #fff;
          font-family: Lato, "Helvetica Neue";
          font-weight: 200;
          font-size: 16px;
          position: absolute;
          width: 100%;
          height: 20px;
          line-height: 20px;
          left: 0;
          top: 0;
        }
        ```