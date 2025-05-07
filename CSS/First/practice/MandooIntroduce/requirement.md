## 요구사항

- html에서 실습한 만두 소개 웹페이지 html을 아래와 같이 수정하자.
    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    
        <link rel="stylesheet" href="./reset.css" />
        <link rel="stylesheet" href="./mandoo.css" />
        <title>Document</title>
      </head>
      <body>
        <h2>고양이 이름이 만두라니</h2>
    
        <section>
          <h2>만두 소개</h2>
          <p class="mandoo-intro">
            만두는 2024년 2월 27일생으로<br />
            이제 2살된 사고뭉치면서 애교쟁이인<br />
            근데 가끔은 장난친다고 자꾸 물어서<br />
            나도 같이 물어버릴까 고민하기도 하는<br />
            그런 귀염둥이 고양이이자 가끔은 사람같은 고양이랍니다.
          </p>
        </section>
    
        <section>
          <h2>만두의 사진을 누르면 네이버로 이동합니다.</h2>
          <a href="https://www.naver.com" target="_blank" rel="noopener noreferrer">
            <img src="./mandoo.jpg" alt="만두 사진" width="300" />
          </a>
        </section>
    
        <section>
          <h2>만두 동생 이름 추천해주세요.</h2>
          <input placeholder="만두 동생 이름을 적어주세요" class="recommend-name" />
        </section>
    
        <section>
          <h2>만두 동생 성별을 선택해주세요.</h2>
          <select>
            <option value="1">딸</option>
            <option value="2">아들</option>
          </select>
        </section>
      </body>
    </html>
    
    ```
- body 에 안쪽 여백 40px 적용하기
- “고양이 이름이 만두라니” h2 는 폰트 사이즈 30px, 굵기는 bold
- section 은 width 50%, 바깥 여백 top&bottom만 10px, 안쪽 여백은 20px, 모서리 둥글기는 10px, 배경색은 lightcyan
- section 안에 있는 h2 는 폰트 사이즈 20px, 바깥 여백 bottom 10px
- “만두 소개” 부분에 있는 p 태그에 명시된 class 명을 활용하여 폰트 사이즈 16px, 줄 간격은 20px
- “만두 동생 이름 추천해주세요” 부분에 있는 input 태그는 width 100%, height 50px, 테두리 선은 없애기, 폰트 사이즈 18px
    - placeholder 스타일은 폰트 사이즈 18px, 글씨 색깔은 gray 사용해주세요.
    - input focus 했을 경우 outline은 none, 테두리 선은 2px 실선 빨간색으로 해주세요.