# replace
* string[meta header]
* std[meta namespace]
* basic_string[meta class]
* function[meta id-type]

```cpp
basic_string& replace(size_type pos1, size_type n1,
                      const basic_string& str);                     // (1)

basic_string& replace(size_type pos1, size_type n1,
                      const basic_string& str,
                      size_type pos2, size_type n2);                // (2) C++11
basic_string& replace(size_type pos1, size_type n1,
                      const basic_string& str,
                      size_type pos2, size_type n2 = npos);         // (2) C++14

basic_string& replace(size_type pos, size_type n1, const charT* s,
                      size_type n2);                                // (3)
basic_string& replace(size_type pos, size_type n1, const charT* s); // (4)
basic_string& replace(size_type pos, size_type n1, size_type n2,
                      charT c);                                     // (5)

basic_string& replace(iterator i1, iterator i2,
                      const basic_string& str);                     // (6) C++03
basic_string& replace(const_iterator i1, const_iterator i2,
                      const basic_string& str);                     // (6) C++11

basic_string& replace(iterator i1, iterator i2,
                      const charT* s, size_type n);                 // (7) C++03
basic_string& replace(const_iterator i1, const_iterator i2,
                      const charT* s, size_type n);                 // (7) C++11

basic_string& replace(iterator i1, iterator i2,
                      const charT* s);                              // (8) C++03
basic_string& replace(const_iterator i1, const_iterator i2,
                      const charT* s);                              // (8) C++11

basic_string& replace(iterator i1, iterator i2,
                      size_type n, charT c);                        // (9) C++03
basic_string& replace(const_iterator i1, const_iterator i2,
                      size_type n, charT c);                        // (9) C++11

template <class InputIterator>
basic_string& replace(iterator i1, iterator i2,
                      InputIterator j1, InputIterator j2);          // (10) C++03
template <class InputIterator>
basic_string& replace(const_iterator i1, const_iterator i2,
                      InputIterator j1, InputIterator j2);          // (10) C++11

basic_string& replace(const_iterator i1, const_iterator i2,
                      initializer_list<charT> il);                  // (11) C++11

// string_view???????????????????????????????????????
template<class T>
basic_string& replace(size_type pos1,
                      size_type n1,
                      const T& t);                                  // (12) C++17
template<class T>
basic_string& replace(size_type pos1, 
                      size_type n1,
                      const T& t,
                      size_type pos2,
                      size_type n2 = npos);                         // (13) C++17
template<class T>
basic_string& replace(const_iterator i1,
                      const_iterator i2,
                      const T& t);                                  // (14) C++17
```

## ??????
????????????????????????????????????

## ???????????????????????????????????????

- (12)(13)(14) : ??????????????????????????????????????????
    - [`is_convertible_v`](/reference/type_traits/is_convertible.md)`<const T&, `[`basic_string_view`](/reference/string_view/basic_string_view.md)`<charT, traits>> == true`
    - [`is_convertible_v`](/reference/type_traits/is_convertible.md)`<const T&, const charT*> == false`

## ??????
- (1) : `pos1 <=` [`size()`](size.md)
- (2) : `pos1 <=` [`size()`](size.md)????????????`pos2 <= str.`[`size()`](size.md)??????????????????
- (3) : `pos1 <=` [`size()`](size.md)??????????????????????????????????????????`s`?????????????????????`n2`??????????????????????????????????????????????????????
- (4) : `pos <=` [`size()`](size.md)??????????????????????????????????????????`s`?????????????????????[`traits::length`](/reference/string/char_traits/length.md)`(s) + 1`??????????????????????????????????????????????????????
- (6) : `[`[`begin()`](begin.md)`, i1)`?????????`[i1, i2)`????????????????????????????????????
- (7) : `[`[`begin()`](begin.md)`, i1)`?????????`[i1, i2)`???????????????????????????????????????????????????????????????????????????`s`?????????????????????`n`??????????????????????????????????????????????????????
- (8) : `[`[`begin()`](begin.md)`, i1)`?????????`[i1, i2)`???????????????????????????????????????????????????????????????????????????`s`?????????????????????[`traits::length`](/reference/string/char_traits/length.md)`(s) + 1`??????????????????????????????????????????????????????
- (9) : `[`[`begin()`](begin.md)`, i1)`?????????`[i1, i2)`????????????????????????????????????
- (10) : `[`[`begin()`](begin.md)`, i1)`???`[i1, i2)`????????????`[j1, j2)`????????????????????????????????????
- (11) : `[`[`begin()`](begin.md)`, i1)`?????????`[i1, i2)`????????????????????????????????????
- (14) : `[`[`begin()`](begin.md)`, i1)`?????????`[i1, i2)`????????????????????????????????????


