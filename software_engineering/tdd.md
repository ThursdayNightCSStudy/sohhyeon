# TDD (Test Driven Development)

소프트웨어 개발 방법론 중의 하나로 테스트를 먼저 진행하고 개발하는 프로그래밍 방법을 말한다.

## 테스트 환경 구축
테스트 환경을 구현하기 위해서는 프레임워크를 사용하는데, 다음은 대표적으로 사용되는 프레임워크이다.

1.<a href="https://jestjs.io/">Jest</a>

Facebook으로 알려진 Meta에서 개발한 프레임워크로 Test-Runner, Assertion Library, Mocking Library 를 포함하는 자주 사용되는 대표적인 프레임워크이다. Mocha와는 다르게 다른 라이브러리에 대한 추가적인 의존성을 갖지 않는다. React 환경에서 주로 사용된다. 

Jest 이전에는 Mocha나 Jasmine을 Test Runner로 사용하고 Chai나 Expect와 같은 Test Matcher를 사용하고 Sinon, Testdouble 같은 Test Mock 라이브러리를 사용헸디.


2.<a href="https://mochajs.org/">Mocha</a>

다양한 Assertion library (should.js)를 사용할 수 있다. 단위 테스트 뿐만 아니라 통합 테스트도 유연하게 사용 가능하다.

Mocha는 Test runner로 써드파티 assertions, mocking, spying tool이 필요하다.



## TDD의 세가지 법칙

1. 실패하는 단위 테스트를 작성할 때까지 실제 코드를 작성하지 않는다.
2. 컴파일은 실패하지 않으면서 실행이 실패하는 정도로만 단위 테스트를 작성한다.
3. 현재 실패하는 테스트를 통과할 정도로만 실제 코드를 작성한다.


## TDD 개발 순서

1. `RED` : 실패하는 테스트를 작성한다.
2. `GREEN` : 테스트를 통과할 정도로만 코드를 작성한다.
3. `REFACTOR` : 리팩토링을 통해 코드를 정리한다.

- 장점
    - 개발자가 기대하는 기능의 동작에 관한 문서를 테스트 케이스가 제공한다.
    - 자동화 도구를 이용해 테스트 케이스를 단위 테스트로 사용할 수 있다.

- 단점
    - 테스트 케이스 설계에 대한 추가적인 시간이 필요하다.
    - 테스트 방향성, 프레임워크 선택 등 추가적인 학습 및 선택이 필요하다.

## 점수 계산 프로그램을 통한 TDD 예제

중간, 기말, 과제 점수를 통해 성적을 계산하는 간단한 프로그램을 만들어보자. 점수 총합 90점 이상은 A, 80점 이상은 B, 70점 이상은 C, 60점 이상은 D, 그 이하는 F로 계산한다.

아래의 코드는 `assertEquals`로 테스트를 진행하는 코드이다.
다음과 같이 작성한 경우, 실제 기능을 구현하기 전에 작성한 테스트 코드이므로 항상 실패한다. (RED)

```java
public class GradeTest {
    @Test
    public void scoreResult() {
        Score score = new Score(35, 25, 25);
        SimpleScoreStrategy scores = new SimpleScoreStrategy();
        String resultGrade = scores.computeGrade(score);

        assertEquals("B", resultGrade);
    }
}
```

테스트 코드에 맞춰서 코드 개발을 진행하자. (GREEN)

```java
// Score 클래스 구현
public class Score {
    private int mid;
    private int final;
    private int homework;

    public Score(int mid, int final, int homework) {
        this.mid = mid;
        this.final = final;
        this.homework = homework;
    }

    public int getMid() {
        return mid;
    }

    public int getFinal() {
        return final;
    }

    public int getHomework() {
        return homework;
    }
}
```

```java
// ScoreStrategy 인터페이스 구현
public interface ScoreStrategy {
    String computeGrade(Score score);
}
```

```java
// SimpleScoreStrategy 클래스 구현
public class SimpleScoreStrategy implements ScoreStrategy {
    public String computeGrade(Score score) {
        int totalScore = score.getMiddleScore() + score.getFinalScore() + score.getHomeworkScore();

        Stirng gradeResult = null;

        if (totalScore >= 90) {
            gradeResult = "A";
        } else if (totalScore >= 80) {
            gradeResult = "B";
        } else if (totalScore >= 70) {
            gradeResult = "C";
        } else if (totalScore >= 60) {
            gradeResult = "D";
        } else {
            gradeResult = "F";
        }

        return gradeResult;
    }
}
```

이후에 리팩토링을 통해 코드를 정리하면 된다! (REFACTOR)


### reference

- <a href="https://www.merixstudio.com/blog/mocha-vs-jest">Mocha vs. Jest: comparison of two testing tools for Node.js</a>