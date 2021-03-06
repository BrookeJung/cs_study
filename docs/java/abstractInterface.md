# 추상클래스 _vs_ 인터페이스
	- 모두 추상 메소드를 가지고 인스턴스화 할 수 없다.

# 추상클래스
`추상` 이란 '여러 사물이나 개념에서 공통되는 특성이나 속성을 추출하여 파악하는 작용' 이다.
 - `추상 클래스`란 다른 클래스들의 공통이 되는 변수나 메서드의 이름과 형태만 기술하고 구체적인 내용이 없는 클래스다.
 - 각 클래스가 상속받을 수 있는 클래스는 최대 1 개다. (단일 상속)
 - 다른 클래스의 템플릿으로 사용된다.

ex)
개/고양이 클래스를 만든다고 할때, 모두 동물로 '소리 내어 운다' 는 공통점이 있다.
이때, 동물에 관한 추상 클래스를 만들어 공통 행동인 'cry' 를 메서드로 적어두면,
개 클래스 , 고양이 클래스는 추상 클래스를 상속하여 'cry'메서드에 개와 고양이가 어떻게 우는지만 다시 정의하면 된다.
```
// 구체적인 내용없이 공통점만 뽑아, 객체를 정의/생성하는 툴인 Animal이라는 클래스를 만든다.  
abstract class Animal { 
  
   //구체적인 내용 없이 공통점만 뽑아 , cry 메서드를 선언한다. 
  abstract void cry();
  
  }
```

```
//Animal 클래스를 확장(상속)하여 Dog 클래스를 만든다. 
//이때 추상클래스를 상속받은 클래스를 서브클래스(자식클래스)라 하고 - Dog , Cat
//상속을 해주는 클래스는 슈퍼클래스(부모클래스) 라 한다. - Animal
class Dog extends Animal {
  void cry(){
   //상속받은 메서드를 구체화한다.
       sout("왈왈");  }
       }
       
class Cat extends Animal {
  void cry(){
      sout("야옹");  }
      }
```
## 추상클래스의 단점
- 상속이 적합한지는 상관없이 무조건 상속 계층이 발생한다.
- 서브 클래스에서는 슈퍼 클래스에 의존하게 되는데, 슈퍼 클래스가 변경 없이 유지된다는 보장이 없기 때문에 의도치 않게 서브 클래스에 문제가 발생할 수 있다.
> 컴포지션으로 해결가능 . 컴포지션이란 슈퍼클래스의 인스턴스를 참조하는 private 필드를 서브 클래스에 주는 설계 방식. 

## 추상클래스의 사용
- 여러개의 가까운 클래스들 (is-a 관계가 형성될) 사이에 동일한 코드를 공유해서 사용하고 싶을때.
- 추상클래스를 상속한 클래스들이 많은 공통 메소드들과 필드와 public 보다 다양한 접근 제어자에 의해 사용하고 싶을때.
- non-static 과 non-final 필드를 선언하고 싶을때.  결과적으로 객체들의 상태를 메소드에서 접근하고 수정 할 수 있게 된다.

# 인터페이스
`interface` 는 '결합부' 라는 뜻으로, 서로 다른 두 장치나 사람 등을 이어주는 부분을 의미한다.
ex) 휴대폰을 조작하기 위해 화면을 누르면 휴대폰 화면이 사람과 핸드폰간의 인터페이스가 된다.
- 자바에서 인터페이스는 클래스와 외부 세계(ex.개발자, 다른 클래스)를 이어주는 역할을 한다.
- 인터페이스는 내부에 추상메서드를 가지고 있고, 인터페이스를 받은 클래스에서는 해당 메서드를 오버라이딩(overriding) 으로 재정의 하여 사용한다.
- 메서드의 선언과 구현을 분리할 수 있어 인터페이스를 상속받아 메서드를 구현하는 클래스와 그 메서드를 호출하는 클래스를 서로 독립적으로 개발하거나 관리할 수 있다.
- 자바의 클래스는 여러 개의 인터페이스로부터 메서드를 받아올 수 있다. (다중상속)
- 인터페이스를 받아 클래스를 만들때는 implements 를 사용하고 , 여러 개의 인터페이스를 상속할 경우 콤마 (,) 를 사용해 인터페이스 명을 구분한다. 상속을 위해 extends 와 같이 쓰일 경우엔 항상 extends 가 implements 보다 먼저 와야 한다.
ex)
```
interface Money{ 
  abstract void give(int money, String date);  
  abstract void receive(int money,String date);
  }
```

```
class Citizen extends Person implements Money{  
  @Override
  public void give(int money, String date){     
        sout(date+": - "+money);
    }
  @Override  
  public void receive(int money,String date){
        sout(date+": + "+money);
    }
  }
```

> java1.5 에서 나온 @Override 어노테이션은 생략해도 되지만 일종의 재정의를 위한 안전장치라고 생각하면된다. 인터페이스로부터 상속받은 메서드를 재정의 하지 않으면 컴파일시 오류가 발생한다.

## 인터페이스의 사용
- 크게 상관없는(is-a 정도는 아닌 has-a 정도인) 클래스들이 인터페이스를 구현( java8 부터는 구현된 것을 사용도 포함)해야 할 필요가 있을때. 예를들어 Comparable and Cloneable
- 특정 데이터타입의 행위를 특별하게 구현하길 원할때 그러나 누가 그것의 행위를 구현 했는지에 대한 관심은 없을때 
- 다중 구현상속의 이점을 누려야 할때 

## 추상클래스와 인터페이스의 차이점
추상 클래스|	인터페이스
---|---
 추상 메소드 와 비추 상 메소드를 가질 수 있다.	|추상 메소드 만 가질 수 있다 . Java 8부터 기본 및 정적 메소드 도 가질 수 있다.
 단일상속|	 다중 상속
 final, non-final, static , non-static 변수들을 가질 수 있다 .|	static , final 변수들만 가질 수 있다.
 abstract 키워드로 선언한다.|	interface 키워드로 선언한다.
 키워드 "extends"를 사용하여 추상 클래스 를 상속 할 수 있다.|	키워드 "implements"를 사용하여 상속 할 수 있다.
 추상클래스는 public, private, protected 등과 같은 클래스 멤버를 가질 수 있다.|	인터페이스의 멤버는 기본적으로 public이다.
 예 :	|예 :
public abstract class Shape {|	public interface Drawable {
public abstract void draw ();|	void draw ();
}|	}

### 정리
- 상속보다는 위임을 사용
- 다형성을 위한 것이라면 클래스 상속보다는 인터페이스를 구현

변하지 않는 구조에서 상속을 사용하면 중복 코드를 제거하고 깔끔하게 코드를 작성할 수 있지만, 변화가 발생하는 순간 상속 구조는 깨지기 쉽다.

상속은 기본적으로 Is-A 관계가 확실하고, 설계 이후에 변화가 없는 곳에서 사용해야 한다. 하지만 현실은 설계 이후에도 기능 변화가 비일비재 하다. 그래서 대부분 인터페이스를 사용한다.



[참고](https://www.javatpoint.com/difference-between-abstract-class-and-interface)
