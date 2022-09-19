The regex find operator, =~
The regex match operator, ==~
The regex pattern operator, ~string

`find`  操作符 --> `=~`
`match` 操作符 --> `==~`
`pattern` 操作符 --> `~String`


示例一：各种字符串的比较
```groovy
assert "abc" == /abc/
assert "\\d" == /\d/
def reference = "hello"
assert reference == /$reference/
```

For a given string and pattern, Groovy supports the following tasks for regular
expressions:
■ Tell whether the pattern fully matches the whole string.
■ Tell whether there’s an occurrence of the pattern in the string.
■ Count the occurrences.
■ Do something with each occurrence.
■ Replace all occurrences with some text.
■ Split the string into multiple strings by cutting at each occurrence. 
对于给定的字符串与模式，Groovy支持以下正则操作：
- 判断模式是否完全匹配整个字符串
- 判断字符串的一部分是否匹配模式
- 判断字符串的子串匹配模式的数量
- 在匹配模式的部分做一些操作
- 用指定的字符串替换匹配模式的部分
- 将匹配模式的部分作为分隔符切割字符串

示例二：各操作符简单示例
1. find: =~
```groovy
def twister = 'she sells sea shells at the sea shore of seychelles'
// twister 必须包含一个长度为3，以's'开头，以'a'结束的子字符串
// find 操作符可以用于 if语句
assert twister =~ /s.a/

// find 表达式 结果是一个Matcher对象
def finder = (twister =~ /s.a/)
assert finder instanceof java.util.regex.Matcher
```
1. match: ==~
```groovy
def twister = 'she sells sea shells at the sea shore of seychelles'
// twister必须只包含由单个空格包含的单词
assert twister ==~ /(\w+ \w+)*/

// match 表达式的值是一个boolean类型值
def WORD = /\w+/
matches = (twister ==~ /($WORD $WORD)*/)
assert matches instanceof java.lang.Boolean

// match 操作符是全匹配， 而 find 不是
assert !(twister ==~ /s.e/)
```
3. 分割与替换
```groovy
def twister = 'she sells sea shells at the sea shore of seychelles'
// 替换
def WORD = /\w+/
def wordsByX = twister.replaceAll(WORD, 'x')
assert wordsByX == 'x x x x x x x x x x'
// 分割
def words = twister.split(/ /)
assert words.size() == 10
assert words[0] == 'she'
```

示例三：于每次模式匹配时，做些事情
```groovy 
def myFairStringy = 'The rain in Spain stays mainly in the plain!'
// 匹配每个以'ain'结尾的单词: \b\w*ain\b
def wordEnding = /\w*ain/
def rhyme = /\b$wordEnding\b/
// 方式一
def found = ''
myFairStringy.eachMatch(rhyme) { match ->
    found += match + ' '
}
assert found == 'rain Spain plain '

// 方式二
found = ''
(myFairStringy =~ rhyme).each { match ->
    found += match + ' '
}
assert found == 'rain Spain plain '

// 批量替换
def cloze = myFairStringy.replaceAll(rhyme){ it-'ain'+'___' }
assert cloze == 'The r___ in Sp___ stays mainly in the pl___!'
```

示例四： Matcher增强
Groovy简化的Matcher的操作，将它类比成数组
```groovy
// example 1
def matcher = 'a b c' =~ /\S/
assert matcher[0] == 'a'
assert matcher[1..2] == ['b','c']
assert matcher.size() == 3

// example 2
def (a,b,c) = 'a b c' =~ /\S/
assert a == 'a'
assert b == 'b'
assert c == 'c'

// example 3
def matcher = 'a:1 b:2 c:3' =~ /(\S+):(\S+)/
assert matcher.hasGroup()
assert matcher[0] == ['a:1', 'a', '1'] // 1st match
assert matcher[1][2] == '2' // 2nd match, 2nd group

// example 4 
def matcher = 'a:1 b:2 c:3' =~ /(\S+):(\S+)/
matcher.each { full, key, value ->
 assert full.size() == 3
 assert key.size() == 1 // a,b,c
 assert value.size() == 1 // 1,2,3
} 
```

模式复用
模式复用性能大约比不复用高3到5倍
> `~String` 表达式的值是一个 java.util.regex.Pattern 的对象
```groovy
def twister = 'she sells sea shells at the sea shore of seychelles'

// 匹配前后字母相同的单词
def regex = /\b(\w)\w*\1\b/
def many = 100 * 1000

start = System.nanoTime()
many.times{
    twister =~ regex
}
timeImplicit = System.nanoTime() - start
start = System.nanoTime()
pattern = ~regex
many.times{
    pattern.matcher(twister)
}
timePredef = System.nanoTime() - start
assert timeImplicit > timePredef * 2
```

Pattern增强
```groovy
def fourLetters = ~/\w{4}/
// case 1
assert fourLetters.isCase('work')
// case 2
assert 'love' in fourLetters
// case 3
switch('beer') {
 case fourLetters: assert true; break
 default : assert false
}
// case 4
beasts = ['bear','wolf','tiger','regex']
assert beasts.grep(fourLetters) == ['bear','wolf'] 
```

Mastering Regular Expressions, 3nd Edition, Jeffrey E. F. Friedl, O'Reilly and Associates, 2006.