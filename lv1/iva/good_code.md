## 좋은 코드란 무엇일까?


### IF 문

*if 문은 조건을 기준으로 컴퓨터가 프로그램을 읽을 때 분기를 할 수 있는 기능을 제공한다.*

### IF 문은 좋지 않은 것인가?

성능 이슈는 없다.

### 그렇다면 왜 IF 문을 꺼려할까?

- 계속적인 if 문은 유지보수하기 어려운 코드로 이어질 수 있기 때문이다.
- 더욱이 else와 같이 쓰이면 그 가능성인 매우 커진다.
    - 물론 무조건적인 if 문이 좋지 않다고 말하는 것 또한 옳지 않다.
- if - else가 연속적이게 되면 향후 관련된 조건의 변경 사항이 일어날 경우 else를 새롭게 추가하여 변경 사항을 처리해줘야하는 상황이 쉽게 발생할 수 있다.
- 위 사항이 한, 두 곳이라면 상관 없겠지만 산발적으로 변경을 해줘야한다면 이는 유지보수하기 매우 어려워진다.
- if - else 문으로 분기가 된다는 것은 실행되는 것이 2개 이상으로 이어지기 때문에 단일 책임 원칙에 위반될 수 있는 여지가 생긴다.

---

### 좋은 코드란 무엇일까?

- 유지보수하기 쉬운 코드라고 할 수 있다.
- 유지보수하기 쉬운 코드란

    1. 누가 짰던 간에 코드를 분석하는데 어려움이 없는 읽기 쉬운 코드
    2. 변경이 일어날 가능성을 최대한 줄이고 유연하게 대처할 수 있는 코드

---

### 좋은 코드를 짜려면 어떻게 해야할까?

- 코드 컨벤션을 잘 지킨다.
- 유지보수 관점에서 코드를 설계하고 작성한다.

    ex) 누가 읽어도 무슨 일을 할 수 있는 메서드인지 명확히 이름에서 드러내도록 한다.

- 변경에 폐쇄적이고 확장에 열리도록 한다.
- 객체 지향적 설계를 준수한다.

---

### 객체 지향적 설계

- SOLID 원칙을 따른다.
    - SRP (단일 책임 원칙) : 하나의 클래스(메서드)는 하나의 책임을 가져야한다. 전혀 관련 없는 책임(일)을 맡게 되면 유지보수하기 어려운 코드로 이어진다.
    - OCP (개방 폐쇄 원칙) : 확장에는 열려있고(개방) 변경에는 닫혀있어야(폐쇄) 한다. 이는 SRP와 연관되어 변경사항에 대해 최대한 닫혀있되 관련된 책임을 지고 있는 클래스(메서드)만 찾으면 되는 형식으로 설계를 할 수 있다.
    - LSP (리스코프 치환 원칙) :
    - ISP (인터페이스 분리 원칙) :
    - DIP (의존관계 역전 원칙) :

- 객체간의 관계를 파악한다.
    - 런타임 시 객체들이 서로 어떻게 접근하는지에 대해 예상하고 그리는 것이 객체간의 관계를 결정하는 것이다.
    - 연관관계 : 어떤 한 객체에서 다른 객체로 빈번하게 가야되는 상황에서 그 경로를 명시적으로 정해놓을 필요가 있을 때 연관관계로 잡아 놓는다.
        - 협력을 위해 필요한 영구적인 탐색 구조

                class A {}
                
                class B {
                  private A a;		// A 객체를 영구적으로 딱 정해놓는 관계 -> 연관관계
                }
                
                // B 객체에서 A 객체를 찾아갈 수 있다. (연관관계의 특징)

    - 의존관계 : 한 객체가 다른 객체에게 접근할 필요가 있을 때, 그 상황이 빈번하게 일어나지 않고 일시적으로 접근만 하면 되는 상황이라면 의존관계로 잡아 놓는다.
        - 협력을 위해 일시적으로 필요한 의존성 (파라미터, 리턴타입, 지역변수)

                class A {}
                
                class B {
                  public A b(A a) {
                    return new A();			// A 객체를 b() 메서드안에서만 일시적으로 사용하고자 할 때
                  }											// 파라미터, 지역변수(직접 생성), 리턴타입 구조로 설정한다.
                }