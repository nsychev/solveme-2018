# Плохой OR: Write-up

Обозначим операцию «плохое **или**» значком ●.

Заметим, что:

* 0 ● 1 ● 1 = 1 ● 1 = 0
* 0 ● 0 ● 0 = 0 ● 0 = 0
* 1 ● 0 ● 0 = 1 ● 0 = 1
* 1 ● 1 ● 1 = 0 ● 1 = 1

Таким образом, если к биту применить «плохое **или**» дважды с одним и тем же битом, то получится исходный бит.

Раз это верно для одного бита, это верно и для числа из произвольного количества бит: *a* ● *b* ● *b* = *a* для любых чисел *a* и *b*.

Когда Акакий шифрует *a* ключом *b*, он получает *c* = *a* ● *b*. Чтобы снова получить *a*, нужно просто ещё раз применить «плохое **или**»: *c* ● *b* = *a* ● *b* ● *b* = *a*.

Попарно применим «плохое **или**» для всех символов с ключом, получим ASCII-коды символов флага.

*Спойлер*: для тех, кто не знал, «плохое **или**» — это [простой XOR](https://ru.wikipedia.org/wiki/%D0%A1%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5_%D0%BF%D0%BE_%D0%BC%D0%BE%D0%B4%D1%83%D0%BB%D1%8E_2).

Можно было решить однострочником на Python:

```python
print("".join(map(lambda x: chr(x ^ 84), map(int, "45 49 53 60 11 54 53 48 11 59 38 11 61 39 11 44 59 38".split()))))
```

Или более понятной программой:

```python
line = "45 49 53 60 11 54 53 48 11 59 38 11 61 39 11 44 59 38"
arr = list(map(int, line.split()))
for item in arr:
    print(chr(item ^ 84), end='')
```

*Мораль*: XOR надежен только когда длина ключа сопоставима с длиной шифротекста. Даже если ключ неизвестен, его можно подобрать, основываясь на частотном анализе. Даже если ключ будет не однобайтным, после анализа текста можно легко подобрать ключ, не перебирая всевозможные последовательности байт. 

Флаг: **yeah_bad_or_is_xor**
