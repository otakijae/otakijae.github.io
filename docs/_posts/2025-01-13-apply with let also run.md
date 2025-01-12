---
layout: post
title: "Kotlin apply, with, let, also, run"
author: "otakijae"
tags: kotlin
excerpt_separator: <!--more-->
---

## Kotlin apply, with, let, also, run 은 언제 사용해야 하는가

- 간단하게 설명

- Kotlin의 `apply`, `with`, `let`, `also`, `run`은 **스코프 함수**로, 객체를 처리할 때 더 간결하고 읽기 쉬운 코드를 작성할 수 있도록 도와줍니다. 각각의 용도는 다음과 같습니다:
<!--more-->

------

### 1. **`apply`**

- **주로 객체 설정**에 사용.
- 객체를 초기화하거나 프로퍼티를 설정할 때 사용.
- **`this`를 암시적으로 참조**.

```
kotlin


코드 복사
val person = Person().apply {
    name = "Alice"
    age = 25
}
```

------

### 2. **`with`**

- **비슷한 작업을 한 객체에 대해 실행할 때** 사용.
- 함수 호출을 그룹화하고 싶을 때 사용.
- **`this`를 암시적으로 참조**, 결과값을 반환.

```
kotlin


코드 복사
val result = with(person) {
    println(name)
    println(age)
    "Completed"
}
```

------

### 3. **`let`**

- **nullable 객체 처리**에 주로 사용.
- **`it`으로 객체를 참조**.
- 새로운 컨텍스트에서 로직을 실행하고 결과를 반환.

```
kotlin


코드 복사
val name = person?.let {
    println(it.name)
    it.name.uppercase()
}
```

------

### 4. **`also`**

- **객체를 사용하면서 부가적인 작업**(로깅, 디버깅 등)을 수행할 때 사용.
- **`it`으로 객체를 참조**.

```
kotlin


코드 복사
val person = Person().also {
    println("Creating person: $it")
}
```

------

### 5. **`run`**

- **apply와 유사하지만 결과 값을 반환**.
- 객체 설정과 로직 실행을 한 번에 처리할 때 사용.
- **`this`를 암시적으로 참조**.

```
kotlin


코드 복사
val result = person.run {
    println(name)
    age += 1
    "Age incremented"
}
```



## 요약

| 함수    | 참조 방법 | 주요 용도                       | 반환값        |
| ------- | --------- | ------------------------------- | ------------- |
| `apply` | `this`    | 객체 설정                       | 객체 자체     |
| `with`  | `this`    | 동일 객체에 대해 여러 작업 실행 | 람다의 결과값 |
| `let`   | `it`      | Nullable 처리, 변환 및 사용     | 람다의 결과값 |
| `also`  | `it`      | 부가 작업 (로깅, 디버깅 등)     | 객체 자체     |
| `run`   | `this`    | 객체 설정 후 결과 반환          | 람다의 결과값 |

**선택 기준**: 작업의 목적(객체 설정, 변환, 부가 작업 등)에 따라 적절한 스코프 함수를 선택하세요.