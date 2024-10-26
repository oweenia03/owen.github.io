---
layout: post
title: 파이썬 GUI 숫자야구게임
subtitle: Python toy project
excerpt_image: https://github.com/jeffreytse/jekyll-theme-yat/assets/9413601/2ed22d49-90b1-4f7e-8e8f-b77b21dee505
categories: project
tags: [Python, GUI] 
top: 3
---

![banner](https://github.com/jeffreytse/jekyll-theme-yat/assets/9413601/2ed22d49-90b1-4f7e-8e8f-b77b21dee505)


### 게임 규칙 ###

<!-- * **게임 규칙** -->

> 사용자에게서 3 이상 9 이하의 자릿수를 입력받고, 그 자릿수에 맞게 랜덤으로 생성된 숫자를 스트라이크 볼 개수를 통해 추리하도록 하는 프로그램이다. 
>
> 이때, 생성되는 각 자리 숫자는 1 ~ 9 사이의 자연수이고 중복되지 않는다.
  자릿수와 숫자 모두 맞추면 스트라이크, 자릿수는 틀렸지만 숫자는 맞는 경우 볼이다.
  모든 숫자를 자릿수에 맞게 맞추면 정답이다.
>
> 자릿수 입력 란에 -1 입력 시 프로그램 종료된다.

<!-- Paragraphs are separated by a blank line. -->

<!-- 2nd paragraph. *Italic*, **bold**, and `monospace`. Itemized lists
look like: -->
<br>

### 프로그램 설명 ###

1. 'Let’s play the game of numbers baseball.' 을 출력한다.  
2. 'Enter the num: '을 출력한 뒤, 사용자에게 3 ~ 5 사이의 자연수 num 을 입력 받는다. (input 활용)  
3. num 에 3 ~ 5 사이의 자연수가 아닌 값이 입력되면, 적절한 메시지 출력 후 num 을 다시 입력 받는다.  
4. num 에 -1 이 입력되면 프로그램은 종료된다. (-1 이 입력될 때까지 게임을 계속한다.)  
5. 랜덤으로 num 자릿수의 숫자를 생성하여 변수 ranNum 에 저장한다  
  ex) num 이 5 일 경우 자릿수가 5 인 숫자 12345 가 생성된다.  
  단, ranNum 을 생성할 때 각 자리의 숫자는 1 ~ 9 사이의 자연수여야 하고, 중복된 수가 있으면 안된다.  
  ex) ranNum 이 12234 일 경우, 2 가 중복되므로 다시 생성해야 한다  
6. 'Enter the num digits(inputNum): '을 출력한 뒤, 사용자에게 숫자 num 자리를 입력 받는다.  
  ex) num 이 5 일 경우, ‘Enter the 5 digits(inputNum): ’을 출력한 뒤, 사용자에게 숫자 5 자리를 입력 받는다.  
7. 게임 원리에 맞게 결과를 아래 형식으로 출력한다.  
  ex) [result] x Strike y Ball  
8. [6] & [7]을 정답을 추리할 때까지 반복한다.  
9. 정답을 맞춘 경우, 정답이라는 문구를 출력한 뒤 게임을 다시 시작한다  


