# regex_replace
* regex[meta header]
* std[meta namespace]
* function template[meta id-type]
* cpp11[meta cpp]

```cpp
namespace std {
  template <class OutputIterator, class BidirectionalIterator,
            class traits, class charT, class FST, class FSA>
  OutputIterator
  regex_replace(OutputIterator out,
                BidirectionalIterator first, BidirectionalIterator last,
                const basic_regex<charT, traits>& e,
                const basic_string<charT, FST, FSA>& fmt,
                regex_constants::match_flag_type flags = regex_constants::match_default); // (1)

  template <class OutputIterator, class BidirectionalIterator,
            class traits, class charT>
  OutputIterator
  regex_replace(OutputIterator out,
                BidirectionalIterator first, BidirectionalIterator last,
                const basic_regex<charT, traits>& e,
                const charT* fmt,
                regex_constants::match_flag_type flags = regex_constants::match_default); // (2)

  template <class traits, class charT, class ST, class SA, class FST, class FSA>
  basic_string<charT, ST, SA>
  regex_replace(const basic_string<charT, ST, SA>& s,
                const basic_regex<charT, traits>& e,
                const basic_string<charT, FST, FSA>& fmt,
                regex_constants::match_flag_type flags = regex_constants::match_default); // (3)

  template <class traits, class charT, class ST, class SA>
  basic_string<charT, ST, SA>
  regex_replace(const basic_string<charT, ST, SA>& s,
                const basic_regex<charT, traits>& e,
                const charT* fmt,
                regex_constants::match_flag_type flags = regex_constants::match_default); // (4)

  template <class traits, class charT, class FST, class FSA>
  basic_string<charT>
  regex_replace(const charT* s,
                const basic_regex<charT, traits>& e,
                const basic_string<charT, FST, FSA>& fmt,
                regex_constants::match_flag_type flags = regex_constants::match_default); // (5)

  template <class traits, class charT>
  basic_string<charT>
  regex_replace(const charT* s,
                const basic_regex<charT, traits>& e,
                const charT* fmt,
                regex_constants::match_flag_type flags = regex_constants::match_default); // (6)
}
```
* basic_regex[link basic_regex.md]
* regex_constants::match_default[link regex_constants/match_flag_type.md]
* basic_string[link ../string/basic_string.md]

## ??????
??????????????????????????????????????????????????????????????????????????????????????????????????????????????????  
??????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????  
??????????????????????????????????????????????????????????????????????????????


## ??????
- (1)???(2) `[first, last)` ???????????????????????????????????????????????????????????? `e` ????????????????????????????????????????????? `fmt` ????????????????????????????????????????????? `out` ??????????????????  
    ??????????????? `fmt` ??????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????  
    ????????????????????????????????????????????????????????? ECMAScript ??????????????????????????????????????????`flags` ??? [`regex_constants::format_sed`](regex_constants/match_flag_type.md) ???????????????????????????????????? POSIX ??????????????????????????? sed ???????????????????????????????????????  
    ??????????????????????????????????????????????????????????????? `fmt` ????????????????????????`flags` ??? [`regex_constants::format_first_only`](regex_constants/match_flag_type.md) ?????????????????????????????????????????????????????????????????????????????????????????????  
    ????????????????????????????????????????????????????????????????????? `out` ????????????????????????`flags` ??? [`regex_constants::format_no_copy`](regex_constants/match_flag_type.md) ?????????????????????????????????????????????????????????????????? `out` ???????????????????????????
- (3)???(4) ???????????????????????? [`basic_string`](../string/basic_string.md)`<charT, ST, SA>` ??????????????? `s` ????????????????????????????????????????????? [`basic_string`](../string/basic_string.md)`<charT, ST, SA>` ??????????????????????????????????????????????????????(1)???(2) ?????????????????????
- (5)???(6) ???????????????????????? `const charT*` ??????????????? `s` ????????????????????????????????????????????? [`basic_string`](../string/basic_string.md)`<charT>` ??????????????????????????????????????????????????????(1)???(2) ?????????????????????

## ?????????
- (1)???(2) ???????????????????????? `out`????????????????????????????????????
- (3)???(4) ????????????????????????
- (5)???(6) ????????????????????????


## ??????
???????????? [`regex_error`](regex_error.md) ????????????????????????????????????  
??????????????????????????? `e` ??????????????????????????? `e.`[`code`](regex_error/code.md)`()` ??? [`regex_constants::error_complexity`](regex_constants/error_type.md) ??? [`regex_constants::error_stack`](regex_constants/error_type.md) ???????????????????????????


## ??????
?????????????????????????????????????????????????????????

