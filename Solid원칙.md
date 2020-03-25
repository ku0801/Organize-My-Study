# SOLID 원칙		

<h2>S .SRP(single Responsibility principle) 단일 책임원칙<h2>

-소프트웨어의 설계 부품(클래스 함수등은) 하나의 책임만을 가져야 함

여기서 책임이란?  기능 정로도 의미를 해석하면된다.

설계를 잘한 프로그램은 기본적으로 새로운 요구 사항과 프로그램 변경에 영향을 받는 부분이 적다.

만약 한 클래스가 수행할 수 있는 기능, 즉 책임이 많아진다. 
즉 클래스나 메소드는 하나의 역활만을 하며 한가지 책임만을 진다.
A 클래스가 존재하고 해당 A 클래스는 B클래스와 C클래스에서 사용된다.

ex)
class B{

  main(){
    A a = new A();
    a.getName();
  }
}

class C{
  main(){
    A a = new A();
    a.getId();
  }
}

A클래스는 B와 C에서 사용되지만 각각 사용되지만 각각 다른 메소드 호출하며 다른 역활을 하고있다.

이 경우 A클래스는 B에서 사용되는 역활 때문에 수정될 수도 있고 C에서 사용되는 역활 때문에 수정

될수도있다. 메소드도 소스를 보다보면 if문 같은 분기문으로 나누어 완전히 다른 로직으로 진행되는 경우를 흔히 볼 수있다. (이런 경우도 메소드를 나누는게 올바른 설계이다.)

O. OCP 개방폐쇄원칙
클래스나 모듈은 확장에 열려 있어야 하고 변경에는 닫혀 있어야 한다.
우선 OCP원칙을 위배되게 코드를 짜보고 OCP원칙을 지킨 코드와 비교를 해보자

자 컴퓨터 부팅이 시작 되구
public class BootStrap {
	public static void main(String[] args) {
		Computer computer = new Computer();
		computer.boot();
	}
}

부팅을 하면서 M사 키보드 연결을 맺으려 한다.
public class Computer{
	private final M_Keyboard = new M_Keyboard();
	public void boot(){
	M_Keyboard.connect();
	}
}
}
M사 키보드가 정상적으로 연결이 되면
public class M_KeyBoard{
	public void connect(){
	System.out.println("M사 키보드가 연결이 되었습니다.");
    }
}
2)예제
public class Bootstrap{
	public void main(String[] args){
		Com com =new Com;
		Com.setKeyboard(new M_Keyboard());
		computer.boot();
	}
}
이제 부팅하면서 키보드를 연결 시키려하면
public class Computer{
	private KeyBoard keyboard;
	public void setKeyborad(Keyboard keyboard){
		this.keyboard=keyboard;
	}
	public void boot(){
	System.out.println("부팅중");
	keyboard.connet();
	}
}
첫번째 코드
Computer 클래스의 멤버 변수에 Keyboard 인터페이스를 정의하고, setKeyboard 메소드를 통해 특정 제조사의 키보드 객체를 주입 받는다. 

이와 같이 인터페이스를 이용해 키보드 연결이라는 행위를 추상화함으로써 Keyboard 인터페이스를 구현한 어떠한 키보드 클래스도 주입 받을 수 있을 것이다.

즉, S사 키보드를 사용하고 싶을 때나 또는 L사 키보드를 사용하고 싶을 때 Computer 클래스를 수정할 필요 없이 외부에서 키보드 객체를 주입해 주기만 하면 되는 것이다.

결국 이를 통해 OCP 원칙중에 하나인 "변경에는 닫혀있다." 라는 원칙이 성립되는 것이다

두번째 코드
새롭게 개발된 소프트웨어를 탑재한 컴퓨터는 Keyboard 인터페이스를 구현한 키보드를 언제든지 사용할 수 있는 확장성을 얻게 되었다.

즉, Computer 클래스의 setKeyboard 메소드를 통해 사용하고자 하는 키보드를 주입시켜 다양한 키보드를 사용할 수 있게 된 것이다.

OCP 원칙의 "확장에는 열려있다."를 수용한다.

L. LSP 리스코프 치환 원칙