<!-- Use 3 dashes for an em-dash. Use 2 dashes for ranges (ex., "it's all
in chapters 12--14"). Three dots ... will be converted to an ellipsis.
Unicode is supported. ☺ -->



<!-- 코드
------------ -->

### 코드 ###

[Download graphics.py](assets/files/graphics.py)


<!-- Here's a numbered list: -->
<!-- 
1. first item
 2. second item
 3. third item

Note again how the actual text starts at 4 columns in (4 characters
from the left side). Here's a code sample:

    # Let me re-iterate ...
    for i in 1 .. 10 { do-something(i) }

As you probably guessed, indented 4 spaces. By the way, instead of
indenting the block, you can use delimited blocks, if you like:

~~~
define foobar() {
    print "Welcome to flavor country!";
}
~~~

(which makes copying & pasting easier). You can optionally mark the
delimited block for Pandoc to syntax highlight it: 
-->

~~~python
from graphics import *  # graphics 모듈을 임포트
import random  # random 모듈을 임포트

#숫자 야구 게임을 구현하는 메인코드 클래스
class Baseball:
    
    #매개변수 num으로 자릿수를 입력받고 생성된 랜덤 숫자를 변수self.ranNum에 할당하는 함수
    def __init__(self, num): 
        self.num = num  # 매개변수 num의 값을 인스턴스 변수 self.num에 저장
        self.ranNum = self.generate_random_number() # generate_random_number 메서드를 호출해 생성된 랜덤 숫자를 변수에 할당함
        
    
    #고유한 자릿수를 가진 숫자를 중복되지 않게 랜덤으로 생성하고, 생성된 숫자를 반환하는 함수
    def generate_random_number(self):
        testNum = []  # 랜덤 숫자를 저장할 리스트로 testNum 생성함
        ranNum = ''  # 변수 ranNum에 랜덤 숫자를 문자열로 저장함
        
        while len(testNum) < self.num:  # 입력받은 자릿수보다 testNum 리스트의 길이가 작을 시 반복됨 
            com = random.randint(1, 9)  # 1부터 9까지의 랜덤 숫자 생성해 변수 com에 할당함
            
            if com not in testNum:  # 리스트 testNum에 변수 com에 해당하는 숫자가 없으면, 즉 숫자가 중복되지 않으면
                testNum.append(com)  # 숫자 com을 testNum 리스트에 추가
                ranNum += str(com)  # 숫자 com을 문자열로 변환하여 변수 ranNum에 저장함
        return ranNum  # 생성된 랜덤 숫자 ranNum을 반환함
    
    
    #사용자가 입력한 추측값에 대해 스트라이크와 볼을 계산하고 반환하는 함수
    def guess_number(self, guess): #매개변수 guess로 추측값을 입력받음
        strike, ball = 0, 0  # 스트라이크와 볼의 초기값을 0으로 설정
        
        for i in range(self.num):  # 입력된 자릿수만큼 반복
            if guess[i] == self.ranNum[i]:  # 사용자가 추측한 값의 i번째 자릿수와 생성된 랜덤숫자의 i번째 자릿수가 동일하면
                strike += 1  # 스트라이크 1 증가
                
            elif guess[i] in self.ranNum:  # 사용자가 추측한 값의 i번째 자릿수가 생성된 랜덤숫자에 존재하지만 자릿수가 맞지 않으면
                ball += 1  # 볼 1 증가
        return strike, ball  # 스트라이크와 볼의 수를 튜플로 반환


#숫자 야구 게임을 그래픽과 함께 실행하는 메인 함수
def main():
    print("Let's play the game of numbers baseball.")  # 게임 시작 시 콘솔창에 메시지 출력

    # 그래픽 창 생성 및 설정
    win = GraphWin("숫자 야구 게임", 400, 300)  # 400x300 크기의 그래픽 창 생성
    win.setCoords(0.0, 0.0, 4.0, 4.0)  # 좌표 시스템 설정 (0.0, 0.0)에서 (4.0, 4.0)으로

    # 초기 화면에 필요한 요소들 생성
    text_input = Text(Point(0.9, 3), "숫자 입력 (3 ~ 9) : ")  # 자릿수 입력 텍스트 생성
    text_input.draw(win)  # 그래픽 창에 그리기
    input_field = Entry(Point(2, 3), 9)  # 입력 필드 생성 (Entry 위젯의 시각적 너비 상 9자리까지 보임)
    input_field.setText("0")  # 초기 값을 "0"으로 설정
    input_field.draw(win)  # 그래픽 창에 그리기
    
    result_output = Text(Point(2, 2.3), "")  # 경고 메세지와 스트라이크 볼 개수를 출력하기 위한 텍스트 생성
    result_output.draw(win)  # 그래픽 창에 그리기
    
    message = Text(Point(2, 0.8), "-1 입력시 프로그램 종료됩니다")  # 프로그램 종료 안내 텍스트 생성
    message.draw(win)  # 그래픽 창에 그리기

    answer = Text(Point(3, 2), "")  # 정답 메시지 출력 위한 텍스트 생성
    answer.draw(win)  # 그래픽 창에 그리기
    
    gamestart = Text(Point(0.7, 2), "*\nLet's play\n the game of\n numbers baseball")  # 게임 시작 텍스트 생성
    gamestart.draw(win)  # 그래픽 창에 그리기
    
    # 랜덤 숫자 생성기 버튼
    button = Text(Point(2, 1.8), "랜덤 숫자 생성기")  # 버튼 텍스트 생성
    button.draw(win)  # 그래픽 창에 그리기
    Rectangle(Point(1.45, 1.5), Point(2.55, 2.1)).draw(win)  # 버튼 주위에 사각형 그려 버튼 모양을 만듦
    
    game = None  # 게임 객체 초기화
    
    while True:  # 무한 루프 시작
        click_point = win.getMouse()  # 사용자가 마우스 클릭한 위치 좌표 가져옴
        
        # 클릭한 위치가 "랜덤 숫자 생성기" 버튼의 영역 내에 있을 때
        if 1.45 <= click_point.getX() <= 2.55 and 1.5 <= click_point.getY() <= 2.1:  
            num_str = input_field.getText() #num_str 변수를 사용해 사용자 입력을 문자열로 가져옴
            print(f"Enter the num: {num_str}")  # 사용자가 입력한 자릿수를 콘솔에 출력
            
            try:
                num = int(num_str)  # 입력 필드에서 사용자가 입력한 값을 정수 num으로 변환
           
                if num == -1:  # 입력 값이 -1이면
                    print("Quit the game.") 
                    break  # 콘솔창에 종료 메시지 출력하고 프로그램 종료
                
                elif num < 3 or num >9:  # 입력 값이 3보다 작거나 9보다 크면
                    result_output.setText(f"숫자 3 ~ 9를 입력하세요")  # 경고 메시지 그래픽창에 출력
                    print("Enter the natural number between 3 and 9.\n") # 콘솔 창에 동일한 의미의 메시지 출력

                else:  # 입력 값이 유효하면
                    game = Baseball(num)  # 클래스 Baseball의 인스턴스 생성
                    result_output.setText("")  # 경고 메시지 그래픽 창에서 안 보이게 하기 위해 택스트 초기화함
                    text_input.setText("추측값 입력 : ")  # 자릿수 입력 텍스트에서 추측값 입력으로 텍스트 변경
                    button.setText("스트라이크-볼")  # "랜덤 숫자 생성기"에서 "스트라이크-볼"로 버튼 텍스트 변경
                    message.setText(f"{game.num}자리 입력")  # 프로그램 종료 안내 택스트에서 자릿수 안내 텍스트로 변경
                    answer.setText("")  # 정답 텍스트 안 보이게 하기 위해 텍스트 초기화
                    gamestart.setText("")  # 게임 시작 텍스트 초기화
                    
                    while True:  # 또 다른 무한 루프 시작
                        click_point = win.getMouse()  # 그래픽 창에서 마우스 클릭한 위치 좌표를 변수 click_point에 저장함
                        
                        if 1.45 <= click_point.getX() <= 2.55 and 1.5 <= click_point.getY() <= 2.1:  # 클릭한 위치가 버튼 영역 내에 있을 때
                            guess = input_field.getText()  # 입력 필드에서 사용자가 입력한 값을 변수 guess에 저장함
                            print(f"Enter the {game.num} digits(inputNum): {guess}") # 사용자가 입력한 추측값을 콘솔에 출력함 
                            # {game.num}은 게임에서 요구하는 숫자의 자릿수를 의미함
                            
                            #사용자가 입력한 값의 길이가 게임에서 요구하는 자릿수와 다르거나, 유효하지 않은 값을 입력한 경우
                            if len(guess) != game.num or not guess.isdigit(): 
                                result_output.setText(f"{game.num} 자리 숫자를 입력하세요.")  # 그래픽창에 경고 메시지 출력
                                continue # 반복문 처음으로 돌아가 추측값 재입력 받음
                            
                            strike, ball = game.guess_number(guess)  # 스트라이크와 볼 계산
                            result_output.setText(f"[결과] {strike} 스트라이크 {ball} 볼")  # 스트라이크 볼 개수 결과를 그래픽 창에 출력
                            print(f"[result] {strike} Strike {ball} Ball\n")  # 스트라이크 볼 개수 결과를 콘솔에 출력
                            
                            if strike == game.num:  # 정답을 맞추면, 즉 사용자가 입력한 숫자와 정답 숫자가 그 자릿수까지 모두 일치하면
                                break # 무한 루프 종료함
                            
                    # 정답을 맞췄을 때 초기 화면으로 돌아가기 위한 설정
                    answer.setText("정답!") #그래픽창에 "정답!" 표시
                    print("Congratulations, you got it!\n") #콘솔에 정답 메시지 출력함
                    
                    gamestart.setText("*\nLet's play\n the game of\n numbers baseball") #그래픽창에 게임 시작 문구 출력함
                    print("Let's play the game of numbers baseball.") #콘솔에 게임 시작 문구 출력함
                    
                    text_input.setText("숫자 입력 (3 ~ 9) : ") #그래픽창에 입력 문구 출력함
                    input_field.setText("0") #입력 필드 값 0으로 설정함
                    
                    result_output.setText("") #그래픽 창에 스트라이크 볼 개수 결과 문구 안 보이게 하기 위해 텍스트 초기화함
                    button.setText("랜덤 숫자 생성기") #"스트라이크-볼"에서 "랜덤 숫자 생성기"로 버튼 텍스트 변경함
                    message.setText("-1 입력시 프로그램 종료됩니다") #그래픽창에 프로그램 종료 안내 문구 표시함
                    
                    
            except ValueError: #사용자가 자릿수 입력에서 정수가 아닌 값을 입력 시 발생하는 ValueError 예외를 처리함
                result_output.setText("잘못된 입력입니다.") #에러 메시지 그래픽창에 출력함
                print("Invalid input.\n")  # 에러 메시지를 콘솔에 출력
    
    win.close()  # 그래픽 창 닫기


main()  # 메인 함수 실행
~~~



### 결과 ###

![example image](/assets/images/1.jpg "An exemplary image")
<br>
![example image](/assets/images/2.jpg "An exemplary image")



<!-- 1. First, get these ingredients:

      * carrots
      * celery
      * lentils

 2. Boil some water.

 3. Dump everything in the pot and follow
    this algorithm:

        find wooden spoon
        uncover pot
        stir
        cover pot
        balance wooden spoon precariously on pot handle
        wait 10 minutes
        goto first step (or shut off burner when done)

    Do not bump wooden spoon or it will fall.

Notice again how text always lines up on 4-space indents (including
that last line which continues item 3 above).

Here's a link to [a website](http://foo.bar), to a [local
doc](local-doc.html), and to a [section heading in the current
doc](#an-h2-header). Here's a footnote [^1].

[^1]: Some footnote text.

Tables can look like this:

Name           Size  Material      Color
------------- -----  ------------  ------------
All Business      9  leather       brown
Roundabout       10  hemp canvas   natural
Cinderella       11  glass         transparent

Table: Shoes sizes, materials, and colors.

(The above is the caption for the table.) Pandoc also supports
multi-line tables:

--------  -----------------------
Keyword   Text
--------  -----------------------
red       Sunsets, apples, and
          other red or reddish
          things.

green     Leaves, grass, frogs
          and other things it's
          not easy being.
--------  -----------------------

A horizontal rule follows.

***

Here's a definition list:

apples
  : Good for making applesauce.

oranges
  : Citrus!

tomatoes
  : There's no "e" in tomatoe.

Again, text is indented 4 spaces. (Put a blank line between each
term and  its definition to spread things out more.)

Here's a "line block" (note how whitespace is honored):

| Line one
|   Line too
| Line tree

and images can be specified like so:

![example image](https://user-images.githubusercontent.com/9413601/123900693-1d9ebd00-d99c-11eb-8e9e-cf7879187606.png "An exemplary image")

Inline math equation: $\omega = d\phi / dt$. Display
math should get its own line like so:

$$I = \int \rho R^{2} dV$$

And note that you can backslash-escape any punctuation characters
which you wish to be displayed literally, ex.: \`foo\`, \*bar\*, etc. 
-->