- (1)???(2) [`regex_iterator`](regex_iterator.md) ???????????????????????? `i` ???

    ```cpp
    regex_iterator<BidirectionalIterator, charT, traits> i(first, last, e, flags)
    ```
    * regex_iterator[link regex_iterator.md]

    ????????????????????????  

    - `i` ?????????????????????????????????????????????????????????????????????????????? 1 ??????????????????????????????  
        `flags &` [`regex_constants::format_no_copy`](regex_constants/match_flag_type.md) ??? `0` ???????????????

        ```cpp
        out = copy(first, last, out)
        ```
        * copy[link ../algorithm/copy.md]

        ??????????????????


    - `i` ??????????????????????????????????????????????????????????????????????????????????????? 1 ??????????????????????????????  
        `i` ???????????? `[first, last)` ????????????????????????????????????????????????????????? [`match_results`](match_results.md)`<BidirectionalIterator>` ???????????????????????? `m` ?????????????????????????????????????????????  
        ????????????`flags &` [`regex_constants::format_first_only`](regex_constants/match_flag_type.md) ??? `0` ????????????????????????????????????????????????????????????  

        - `flags &` [`regex_constants::format_no_copy`](regex_constants/match_flag_type.md) ??? `0` ???????????????
            ```cpp
            out = copy(m.prefix().first, m.prefix().second, out)
            ```
            * copy[link ../algorithm/copy.md]
            * prefix[link match_results/prefix.md]

            ??????????????????  

        - ????????????(1) ?????????????????????

            ```cpp
            out = m.format(out, fmt, flags)
            ```
            * format[link match_results/format.md]

            ??????(2) ?????????????????????

            ```cpp
            out = m.format(out, fmt, fmt + char_traits<charT>::length(fmt), flags)
            ```
            * format[link match_results/format.md]
            * char_traits[link ../string/char_traits.md]
            * length[link ../string/char_traits/length.md]

            ??????????????????

        ????????????`flags &` [`regex_constants::format_no_copy`](regex_constants/match_flag_type.md) ??? `0` ???????????????????????????????????? `m` ??????????????? `last_m` ?????????

        ```cpp
        out = copy(last_m.suffix().first, last_m.suffix().second, out)
        ```
        * copy[link ../algorithm/copy.md]
        * suffix[link match_results/suffix.md]

        ??????????????????

- (3)???(4) [`basic_string`](../string/basic_string.md)`<charT, ST, SA>` ??????????????????????????????????????? `result` ???????????????`regex_replace(`[`back_inserter`](../iterator/back_inserter.md)`(result), s.`[`begin`](../string/basic_string/begin.md)`(), s.`[`end`](../string/basic_string/end.md)`(), e, fmt, flags)` ??????????????????  
    ???????????? `result` ????????????
- (5)???(6) [`basic_string`](../string/basic_string.md)`<charT>` ??????????????????????????????????????? `result` ???????????????`regex_replace(`[`back_inserter`](../iterator/back_inserter.md)`(result), s, s +` [`char_traits`](../string/char_traits.md)`::`[`length`](../string/char_traits/length.md)`(s), e, fmt, flags)` ??????????????????  
    ???????????? `result` ????????????


## ???
```cpp example
#include <iostream>
#include <iterator>
#include <list>
#include <regex>
#include <string>

int main()
{
  {
    // (1) ?????????
    const std::list<char> s = { 'a', 'b', 'c', '0', '1', '2', 'd', 'e', 'f' };
    const std::regex re("\\d+");
    const std::string fmt = "[$&]";
    std::cout << "(1) '";
    std::regex_replace(std::ostream_iterator<char>(std::cout), std::begin(s), std::end(s), re, fmt);
    std::cout << '\'' << std::endl;
  }
  {
    // (2) ?????????
    const std::list<char> s = { 'a', 'b', 'c', '0', '1', '2', 'd', 'e', 'f' };
    const std::regex re("\\d+");
    const char fmt[] = "[$&]";
    const std::regex_constants::match_flag_type flags = std::regex_constants::format_no_copy;
    std::cout << "(2) '";
    std::regex_replace(std::ostream_iterator<char>(std::cout), std::begin(s), std::end(s), re, fmt, flags);
    std::cout << '\'' << std::endl;
  }
  {
    // (3) ?????????
    const std::string s = "abc123def456ghi";
    const std::regex re("\\d+");
    const std::string fmt = "[$&]";
    std::cout << "(3) '" << std::regex_replace(s, re, fmt) << '\'' << std::endl;
  }
  {
    // (4) ?????????
    const std::string s = "abc123def456ghi";
    const std::regex re("\\d+");
    const char fmt[] = "[$&]";
    const std::regex_constants::match_flag_type flags = std::regex_constants::format_first_only;
    std::cout << "(4) '" << std::regex_replace(s, re, fmt, flags) << '\'' << std::endl;
  }
  {
    // (5) ?????????
    const char s[] = "abc123def456ghi";
    const std::regex re("(\\d)(\\d)(\\d)");
    const std::string fmt = "[$3$2$1]";
    std::cout << "(5) '" << std::regex_replace(s, re, fmt) << '\'' << std::endl;
  }
  {
    // (6) ?????????
    const char s[] = "abc123def456ghi";
    const std::regex re("(\\d)(\\d)(\\d)");
    const char fmt[] = "[\\3\\2\\1]";
    const std::regex_constants::match_flag_type flags = std::regex_constants::format_sed;
    std::cout << "(6) '" << std::regex_replace(s, re, fmt, flags) << '\'' << std::endl;
  }
}
```
* std::regex_replace[color ff0000]
* std::regex[link basic_regex.md]
* std::regex_constants::match_flag_type[link /reference/regex/regex_constants/match_flag_type.md]
* std::regex_constants::format_no_copy[link /reference/regex/regex_constants/match_flag_type.md]
* std::regex_constants::format_first_only[link /reference/regex/regex_constants/match_flag_type.md]
* std::regex_constants::format_sed[link /reference/regex/regex_constants/match_flag_type.md]

### ??????
```
(1) 'abc[012]def'
(2) '[012]'
(3) 'abc[123]def[456]ghi'
(4) 'abc[123]def456ghi'
(5) 'abc[321]def[654]ghi'
(6) 'abc[321]def[654]ghi'
```


## ???????????????
### ??????
- C++11

### ?????????
- [Clang](/implementation.md#clang): 3.0, 3.1, 3.2, 3.3, 3.4, 3.5, 3.6
- [GCC](/implementation.md#gcc): 4.9.0, 4.9.1, 4.9.2, 5.0.0
- [ICC](/implementation.md#icc): ??
- [Visual C++](/implementation.md#visual_cpp): ??


## ??????
* [C++??????????????????????????????: std::regex | ?????????](https://cpplover.blogspot.jp/2015/01/c-stdregex.html)
