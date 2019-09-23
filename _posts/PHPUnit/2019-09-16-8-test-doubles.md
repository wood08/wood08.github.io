---
title: "8. 테스트 더블 (test doubles)"
categories:
  - PHPUnit
tags:
  - PHPUnit, test
---

8. 테스트 더블
===

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
이 테스트더블오브젝트는 원래 오브젝트를 필요료 하는 모든 상황에 쓰는것이 가능합니다.

``createMock($type)`` 메소드는, 시정한 형태(인터페이스나 클래스)
의 테스트더블 오브젝트를 그 자리로 돌려줍니다.
테스트더블의 작성은, 기본적으로 모범형태(best practice defaults)에 따라 진행됩니다.
(원래 클래서의 ``__construct()`` 나 ``__clone()`` 는 실행하지 않는다.)
그리고, 테스트더블의 메소드에 넘겨받은 인수는 복제되지 않습니다.
디폴트와 다른 행동을 원하는 경우에는,
``getMockBuilder($type)`` 메소드를 사용해서 테스트더블 생성을 커스터마이즈 해야 합니다.

기본적으로, 원래 클래서의 모든 메소드가 치환되어,
(원래의 메소드는 부르지 않고) 단순히 ``null`` 을 돌려주는 더미를 구현합니다.
예를들자면, ``will($this->returnValue())`` 메소드를 쓰면,
더미가 불러질때 값을 돌려주도록 설정하는것이 가능합니다.

.. admonition:: 제한：final、private 또는 static 메소드

   ``final``, ``private`` 또는
   ``static`` 메소드를 stub 이나 mock 으로 만들수 없는것에 주의.
   PHPUnit 의 테스트더블 함수에서는 이것들을 무시하고, 원래 메소드의 기능을 그대로 유지합니다.
   단, ``static`` 메소드는 ``\PHPUnit\Framework\MockObject\BadMethodCallException``
   를 반환하는 메소드로 대처됩니다.

.. _test-doubles.stubs:

Stubs(스텁)
===

실제의 오브젝트를 교체해서,
설장한 무언가의 값을(옵션에서) 반환하는 테스트더블을
*Stubs* 하고 합니다.
*Stubs* 를 사용하면, 
「SUT 가 의존하고 있는 실제 컴포넌트를 교체해서,
SUT 의 입력을 간접적으로 컨트롤 하는것이 가능합니다.
이것으로, SUT 가 다른것을 실행하지 않는것을 강제할 수 있습니다.」

Example 8.2 에서, 스텁 메소드의 작성과 반환값의 설정 방법을 나타내고 있습니다.
우선, ``PHPUnit\Framework\TestCase`` 클래스의 
``createMock()`` 메소드를 사용하여 
``SomeClass`` 오브젝트의 스텁을 작성합니다(Example 8.1).
그 다음, PHPUnit 이 제공하는, 예를 들면 
Fluent Interface[https://martinfowler.com/bliki/FluentInterface.html] 
(흐르는듯한 인터페이스)를 사용하여 스텁의 동작을 설정 합니다.
간단하게 말하자면, 몇가지 임시 오브젝트를 작성해서,
그것을 연결시키는 작업이 필요없다는 것입니다.
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
    
.. admonition:: 제한： "method" 라는 이름의 메소드

    이 에가 제대로 작동하는것은, 원래 클래스에서 "method" 라는 이름의 메소드가 선언 되어 있지 않을때입니다.
    
    원래 클래스에 "method" 라는 이름의 메소드가 선언 되어있는 경우,
    ``$stub->expects($this->any())->method('doSomething')->willReturn('foo');`` 라고 해야 합니다.
    
무대 뒤(Behind the scenes) 에서 ``createMock()`` 메소드가 사용되었을때
PHPUnit 이 자동으로 요구하는 동작을 구현한 새로운 PHP 클래스를 생성합니다.

Example 8.3 에서 예를 나타내고 있습니다.
이것은, mock builder 의 흐르는닷한 인터페이스를 써서, 테스트더블의 작성방법을 설정하는 것입니다.
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