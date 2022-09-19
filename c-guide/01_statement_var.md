## Variables and Statements

“It takes all kinds to make a world, does it not, Padre?”  
“So it does, my son, so it does.”  
—Pirate Captain Thomas Bartholomew Red to the Padre, Pirates

There sure can be lotsa stuff in a C program.
C程序中肯定有很多东西

And for various reasons, it’ll be easier for all of us if we classify some of the types of things you can find in a program, so we can be clear what we’re talking about.
由于各种原因，如果我们对程序中可以找到的某些类型的事物进行分类，对我们所有人来说都会更容易，这样我们就可以清楚我们在说什么

### 3.1 Variables
It’s said that “variables hold values”. But another way to think about it is that a variable is a humanreadable name that refers to some data in memory.
有人说变量是数据的持有者。但也有人认为变量是对应着内存数据的一个人类可读名称。

We’re going to take a second here and take a peek down the rabbit hole that is pointers. Don’t worry about it.
这里我们比较认可第二种方式， 并对指针的困惑进行探索。不过不用担心。

You can think of memory as a big array of bytes. Data is stored in this “array”. 
你可以把内存想象成一个巨大的字节数组，数据储存在这个数组中。
> A “byte” is an 8-bit binary number. Think of it as an integer that can only hold the values from 0 to 255, inclusive  
字节是一个8位二进制数。可以把它当作一个数值范围为0到255的整型数
> I’m seriously oversimplifying how modern memory works, here. But the mental model works, so please forgive me  
我这里严重简化的现代内存的工作原理。但对于新手，这个内心模型是很有用的。

If a number is larger than a single byte, it is stored in multiple bytes. Because memory is like an array, each byte of memory can be referred to by its index. This index into memory is also called an address, or a location, or a pointer.
When you have a variable in C, the value of that variable is in memory somewhere, at some address. Of
course. After all, where else would it be? But it’s a pain to refer to a value by its numeric address, so we
make a name for it instead, and that’s what the variable is.
The reason I’m bringing all this up is twofold:
1. It’s going to make it easier to understand pointer variables later—they’re variables that hold the
address of other variables!
2. Also, it’s going to make it easier to understand pointers later.
So a variable is a name for some data that’s stored in memory at some address.