부모 클래스와 자식 클래스 사이의 행위가 일관성 있어야 한다는 의미로 LSP를 만족하면
프로그램에서 부모 ㅡ클래스와 인스턴스 대신에 자식 클래스의 인스턴스로 대체해도 
프로그램의 의미는 변화 되지 않는다.

예시1)
일반화 관계는 "is a kind of 관계" 에서 아이폰은 스마트폰이다 .따라서 부모 클래스는 스마트폰 자식클래스는 아이폰을 설정하는것은 당연한것
	-스마트 폰은 다른사람과 전화 및 메세지 가 가능하다
	-스마트 폰은 데이터 또는 와이파이를 통해 인터넷 사용 가능
	-스마트 폰은 앱 마켓을 통해 앱을 다운 받을 수 있다.
	
위 설명을 갤럭시 폰으로 대체 하면 아래와 같다.
	-아이폰은 다른사람과 전화와 메세지가 가능하다.
	-갤럭시 폰은 데이터 또는 와이파이를 이용해 인터넷을 사용할 수 있다.
	-스마트폰은 앱 마켓을 통해 앱을 다운 가능
	
부모 클래스(스마트폰)을 자식 클래스(아이폰)으로 바꿔도 전혀 문제가 없다.
LSP를 만족하는것 이렇게 부모 클래스와 자식 클래스 사이에 일관성이 있으려면 최소한 부모 클래스의 인스턴스가 실행 행위는 자식 클래스의 인스턴스도 일관성 있게 할 수 있어야 한다.

예시2)
public class Bag{
	private int price;
	public void setPrice(int price){
	this.price =price;
	}
	public int getPrice(){
	return price;
	}
}
여기 예제에서 Bag 클래스는 가격을 설정 조회 하는 기능이 있다 .
위 클래스는 "가격은 설정된 가격 그래도 조회 된다."라는 행위를 가지고 있다. 이런 경우
Bag 클래스의 행위를 손상하지 않고 일관성 있게 실행하는 클래스를 만들려면 가장 쉬운 
방법이 슈퍼 클래스에서 상속 받은 메소드들이 서브 클래스에 재정의 되지 않도록 하면 된다.

public class DiscountedBag extends Bag {
   private double discountedRate = 0;
   
   public void setDiscounted(double dc){
         discountedRate = dc;
   }
   public void applyDiscount(int price){
         super.setPrice(price-(int)(discountedRate * price));
   }

위 클래스는 할인된 가격을 계산하는 기능을 추가되어있고 상속 받은 메소드가 정의 되어있다.
Bag b1 = new Bag();               DiscountedBag b1 = new DiscoutedBag()
b1.setPrice(500);                     b1.setPrice(500);
sysout(b1);                            sysout(b1);

위 코드를 보면 Bag 클래스를 DiscountedBag로 바꿔도 실행 결과가 동일 즉 일관성이 유지
즉 LSP가 만족이 된다.

public class DiscountedBag extends Bag{
	private double discountedRate =0';
	public void setDiscounted(double dc){
	discountedRate =dc;
	}	
	public void setPrice(int price){
	super.setPrice(price-(int)(discountedRate) * price);
	}
}
만약 DiscountedBag 클래스를 위와 같이 만들면 실행 결과가 달라진다. 따라서, 일관성이 깨져 LSP를 만족하지 않고 피터 코드의 상속 규칙에서 "서브 클래스가 슈퍼 클래스의 책임을 무시하거나 재정의하지 않고 확장만 수행한다"라는 규칙에도 어긋난다. 이는 슈퍼 클래스의 메서드를 오버라이딩 하지 않는 것과 같다. 즉, 피터 코등의 상속 규칙을 지키는 것은 LSP를 만족시키는 하나의 방법이다.

I. ISP(인터페이스 분리 원칙)
어떤 클래스가 있고 그 클래스가 특정한 인터페이스를 사용하여 구현된다면 그 클래스는 반드시
그 인터페이스에 포함 되어있는 메소드를 구현 하도록 강제하는것

예제1)
Interface Baby{
	public void cry();
	
}
class CuteBaby implements Baby{
	public void cry(){
		System.out.println("으앙");
	}
}
class PrettyBaby implements Baby{
	publci void cry()
	{
	System.out.println("엉엉");
	}
}

