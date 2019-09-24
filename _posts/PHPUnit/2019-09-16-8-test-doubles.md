---
title: "8. 테스트 더블 (test doubles)"
categories:
  - PHPUnit
tags:
  - PHPUnit, test
---

# 8. 테스트 더블

Gerard Meszaros 은, 테스트 더블의 개념을 Meszaros2007 에서 이렇게 말하고 있다.

    *Gerard Meszaros*:

    Sometimes it is just plain hard to test the system under test (SUT)
    because it depends on other components that cannot be used in the test
    environment. This could be because they aren't available, they will not
    return the results needed for the test or because executing them would
    have undesirable side effects. In other cases, our test strategy requires
    us to have more control or visibility of the internal behavior of the SUT.

    \- 테스트 대상 시스템(SUT:system under test)을 
    테스트를 하는 것은, 때로는 매우 힘들다. 왜냐하면, 
    시스템이 다른 컴포넌트에 의존하고, 
    그 컴포넌트를 테스트 환경에서 이용할 수 없을 수도 있기 때문입니다. 
    애초에 이용불가이거나 테스트에서 필요한 결과를 주지 않거나, 
    또는 바르지 않은 부작용이 있거나 합니다. 
    이 외의 경우에도, 테스트 환경의 내부적인 활동을 제대로 제어해서 
    눈에 보이도록 할 필요가 있습니다.

    When we are writing a test in which we cannot (or chose not to) use a real
    depended-on component (DOC), we can replace it with a Test Double. The
    Test Double doesn't have to behave exactly like the real DOC; it merely
    has to provide the same API as the real one so that the SUT thinks it is
    the real one!

    \- 실제로 의존하는 컴포넌트(DOC: depended-on component) 
    를 쓰지 않는 테스트를 만드는 경우에는, 그것을 테스트 더블로 치환할 수 있습니다. 
    테스트 더블은, 반드시 실제 DOC 와 똑같은 행동을 할 필요는 없습니다. 
    단순히 실제와 같은 API 를 제공하고, 
    SUT 에게 '이게 진짜다!' 라고 생각하게 만드는걸로 충분합니다.
    
PHPUnit 의 ``createMock($type)`` 메소드나 ``getMockBuilder($type)`` 메소드를 사용하면 
지정한 원래 인터페이스(또는 원래 클래스) 테스트더블로서 행동할 오브젝트를 자동으로 생성하는게 가능합니다.
이 테스트더블 오브젝트는 원래 오브젝트를 필요료 하는 모든 상황에 쓰는것이 가능합니다.

``createMock($type)`` 메소드는, 지정한 형태(인터페이스나 클래스) 의 
테스트더블 오브젝트를 그 자리로 돌려줍니다.
테스트더블의 작성은, 기본적으로 모범형태(best practice defaults)에 따라 진행됩니다.
(원래 클래스의 ``__construct()`` 나 ``__clone()`` 는 실행하지 않는다.)
그리고, 테스트더블의 메소드에 넘겨받은 인수는 복제되지 않습니다.
디폴트와 다른 행동을 원하는 경우에는,
``getMockBuilder($type)`` 메소드를 사용해서 테스트더블 생성을 커스터마이즈 해야 합니다.

기본적으로, 원래 클래스의 모든 메소드가 치환되어,
(원래의 메소드는 부르지 않고) 단순히 ``null`` 을 돌려주는 더미를 구현합니다.
예를들자면, ``will($this->returnValue())`` 메소드를 쓰면,
더미구현을 호출할때 값을 돌려주도록 설정하는것이 가능합니다.

> ### 제한：final, private 또는 static 메소드
>   ``final``, ``private`` 또는 ``static`` 메소드를 stub 이나 mock 으로 만들수 없는것에 주의.
   PHPUnit 의 테스트더블 기능에서는 이것들을 무시하고, 원래 메소드의 동작을 그대로 유지합니다.
   단, ``static`` 메소드는 ``\PHPUnit\Framework\MockObject\BadMethodCallException``
   을 throw 하는 메소드로 대처됩니다.