## ??????
- (1) : `replace(pos1, n1, str.`[`data()`](data.md)`, str.`[`size()`](size.md)`)`??????????????????
- (2) :
    - `n2`???`str.`[`size()`](size.md) `- pos2`????????????????????????`rlen`????????????`n == npos` ??????????????? `str.`[`size`](size.md)`() - pos2` ?????????????????????
    - `replace(pos1, n1, str.`[`data()`](data.md) `+ pos2, rlen)`??????????????????
- (3) : `n1`???[`size()`](size.md) `- pos1`????????????????????????`xlen`??????????????????`pos1`????????????`xlen`??????????????????????????????`s`?????????`n2`???????????????????????????
- (4) : `replace(pos, n, s,` [`traits::length`](/reference/string/char_traits/length.md)`(s))`??????????????????
- (5) : `replace(pos1, n1, basic_string(n2, c))`???????????????????????????
- (6) : `replace(i1 -` [`begin()`](begin.md)`, i2 - i1, str)`??????????????????
- (7) : `replace(i1 -` [`begin()`](begin.md)`, i2 - i1, s, n)`??????????????????
- (8) : `replace(i1 -` [`begin()`](begin.md)`, i2 - i1, s,` [`traits::length`](/reference/string/char_traits.md)`(s))`??????????????????
- (9) : `replace(i1 -` [`begin()`](begin.md)`, i2 - i1, basic_string(n, c))`??????????????????
- (10) : `replace(i1 -` [`begin()`](begin.md)`, i2 - i1, basic_string(j1, j2))`??????????????????
- (11) : `replace(i1 -` [`begin()`](begin.md)`, i2 - i1, il.`[`begin()`](/reference/initializer_list/initializer_list/begin.md)`, il.`[`size()`](/reference/initializer_list/initializer_list/size.md)`)`??????????????????
- (12) : ??????????????????
  ```cpp
  basic_string_view<charT, traits> sv = t;
  return replace(pos1, n1, sv.data(), sv.size());
  ```
  * basic_string_view[link /reference/string_view/basic_string_view.md]

- (13) : ??????????????????
  ```cpp
  basic_string_view<charT, traits> sv = t;
  return replace(pos1, n1, sv.substr(pos2, n2));
  ```
  * basic_string_view[link /reference/string_view/basic_string_view.md]
  * substr[link /reference/string_view/basic_string_view/substr.md]

- (14) : ??????????????????
  ```cpp
  basic_string_view<charT, traits> sv = t;
  return replace(i1 - begin(), i2 - i1, sv.data(), sv.size());
  ```
  * basic_string_view[link /reference/string_view/basic_string_view.md]


## ?????????
`*this`


## ??????
- (1) : `pos1 >` [`size()`](size.md)????????????[`out_of_range`](/reference/stdexcept.md)????????????????????????
- (2) : `pos1 >` [`size()`](size.md)????????????`pos2 > str.`[`size()`](size.md)??????????????????[`out_of_range`](/reference/stdexcept.md)????????????????????????
- (3) : `pos1 >` [`size()`](size.md)????????????[`out_of_range`](/reference/stdexcept.md)??????????????????????????????????????????????????????????????????`max_size()`?????????????????????[`length_error`](/reference/stdexcept.md)????????????????????????
- (13) : `pos1 >` [`size()`](size.md)????????????`pos2 > sv.`[`size()`](/reference/string_view/basic_string_view/size.md)??????????????????[`out_of_range`](/reference/stdexcept.md)????????????????????????


