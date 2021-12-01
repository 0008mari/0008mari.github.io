---
layout: post
title: "[C#] Question Marks"
date: 2021-12-01
categories: csharp
tags: "csharp"
---


# [C#] 물음표 연산자

아래와 같은 변수 선언문을 만났다.

```csharp
public string? Name { get; set; }
```

이것은 선언된 변수가 `Nullable`임을 의미한다.

`Nullable`이라는 용어의 의미는 아래 예제를 보면 알 수 있다.

```csharp
int i1=1; //ok
int i2=null; //not ok

int? i3=1; //ok
int? i4=null; //ok
```

또한 이렇게 표현해도 된다. 원래 아래와 같이 쓰는 것이 정식이고 물음표가 축약 형태이다.

```csharp
public Nullable<string> Name { get; set; }
```

## 비슷한 친구들

### 삼항연산자 `?`

```csharp
condition ? consequent : alternative
```

설명 생략

### null-conditional operator `?.`

```csharp
ction<TValue> myAction = null;

if (myAction != null)
{
  myAction(TValue);
}
```

위의 동작을 `?.`를 사용하면 아래와 같이 표기할 수 있다.

```csharp
myAction?.Invoke(TValue);
```

### null-coalescing operator `??`

왼쪽 피연산자의 값이 null이 아닌 경우 그것을 반환한다. 왼쪽 피연산자의 값이 null인 경우 오른쪽 피연산자를 평가하고 반환한다.

### null-coalescing assignment operator `??=`

Available in C# 8.0 and later, the null-coalescing assignment operator `??=` assigns the value of its right-hand operand to its left-hand operand only if the left-hand operand evaluates to `null`. The `??=` operator doesn't evaluate its right-hand operand if the left-hand operand evaluates to non-null.

## 참고문서

[c# - What is the purpose of a question mark after a type (for example: int? myVariable)? - Stack Overflow](https://stackoverflow.com/questions/2690866/what-is-the-purpose-of-a-question-mark-after-a-type-for-example-int-myvariabl)

[What does question mark and dot operator ?. mean in C# 6.0? - Stack Overflow](https://stackoverflow.com/questions/28352072/what-does-question-mark-and-dot-operator-mean-in-c-sharp-6-0)

[?? and ??= operators - C# reference | Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/null-coalescing-operator)

[Member access operators and expressions - C# reference | Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/member-access-operators#null-conditional-operators--and-)