원칙
	1. 어떤 클래스를 인터페이스를 사용하여 구현할 때 사용하지 않는 메소드를 가지고 있는 
	인터페이스에 의존하게 하지 말아야함
	
	2. 클래스가 사용하는기능 만 제공 하도록 인터페이스를 분리 하는것
	
	3. 하나의 일반적인 인터페이스보다는 여러개의 구체적인 인터페이스가 낫다

두개의 클래스가 필요하지 않는 행위를 하는 메소드를 구현해야하는 문제에 대해서
아래 예제의 코드를 비교해 보자

Interface Animal{
    public void walk();
    public void eat();
    public void fly();
    public void buy();
}
 
 
class Korean implements Animal{
    public void walk() {...}
    public void eat() {...}
    public void fly() {} // 필요 없음!
    public void buy() {...}
 
}
 
class Parrot implements Animal{
    public void walk() {...}    
    public void eat() {...}
    public void fly() {...}
    public void buy() {} // 필요 없음!
}
예제3)
이제 인터페이스를 더 세분화 하면 클래스에 필요한 메소드만 구현 가능
아래의 예제는 불필요한 메소드는 구현하지않고 필요한 메소드만 구현 해보자

Interface Animal{
    public void walk();
    public void eat();
}
 
Interface Person {
    public void buy();
}
 
Interface Bird {
    public void fly();
}
 
class Korean implements Animal, Person{
    public void walk() {...}
    public void eat() {...}
    public void buy() {...}
}
 
class Bird implements Animal, Bird{
    public void walk() {...}    
    public void eat() {...}
    public void fly() {...}
}


ISP의 이점
1. 클래스에 필요한 메소드만 선언 가능
2. 재사용성 이 높아진다
3.  용도가 명확한 인터페이스 제공 가능 

D. DIP 의존 역전 원칙

고차원 모듈은 저차원 모듈에 의존하면 안 된다. 이 두 모듈 모두 다른 추상화된 것에 의존해야 한다."

"추상화된 것은 구체적인 것에 의존하면 안된다. 구체정인 것이 추상화된 것에 의존해야 한다."

"자주 변경되는 구체 클래스에 의존하면 안된다."

자신보다 변하기 쉬운것에 의존 하면 안된다

자신보다 변하기 쉬운 것에 의존하던 것을 추상화된 인터페이스나 상위 클래스를 두어 변화기 쉬운 것에 영향받지 않게 하는 것이 의존 역전 원칙이다.

상위 클래스는 하위 클래스에 의존해서는 안된다. 하위 클래스가 상위 클래스에 의존을 해야지 반대로 의존한다는것 원칙에 위반된다.

예제1)


class Robot{

    override fun toString(): String {
        return "Robot"
    }
}

class Kid(private val robot: Robot) {

    fun play() {
        println("play toy : $robot")
    }
}
fun main() {

    val toy = Robot()
    val kid = Kid(toy)
    kid.play()
}
아이는 로봇이라는 장난감을 가지고 놀수있다 하지만 kid의 파라미터는 Robot으로 변하기
쉬운것에 의존 하고있기때문에 다른 장난감이 생기게되면 kid클래스를 새로 정의 해야한다.

before 예제 2)

open class Toy

class Robot: Toy() {

    override fun toString(): String {
        return "Robot"
    }
}

class Dinosaur: Toy() {

    override fun toString(): String {
        return "Dinosaur"
    }
}

class Kid(private val toy: Toy) {

    fun play() {
        println("play toy : $toy")
    }
}
fun main() {

    val robot = Robot()
    val Dinosaur = Dinosaur()

    //robot 과 dinosaur 를 선택해서 아이에게 줄 수 있다.
    val kid = Kid(robot)
    kid.play()
}

이번에는 장난감을 변하기 어려운 것 (Toy 클래스)에  의존함 으로서 문제를 해결했다.
이번에는 장난감을 변하기 어려운 것(Toy 클래스)에 의존함으로서 문제를 해결한 모습입니다. 이제는 새로운 장난감이 생겨도 Kid 클래스를 새로 정의해 주지 않아도 됩니다. 위 예제 코드를 보시면 DIP 또한 추상화된 것에 의존해야 된다는 것은 결국 변화에 열려있고 수정에는 닫혀있어야 되는 OCP 원칙과 비슷한 맥락인 것 같습니다.