## ???
```cpp example
#include <iostream>
#include <string>

int main()
{
  // (1) ????????????????????????N???????????????????????????????????????
  {
    std::string s1 = "12345";
    std::string s2 = "abcde";

    // 1????????????2????????????s2???????????????????????????
    s1.replace(1, 2, s2);

    std::cout << "(1) : " << s1 << std::endl;
  }

  // (2) ?????????????????????N????????????????????????????????????????????????
  {
    std::string s1 = "12345";
    std::string s2 = "abcde";

    // 1????????????2????????????s2.substr(2, 3)??????????????????
    s1.replace(1, 2, s2, 2, 3);

    std::cout << "(2) : " << s1 << std::endl;
  }

  // (3) ????????????????????????N?????????????????????????????????M????????????????????????
  {
    std::string s1 = "12345";

    // 1????????????2????????????"abcde"?????????3????????????????????????
    s1.replace(1, 2, "abcde", 3);

    std::cout << "(3) : " << s1 << std::endl;
  }

  // (4) ????????????????????????N??????????????????????????????????????????
  {
    std::string s = "12345";

    s.replace(1, 2, "abcde");

    std::cout << "(4) : " << s << std::endl;
  }

  // (5) ????????????????????????N????????????M??????????????????????????????
  {
    std::string s = "12345";

    // 1????????????2????????????3??????'x'??????????????????
    s.replace(1, 2, 3, 'x');

    std::cout << "(5) : " << s << std::endl;
  }

  // (6) ??????????????????????????????????????????????????????????????????
  {
    std::string s1 = "12345";
    std::string s2 = "abcde";

    // '2'??????'3'???s2??????????????????
    s1.replace(s1.begin() + 1, s1.begin() + 3, s2);

    std::cout << "(6) : " << s1 << std::endl;
  }

  // (7) ????????????????????????????????????????????????????????????N????????????????????????
  {
    std::string s = "12345";

    // '2'??????'3'??????"abcde"?????????3????????????????????????
    s.replace(s.begin() + 1, s.begin() + 3, "abcde", 3);

    std::cout << "(7) : " << s << std::endl;
  }

  // (8) ?????????????????????????????????????????????????????????????????????
  {
    std::string s = "12345";

    s.replace(s.begin() + 1, s.begin() + 3, "abcde");

    std::cout << "(8) : " << s << std::endl;
  }

  // (9) ???????????????????????????????????????N??????????????????????????????
  {
    std::string s = "12345";

    // '2'??????'3'??????3??????'x'??????????????????
    s.replace(s.begin() + 1, s.begin() + 3, 3, 'x');

    std::cout << "(9) : " << s << std::endl;
  }

  // (10) ??????????????????????????????????????????????????????????????????????????????????????????
  {
    std::string s1 = "12345";
    std::string s2 = "abcde";

    s1.replace(s1.begin() + 1, s1.begin() + 3, s2.begin(), s2.end());

    std::cout << "(10) : " << s1 << std::endl;
  }

  // (11) ???????????????????????????????????????????????????????????????????????????????????????
  {
    std::string s = "12345";

    s.replace(s.begin() + 1, s.begin() + 3, {'a', 'b', 'c', 'd', 'e'});

    std::cout << "(11) : " << s << std::endl;
  }

  // (12) ????????????????????????basic_string_view????????????????????????????????????????????????
  {
    std::string s1 = "12345";
    std::string_view sv2 = std::string_view{"XXXabcdeYYY"}.substr(3, 5);

    // 1????????????2????????????sv2???????????????????????????
    s1.replace(1, 2, sv2);

    std::cout << "(12) : " << s1 << std::endl;
  }

  // (13) ????????????????????????basic_string_view??????????????????????????????????????????
  {
    std::string s1 = "12345";
    std::string_view sv2 = "XXXabcdeYYY";

    // 1????????????2????????????sv2???????????????????????????
    s1.replace(1, 2, sv2, 3, 5);

    std::cout << "(13) : " << s1 << std::endl;
  }

  // (14) ???????????????????????????????????????basic_string_view????????????????????????????????????????????????
  {
    std::string s1 = "12345";
    std::string_view sv2 = std::string_view{"XXXabcdeYYY"}.substr(3, 5);

    // 1????????????2????????????sv2???????????????????????????
    s1.replace(s1.begin() + 1, s1.begin() + 3, sv2);

    std::cout << "(14) : " << s1 << std::endl;
  }
}
```
* replace[color ff0000]
* begin()[link begin.md]
* end()[link end.md]

### ??????
```
(1) : 1abcde45
(2) : 1cde45
(3) : 1abc45
(4) : 1abcde45
(5) : 1xxx45
(6) : 1abcde45
(7) : 1abc45
(8) : 1abcde45
(9) : 1xxx45
(10) : 1abcde45
(11) : 1abcde45
(12) : 1abcde45
(13) : 1abcde45
(14) : 1abcde45
```


## ??????
- [N2679 Initializer Lists for Standard Containers(Revision 1)](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2008/n2679.pdf)
    - (11)??????????????????????????????
- [LWG ISsue 2268. Setting a default argument in the declaration of a member function `assign` of `std::basic_string`](http://www.open-std.org/jtc1/sc22/wg21/docs/lwg-defects.html#2268)
    - C++14??????(2)??????????????????????????????`n = npos`????????????????????????????????????
- [P0254R2 Integrating `std::string_view` and `std::string`](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0254r2.pdf)
- [LWG Issue 2758. `std::string{}.assign("ABCDE", 0, 1)` is ambiguous](https://wg21.cmeerw.net/lwg/issue2758)
- [LWG Issue 2946. LWG 2758's resolution missed further corrections](https://wg21.cmeerw.net/lwg/issue2946)
    - ?????????????????????????????????????????????`string_view`?????????????????????????????????(12)(13)(14)???????????????`const T&`?????????
