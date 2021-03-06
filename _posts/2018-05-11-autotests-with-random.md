---
title: Мой взгляд на рандом в автотестах 
date: 2018-05-10
categories:
- Разное
tags:
- java
- random
---
По мотивам [поста Темы](http://artkoshelev.github.io/posts/random-test-data). 
**Поделюсь своим опытом.**

# Когда стоит и не стоит использовать рандом в автотестах
Для начала когда стоит.
1. Когда тестовые данные отображают какой-то класс эквивалентности. 
Например, допустим нам нужно проверить валидацию тестового поля на длину входящей строки. Здесь, можно использовать рандом и написать для граничного значения:
```java
getRandomString(MAX_LENGTH);
```
Для строки длиной больше максимально допустимой:
```java
getRandomString(MAX_LENGTH + 1);
```
Здесь `MAX_LENGTH` - максимальная допустимая длина строки.
В этом случае мы в кейс закладываем больше логики, что делает его более понятным. При этом автотест будет намного наглядней, чем если бы мы не использовали рандом, а захаркодили определенную строку.

2. Когда рандомные значения никак не влияют на тестовую логику. 
При формировании тестовых данных, нам порой не важно какими они будут, а важно только их наличие.
В этом случае их можно также рандомить. 

В остальных случаях лучше избегать рандома. Также следуют избегать рандома для слишком сложных структур данных и объектов, для которых при использовании есть множества ограничений. Не стоит использовать рандом и для формирования уникальных сущностей: для них подойдет системное время (как писал Тема). 

# Почему рандом это хорошо
Правильное использование рандома в тесте помогает сделать код более наглядным и заодно избавиться от магических значений в коде.

# Почему рандом это плохо
Неправильное использование рандома ведет к ошибкам, которые очень тяжело отловить. Также неправильно использование при формировании тестовых данных может негативно сказываться на покрытии. 

# Полезные библиотеки
* [Apache Commons Lang](https://github.com/apache/commons-lang) тут обратить внимание на классы `RandomStringUtils.java` и `RandomUtils.java`
* [Random Beans](https://github.com/benas/random-beans) для рандомных объектов на основе java бинов
* [wordnet-random-name(Human-friendly Random Name Generator)](https://github.com/kohsuke/wordnet-random-name)  полезная библиотека, которая позволяет получать рандомные строки в читаемом виде.