# Stubs(스텁)

실제의 오브젝트를 교체해서, 구현한 무언가의 값을(옵션으로) 반환하는 테스트더블을 *Stubs* 라고 합니다. 
*Stubs* 를 사용하면, 
「SUT 가 의존하고 있는 실제 컴포넌트를 교체해서,
SUT 의 입력을 간접적으로 컨트롤 하는것이 가능합니다.
이것으로, SUT 가 다른것을 실행하지 않는것을 강제할 수 있습니다.」

Example 8.2 에서, 스텁 메소드의 작성과 반환값의 설정 방법을 나타내고 있습니다.
우선, ``PHPUnit\Framework\TestCase`` 클래스의 
``createMock()`` 메소드를 사용하여 
``SomeClass`` 오브젝트의 스텁을 작성합니다(Example 8.1).
그 다음, PHPUnit 이 제공하는, 예를 들면 
[Fluent Interface](https://martinfowler.com/bliki/FluentInterface.html) (흐르는듯한 인터페이스)를 사용하여 스텁의 동작을 설정 합니다.
간단하게 말하자면, 몇가지 임시 오브젝트를 작성해서, 그것을 연결시키는 작업이 필요없다는 것입니다.
그 대신, 예처럼 메소드 호출을 연동합니다.
이 방법이, 보다 읽기 편한 '흐르는듯한' 코드가 됩니다.

Example 8.1 스텁을 만들고싶은 클래스

    <?php
    class SomeClass
    {
        public function doSomething()
        {
            // 뭔가를 한다
        }
    }
    
Example 8.2 메소드에 고정값을 반환하는 스텁

    <?php
    use PHPUnit\Framework\TestCase;
    
    class StubTest extends TestCase
    {
        public function testStub()
        {
            // SomeClass 클래스의 스텁을 작성한다.
            $stub = $this->createMock(SomeClass::class);
    
            // 스텁을 설정한다.
            $stub->method('doSomething')
                 ->willReturn('foo');
    
            // $stub->doSomething() 을 호출하면
            // 'foo' 를 반환하도록 한다.
            $this->assertSame('foo', $stub->doSomething());
        }
    }
    
> ### admonition:: 제한： "method" 라는 이름의 메소드
>이 에가 제대로 작동하는것은, 원래 클래스에서 "method" 라는 이름의 메소드가 선언 되어 있지 않을때입니다.
원래 클래스에 "method" 라는 이름의 메소드가 선언 되어있는 경우,
``$stub->expects($this->any())->method('doSomething')->willReturn('foo');`` 라고 해야 합니다.
    
무대 뒤(Behind the scenes) 에서 ``createMock()`` 메소드가 사용되었을때
PHPUnit 이 자동으로 요구하는 동작을 구현한 새로운 PHP 클래스를 생성합니다.

Example 8.3 에서 예를 나타내고 있습니다.
이것은, mock builder 의 흐르는듯한 인터페이스를 써서, 테스트더블의 작성방법을 설정하는 것입니다.
이 테스트더블로 사용하는 설정은, ``createMock()`` 가 디폴트로 사용되는 모범형태(best practice)와 동일합니다.

Example 8.3 mock builder API 를 사용하여, 생성된 테스트더블 클래스 변경

    <?php
    use PHPUnit\Framework\TestCase;
    
    class StubTest extends TestCase
    {
        public function testStub()
        {
            // SomeClass 클래스의 스텁을 작성한다.
            $stub = $this->getMockBuilder(SomeClass::class)
                         ->disableOriginalConstructor()
                         ->disableOriginalClone()
                         ->disableArgumentCloning()
                         ->disallowMockingUnknownTypes()
                         ->getMock();
    
            // 스텁 설정을 한다.
            $stub->method('doSomething')
                 ->willReturn('foo');
    
            // $stub->doSomething() 을 호출하면
            // 'foo' 를 반환하도록 한다.
            $this->assertSame('foo', $stub->doSomething());
        }
    }
    
여기까지의 예에서는 ``willReturn($value)`` 를 써서 심플하게 값을 반환해줬습니다.
이 구문은 ``will($this->returnValue($value))`` 와 같은 의미입니다.
이 긴 구문 검증으로, 보다 복잡한 동작을 하는 스텁을 만들수 있습니다.

때로는, 메소드를 호출할때의 인수 하나를(그대로) 스텁 메소드 호출의 반환값으로 하고 싶을때가 있습니다.
Example 8.4 는, ``returnValue()`` 대신 ``returnArgument()`` 를 써서 이걸 구현하는 예 입니다.

Example 8.4 메소드의 인수 중 하나를 돌려주는 스텁

    <?php
    use PHPUnit\Framework\TestCase;
    
    class StubTest extends TestCase
    {
        public function testReturnArgumentStub()
        {
            // SomeClass 클래스의 스텁을 작성한다.
            $stub = $this->createMock(SomeClass::class);
    
            // 스텁을 설정한다.
            $stub->method('doSomething')
                 ->will($this->returnArgument(0));
    
            // $stub->doSomething('foo') 는 'foo' 를 돌려준다.
            $this->assertSame('foo', $stub->doSomething('foo'));
    
            // $stub->doSomething('bar') 는 'bar' 를 돌려준다.
            $this->assertSame('bar', $stub->doSomething('bar'));
        }
    }
    
흐르는듯한 인터페이스를 테스트 할 때는, 
스텁 메소드가 자기 자신을 반환하도록 하면 편리합니다. 
Example 8.5  ``returnSelf()`` 를 사용하여 이걸 구현하는 예 입니다.

Example 8.5 스텁 오브젝트의 참조를 반환하는 메소드

    <?php
    use PHPUnit\Framework\TestCase;
    
    class StubTest extends TestCase
    {
        public function testReturnSelf()
        {
            // SomeClass 클래스의 스텁을 작성한다.
            $stub = $this->createMock(SomeClass::class);
    
            // 스텁을 설정한다.
            $stub->method('doSomething')
                 ->will($this->returnSelf());
    
            // $stub->doSomething() 는 $stub 을 반환한다.
            $this->assertSame($stub, $stub->doSomething());
        }
    }
    
스텁 메소드를 호출한 결과로, 정의한 인수 목록에 맞춰서 다른 값을 돌려주지 않으면 안될때가 있습니다. 
``returnValueMap()`` 을 사용하면, 맵을 만들어서 인수와 관계를 만들어서,
그것을 반환값으로 대응시키는것이 가능합니다.
Example 8.6 을 참조해주세요.

Example 8.6 메소드에 맵에서 값을 반환하는 스텁

    <?php
    use PHPUnit\Framework\TestCase;
    
    class StubTest extends TestCase
    {
        public function testReturnValueMapStub()
        {
            // SomeClass 클래스를 작상한다.
            $stub = $this->createMock(SomeClass::class);
    
            // 값을 돌려주기위해, 인수의 맵을 만든다.
            $map = [
                ['a', 'b', 'c', 'd'],
                ['e', 'f', 'g', 'h']
            ];
    
            // 스텁을 설정한다.
            $stub->method('doSomething')
                 ->will($this->returnValueMap($map));
    
            // $stub->doSomething() 는, 전달한 인수에 다른 값을 반환한다.
            $this->assertSame('d', $stub->doSomething('a', 'b', 'c'));
            $this->assertSame('h', $stub->doSomething('e', 'f', 'g'));
        }
    }
    
스텁메소드를 호출한 결과로 고정값(``returnValue()`` 를 참조해주세요.)이나 
(변하지 않는) 인수(``returnArgument()`` 를 참고해주세요.)가 아닌 계산한 값을 반환하는 경우에는, 
``returnCallback()`` 을 사용합니다.
이것은 스텁메소드에서 콜백 함수나 메소드의 결과를 반환합니다.
Example 8.7 을 참조해주세요.

Example 8.7 메소드의 콜백에서 값을 반환하는 스텁

    <?php
    use PHPUnit\Framework\TestCase;
    
    class StubTest extends TestCase
    {
        public function testReturnCallbackStub()
        {
            // SomeClass 클래스의 스텁을 작성한다.
            $stub = $this->createMock(SomeClass::class);
    
            // 스텁 설정을 한다.
            $stub->method('doSomething')
                 ->will($this->returnCallback('str_rot13'));
    
            // $stub->doSomething($argument) 는 str_rot13($argument) 를 반환한다.
            $this->assertSame('fbzrguvat', $stub->doSomething('something'));
        }
    }
    
콜백메소드를 설정하는 것보다 좀 더 심플한 방법으로, 
원하는 값을 반환하는 리스트를 지정하는 것이 가능합니다. 
이 경우 사용하는 것은 ``onConsecutiveCalls()`` 메소드 입니다.
Example 8.8 의 예를 참조해주세요.

Example 8.8 메소드에 리스트로 지정한 값을 순서대로 반환하는 스텁

    <?php
    use PHPUnit\Framework\TestCase;
    
    class StubTest extends TestCase
    {
        public function testOnConsecutiveCallsStub()
        {
            // SomeClass 클래스의 스텁을 작성한다.
            $stub = $this->createMock(SomeClass::class);
    
            // 스텁 설정
            $stub->method('doSomething')
                 ->will($this->onConsecutiveCalls(2, 3, 5, 7));
    
            // $stub->doSomething() 는 매번 다른값을 반환한다.
            $this->assertSame(2, $stub->doSomething());
            $this->assertSame(3, $stub->doSomething());
            $this->assertSame(5, $stub->doSomething());
        }
    }

값을 반환하는 것이 아니라, 스텁메소드에서 예외를 발생시키는 경우가 있습니다. 
Example 8.9의 ``throwException()`` 로 이걸 발생시키는 방법을 지정합니다.

Example 8.9 메소드의 예외를 throw 하는 스텁

    <?php
    use PHPUnit\Framework\TestCase;

    class StubTest extends TestCase
    {
        public function testThrowExceptionStub()
        {
            // SomeClass 클래스의 스텁을 작성
            $stub = $this->createMock(SomeClass::class);

            // 스텁 설정
            $stub->method('doSomething')
                 ->will($this->throwException(new Exception));

            // $stub->doSomething() 는 예외를 throw 한다.
            $stub->doSomething();
        }
    }

그리고, 스텁을 사용하는 것으로, 보다 좋은 설계를 하는것이 가능해집니다. 
이곳 저곳에서 이용되는 리소스를 단일 창구(façade : 파사드)를 통해 엑세스 하게 하는것을 통해, 
이걸 간단하게 스텁으로 치환할 수 있게 됩니다.
예를 들면, 데이터베이스의 접속코드를 이곳 저곳 넣는것이 아니라, 
그 대신에 ``IDatabase`` 인터페이스를 구현한 단일 ``Database`` 오브젝트를 이용하도록 합니다. 
그렇게하면 ``IDatabase`` 를 구현한 스텁을 작성하는 것으로, 
그것을 테스트에 사용하게 되는 것입니다. 
동시에, 테스트를 행할때 스텁 데이터베이스를 이용하나, 실제 데이터베이스를 사용하나 를 선택 가능하게 합니다.
즉 개발시에는 로컬환경에서 테스트를 하고, 통합 테스트 때에는 실제 데이터베이스로 테스트하도록 하는것이 가능해집니다.

스텁화 하지않으면 안되는 기능은, 대게 동일 오브젝트 내에서 밀접하게 결합해 있습니다. 
이 기능을 하나로 결합한 인터페이스로 정리하는 것으로, 
시스템의 다른 부분과 결합을 느슨하게 할 수 있습니다.

