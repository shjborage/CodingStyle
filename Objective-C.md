# Objective-C Coding Style
> 基于 Google Objective-C Style Guide  
> 文中提到的 C++ 标准后续也完善出来

*by Eric Shi(shjborage@gmail.com)*


[1. 前言](#1-前言)

[2. 缩进与格式](#2-缩进与格式)  

　　[2.1. 缩进符](#21-缩进符)   
　　[2.2. 每行的长度](#22-每行的长度)   
　　[2.3. 逗号分隔项](#23-逗号分隔项)   
　　[2.4. 左大括号位置](#24-左大括号位置)   
　　[2.5. 声明与定义](#25-声明与定义)   
　　[2.6. 方法调用](#26-方法调用)   
　　[2.7. @public、@protected与@private](#27-)   
　　[2.8. 异常](#28-异常)   
　　[2.9. 协议](#29-协议)   
　　[2.10. Blocks](#210-)   
　　[2.11. Container Literals](#211-)   
　　[2.12. if else 括号位置](#212-)   
　　[2.13. 空行与空格其它补充](#213-空行与空格其它补充)   

3. 命名规范
    - 3.1. 文件名
    - 3.2. Objective-C++
    - 3.3. 类名
    - 3.4. Category名
    - 3.5. Objective-C 方法名
    - 3.6. 变量名
        - 3.6.1. 普通变量名
        - 3.6.2. 类成员变量
        - 3.6.3. 常量

4. 注释
    - 4.1. 文件注释
    - 4.2. 声明部分的注释
    - 4.3. 实现部分的注释

5. Cocoa 和 Objective-C 特性
    - 5.1. 重载指定构造函数
    - 5.2. 重载 NSObject 的方法
    - 5.3. 初始化
    - 5.4. 避免调用+ new
    - 5.5. 保持公共 API 简单
    - 5.6. #import与#include
    - 5.7. 使用根框架
    - 5.8. 在init和dealloc中避免使用存取方法
    - 5.9. 按照声明顺序销毁实例变量
    - 5.10. setter中对NSString进行copy
    - 5.11. 避免抛出异常
    - 5.12. BOOL的使用
    - 5.13. 属性
        - 5.13.1. 命名
        - 5.13.2. 位置
        - 5.13.3. 字符串应使用 copy 属性
    - 5.14. 没有实例变量的接口


## 1. 前言
本规范基于Google Objective-C Style Guide，结合对Objective-C使用习惯和实际开发情况，对其中的说明性语句及非ARC部分进行了删减。
每项规范前面的[强制]代表该规范需要强制执行，[建议]代表推荐执行但不强制。

本文档风格约定部分可能跟你的喜好有冲突，请尽量用包容的心态来阅读。有任何问题或建议，欢迎反馈给我：<shjborage@gmail.com>

## 2. 缩进与格式
### 2.1. 缩进符
**[强制]** 只用空格，用4个空格表示一个缩进。

### 2.2. 每行的长度
**[建议]** 应尽量控制每行代码的长度在 **120** 个字符以内，80 对于 Objective-C 来说有点太短了。

### 2.3. 逗号分隔项
**[强制]** 用逗号分隔多项时，每个逗号后使用1个空格进行分隔

### 2.4. 左大括号位置  
**[建议]** 左大括号 `{` 不单独占据一行，放置在上一行的末尾，可以在 `{` 前增加一个空格  

如果方法参数过多或 `if` 条件过多，可考虑把 `{` 的换行，这样更清晰  
示例
```
- (NSInteger)tableView:(UITableView *)tableView
sectionForSectionIndexTitle:(NSString *)title
               atIndex:(NSInteger)index
{
}
```

### 2.5. 声明与定义
**[强制]** `-`，`+` 与返回类型之间必须有一个空格，在参数列表中，除了参数之间不要有任何间距。  

示例
```
- (void)doSomethingWithString:(NSString *)theString {
    ...
}
```

**[强制]** `*` 号前面必须要加空格，增加可读性  
**[建议]** 如果有参数太多无法放在同一行内， 最好每个参数各自一行。如果采用多行，每个参数建议按照 `:` 进行对齐  

示例
```
- (void)doSomethingWith:(GTMFoo *)theFoo
                  rect:(NSRect)theRect
              interval:(float)theInterval {
    ...
}
```

**[建议]** 当第一个关键词比其他的短时，可以缩进之后的行至少4个空格，同样按 `:` 进行对齐  

示例
```
- (void)short:(GTMFoo *)theFoo
          longKeyword:(NSRect)theRect
    evenLongerKeyword:(float)theInterval
                error:(NSError **)theError {
    ...
}
```

**[建议]** 参数太多无法在一行时，可将括号位置向下调整提高可读性  

示例
```
- (void)short:(GTMFoo *)theFoo
          longKeyword:(NSRect)theRect
    evenLongerKeyword:(float)theInterval
                error:(NSError **)theError
{
    ...
}
```

### 2.6. 方法调用

**[建议]** 方法调用的格式须要与定义时的格式一致。当有多种格式化的样式可供选择的时候，按照惯例，采用在给定的源文件中使用过的那个方式。  
**[建议]** 所有的参数都应该在同一行：  

示例
```
[myObject doFooWith:arg1 name:arg2 error:arg3];
```

或者每个参数一行，并按 `:` 对齐

示例
```
[myObject doFooWith:arg1
              name:arg2
            error:arg3];
```

不建议采用以下风格：

示例
```
[myObject doFooWith:arg1 name:arg2 //这行写了两个参数
              error:arg3];

[myObject doFooWith:arg1
              name:arg2 error:arg3];
```


就像声明和定义一样，当第一个关键词比其他的短时，可以缩进之后的行至少4个空格，同样按 `:` 进行对齐

示例
```
[myObj short:arg1
        longKeyword:arg2
  evenLongerKeyword:arg3
              error:arg4];
```

调用中如果有包含内联的 block 也可以缩进至少4个空格，然后左对齐。

### 2.7. `@public` 、`@protected` 与 `@private`
**[强制]** 访问修饰符 @public， @private，@protected必须缩进2个空格。

### 2.8. 异常
**[建议]** 在单独一行时，使用 `@` 标签格式化 `exceptions`， `@` 标签和左大括号 `{` 间加一个空格，在 `@catch` 和 对象捕获声明之间也一样。  
建议遵循下面的格式(其实跟苹果Xcode内置的Snippet是一样的)：

示例
```
@try {
    foo();
}
@catch (NSException *ex) {
    bar(ex);
}
@finally {
    baz();
}
```

### 2.9. 协议
**[强制]** 在类型标识符和封装在尖括号中的 `Protocols` 名称之间要有空格。  

这些适用于类的声明、实例变量和方法的声明  

示例
```
@interface MyProtocoledClass : NSObject <NSWindowDelegate> {
  @private
    id <MyFancyDelegate> delegate;
}

- (void)setDelegate:(id <MyFancyDelegate>)aDelegate;
@end
```

### 2.10. Blocks
**[强制]** 块内的代码应缩进4个空格。  
**[建议]** 因为具体block长度的不同，可以有以下几种风格：  

- 如果block一行就能放下，就不需要换行
- 如果必须要换行，那么 `}` 需要和block所在行的第一个字符对齐
- block中的代码块应该缩进4个空格。
- 如果block很大，比如超过20行，建议单独拿出来赋给一个本地变量
- 如果block没有参数，那字符 `^{` 之间就不应有空格。如果有参数，字符 `^{` 之间同样没有空格，但是字符 `) {` 之间需要有一个空格。
- 包含内联block的函数调用可以在缩进4个空格的基础上左对齐，尤其是调用中包含多个内联block。

示例
```
// 整个block放在一行的
[operation setCompletionBlock:^{ [self onOperationDone]; }];

//多行时缩进四个空格，{ 要和block所在行的第一个字符对齐
[operation setCompletionBlock:^{
    [self.delegate newDataAvailable];
}];

// 在C函数中使用block时遵循和Objective-C同样的对齐和缩进原则
dispatch_async(fileIOQueue_, ^{
    NSString *path = [self sessionFilePath];
    if (path) {
      // ...
    }
});

// 方法参数与block声明能放到一行时。注意比较^(SessionWindow *window) {和上面的^{。
[[SessionService sharedService]
    loadWindowWithCompletionBlock:^(SessionWindow *window) {
        if (window) {
          [self windowDidLoad:window];
        } else {
          [self errorLoadingWindow];
        }
    }];

//方法参数与block声明不能放到一行时。
[[SessionService sharedService]
    loadWindowWithCompletionBlock:
        ^(SessionWindow *window) {
            if (window) {
              [self windowDidLoad:window];
            } else {
              [self errorLoadingWindow];
            }
        }];

// 较长的Block可声明为变量。
void (^largeBlock)(void) = ^{
    // ...
};
[operationQueue_ addOperationWithBlock:largeBlock];

// 一次调用中包含多个内联block。
[myObject doSomethingWith:arg1
    firstBlock:^(Foo *a) {
        // ...
    }
    secondBlock:^(Bar *b) {
        // ...
    }];
```

### 2.11. Container Literals
**[强制]** 使用容器（数组和字典）常量，如果其内容被分为多行，应该缩进4个空格。  
**[建议]** 如果内容单行就能放下，在左大括号之后和右大括号之前各添加一个空格。  

示例
```
NSArray *array = @[ [foo description], @"Another String", [bar description] ];
NSDictionary *dict = @{ NSForegroundColorAttributeName : [NSColor redColor] };
```

**[建议]** 如果内容跨越多行，将左括号和声明放在同一行，之后换行的内容缩进4个空格，并将右括号单独放在新的一行里和声明行对齐。

示例
```
NSArray *array = @[
    @"This",
    @"is",
    @"an",
    @"array"
];
NSDictionary *dictionary = @{
    NSFontAttributeName : [NSFont fontWithName:@"Helvetica-Bold" size:12],
    NSForegroundColorAttributeName : fontColor
};
```

**[强制]** 对于字典常量，在 `:` 之前不加空格，之后至少一个空格（或者空格的数量能够满足对齐的要求）

示例
```
NSDictionary *option1 = @{
    NSFontAttributeName: [NSFont fontWithName:@"Helvetica-Bold" size:12],
    NSForegroundColorAttributeName: fontColor
};

NSDictionary *option2 = @{
    NSFontAttributeName:            [NSFont fontWithName:@"Arial" size:12],
    NSForegroundColorAttributeName: fontColor
};
```

下面的都是错误的:

示例
```
// 左大括号之后的内容应该另起一行，或者都放在同一行
// : 前不应该有空格
NSDictionary *alsoWrong= @{ AKey : @"a",
                            BLongerKey : @"b" };

// :之前不应该有多个空格
NSDictionary *stillWrong = @{
  AKey      : @"b",
  BLongerKey : @"c",
};
```

### 2.12. `if` `else` 括号位置
**[建议]** 有 `if` 就应该有 `else`，并且要在 `if` 后 `else` 前后留好空格  

示例
```
if ([someObject isRight]) {
    // do something
} else {
    // do anotherThing
}
```
或
```
if ([someObject isRight]) {
    // do something
} else if (NO) {
    // break this
} else {
    // do anotherThing
}
```

### 2.13. 空行与空格其它补充
**[建议]** 注释符号与注释内容间需要有空格  
示例
```
// 注释内容
```

**[建议]** 文件头尾要留个空行，各个方法间也要空一行  
**[建议]** 不同功能在同一个文件（包含头文件）中要按`#pragma mark -`分隔开  

示例
```
//
//  DataViewController.m
//  DevelopDemo
//
//  Created by shihaijie on 3/30/16.
//  Copyright © 2016 Saick. All rights reserved.
//

#import "DataViewController.h"

@interface DataViewController ()

@end

@implementation DataViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view, typically from a nib.

    [self.view addSubview:[self genView]];
}

- (void)didReceiveMemoryWarning {
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}

- (void)viewWillAppear:(BOOL)animated {
    [super viewWillAppear:animated];
    self.dataLabel.text = [self.dataObject description];
}

- (UIView *)genView {
    return [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 320)];
}

#pragma mark - test block

+ (void)testBlock:(void(^)(NSString *content, BOOL success))callback {
    callback(@"I'm the test content", YES);
}

@end

```  


## 3. 命名规范
在撰写纯粹的 Objective-C 代码时，推荐使用驼峰命名法（部分 model 要与其它端一致的情况就和其它端保持一致吧）。  

### 3.1. 文件名
文件名应该反映其中包含的类实现的名称，按照项目中的约定且大小写相关，一个文件中建议只实现一个类。

常见的扩展名如下:

```
.h
C/C++/Objective-C header file

.m
Objective-C implementation file

.mm
Objective-C++ implementation file

.cc
Pure C++ implementation file

.c
C implementation file
```

**[强制]** 实现Category的文件名需包含类名，且需要加前辍，如 `NSString+SQUtils.h` 或 `NSTextView+SQAutocomplete.h`。

### 3.2. Objective-C++

在一个源码文件中， Objective-C++ 遵循你实现的函数/方法的风格。

为了最小化在混合开发 Cocoa/Objective-C 和 C++ 时由命名风格造成的冲突，遵循正在实现方法的风格。如果正在实现的方法是在 @implementation 块中, 使用Objective-C 的命名规范。如果正在实现的方法是在C++的class中，则采用C++的命名规范。

示例
```
// 文件: cross_platform_header.h

class CrossPlatformAPI {
public:
  ...
  int DoSomethingPlatformSpecific();  // 每个平台的实现都不一样
private:
  int an_instance_var_;
};

// 文件: mac_implementation.mm
#include "cross_platform_header.h"

// 典型的Objective-C class, 使用Objective-C命名规范。
@interface MyDelegate : NSObject {
  @private
    int _instanceVar;
    CrossPlatformAPI *_backEndObject;
}
- (void)respondToSomething:(id)something;
@end

@implementation MyDelegate

- (void)respondToSomething:(id)something {
    // 从Cocoa桥接到C++的后端
    _instanceVar = _backEndObject->DoSomethingPlatformSpecific();
    NSString *tempString = [NSString stringWithFormat:@"%d", _instanceVar];
    NSLog(@"%@", tempString);
}

@end

// C++ class平台相关的实现, 使用C++命名规范
int CrossPlatformAPI::DoSomethingPlatformSpecific() {
    NSString *temp_string = [NSString stringWithFormat:@"%d", an_instance_var_];
    NSLog(@"%@", temp_string);
    return [temp_string intValue];
}
```

### 3.3. 类名

**[强制]** 类名（包括Category和Protocol名）以大写字母开始，通过大小写而不是下划线分隔。  
**[建议]** 在设计可跨越多个应用之间共享的代码时，推荐使用前缀，（例如，GTMSendMessage）。还有很多外部依赖库的大型应用中设计的类最好也使用前缀。  
**[强制]** 若使用前缀，则前缀缩写要大于2个字符  

### 3.4. Category名

**[强制]** 类别（Category）名中需要加入被扩展的类名。

解释  
比如我们要给NSString类加一个解析的功能，我们创建一个category，命名为 `GTMParsing`，并且放在名为 `NSString+GTMParsing.h` 的文件中。

**[强制]** 类名与左括号中间需要有一个空格。

示例
```
//扩展一个framework类：
@interface NSString (GTMStringParsingAdditions)

- (NSString *)foobarString:

@end

//使方法和属性私有化
@interface FoobarViewController ()

@property(nonatomic, retain) NSView *dongleView;

- (void)performLayout;

@end
```

### 3.5. Objective-C 方法名
**[强制]** 方法名应该以小写字母开头，混合大小写。每个命名参数也应该以小写字母开头。  
**[建议]** 方法名称应该尽可能读起来像句子，意味着你应该选择能够搭配方法名的参数名。（比如：`convertPoint:fromRect:`   
或 `replaceCharactersInRange:withString:`）。  
**[强制]** getter类型的方法不加get前缀。  

示例
```
- (id)getDelegate;    // 错误的
- (id)delegate;       // 推荐的
```

**[强制]** 在所有参数前面添加关键字  

示例

```
- (void)sendAction:(SEL)aSelector toObject:(id)anObject forAllCells:(BOOL)flag;  // 推荐的
- (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag;  // 错误的
```

**[建议]** 确保参数前面的关键字可以正确描述参数  

示例

```
- (id)viewWithTag:(NSInteger)aTag;  // 推荐的
- (id)taggedView:(int)aTag;         // 错误的
```

**[强制]** 当需要基于已有的一个方法创建新方法时，请将新的关键字添加到原有方法后面

示例

```
- (id)initWithFrame:(CGRect)frameRect;  // 原有方法
- (id)initWithFrame:(NSRect)frameRect mode:(int)aMode cellClass:(Class)factoryId numberOfRows:(int)rowsHigh numberOfColumns:(int)colsWide;  // 新方法
```

**[建议]** 尽量不要使用 “and” 描述参数

示例
```
- (int)runModalForDirectory:(NSString *)path file:(NSString *) name types:(NSArray *)fileTypes;        // 推荐的
- (int)runModalForDirectory:(NSString *)path andFile:(NSString *)name andTypes:(NSArray *)fileTypes;   // 错误的
```

### 3.6. 变量名
**[强制]** 变量名以小写字母开头，混合大小写以区分单词（驼峰命名法）。  

### 3.6.1. 普通变量名
**[强制]** 不要使用匈牙利命名法，比如不要使用变量的静态类型（int 或 pointer）。尽量写具有描述意义的名称。比如不要使用下面的变量全名：

示例
```
int w;
int nerr;
int nCompConns;
tix = [[NSMutableArray alloc] init];
obj = [someObject object];
p = [network port];
```

建议使用如下的变量命名：

```
int numErrors;
int numCompletedConnections;
tickets = [[NSMutableArray alloc] init];
userInfo = [someObject object];
port = [network port];
```

### 3.6.2. 类成员变量
**[建议]** 类成员变量的命名是在普通变量的名字前，添加一个下划线做前缀，比如 `_usernameTextField`。  
**[建议]** 无特殊情况，不建议直接定义类成员变量，应直接使用 `property`。

### 3.6.3. 常量
**[建议]** 常量名（宏，本地常变量等）首字母应该以小写的k开头，然后使用混合大小写区分单词，枚举值前面需要以枚举名为前缀。  

示例
```
const int kNumberOfFiles = 12;
NSString *const kUserKey = @"kUserKey";
enum DisPlayTinge {
  DisplayTingeGreen = 1
  DisplayTingeBlue = 2
};
```

## 4. 注释
### 4.1. 文件注释
**[建议]** 创建文件时会生成默认的注释。如果看了文件名还不懂该文件是干什么，可以有选择的在一个文件开头写一段关于内容的描述。  
**[建议]** 如果默认的注释用户名或公司不对，请自行修改。  

### 4.2. 声明部分的注释

**[建议]** 每个接口，类别，协议的声明都应该有个伴随的注释，来描述它的作用以及它如何融入整体环境。注释遵循 apple doc 风格，以/\*!开始，\*/结束。  
**[强制]** 声明部分的注释如果以 “//” 开头，且与代码同一行，在 “//” 前加空格或与其它行对齐。 在 "//" 后也要带一个空格。  

示例

```
/*!
 * <#Description#>
 *
 * @param nibNameOrNil <#nibNameOrNil description#>
 * @param nibBundleOrNil <#nibBundleOrNil description#>
 *
 * @return <#return value description#>
 */

- (id)initWithNibName:(NSString *)nibNameOrNil bundle:(NSBundle *)nibBundleOrNil;

@property (copy) NSString *host; // network host

// 或以下这种对齐方式
@property (copy) NSString *anotherHost;   // another host
@property (copy) NSString *bHost;         // b host

```

**[建议]** 公共接口的每个方法，都应该有注释来解释它的作用、参数、返回值以及其它影响。

### 4.3. 实现部分的注释
**[强制]** 实现部分的注释如果以 “//” 开头，且与代码同一行，在 “//“ 前加空格。在 "//" 后也要带一个空格。  

## 5. Cocoa 和 Objective-C 特性
### 5.1. 重载指定构造函数
**[强制]** 当写子类的时候，如果需要 `init...` 方法，必须重载父类的指定构造函数。  

### 5.2. 重载 NSObject 的方法
**[建议]** 如果重载了NSObject类的方法，建议把它们放在 `@implementation` 内的前边，这也是惯例。   
通常适用（但不局限）于 `init...`，`copyWithZone:`，以及 `dealloc` 方法。所有 `init...` 应放在一起，后面跟着其他 `NSObject` 的方法。

### 5.3. 初始化
**[建议]** 不要在 `init` 方法中，将成员变量初始化为 `0` 或 `nil`。如果一个对象可被复用，状态需要全部重置，这时可引入 `reset` 方法。  
**[强制]** 局部变量不会被编译器初始化，所有局部变量使用前必须初始化。

### 5.4. 避免调用 `+ new`
**[强制]** 不要调用 `NSObject` 的类方法 `new`，也不要在子类中重载它。使用 `alloc` 和 `init` 方法创建并初始化对象。  

### 5.5. 保持公共 API 简单
**[建议]** 保持公共API简单，避免“包含一切式“的API。 每个API只做一件事，并且意义清晰。

示例

```
// GTMFoo.m
#import "GTMFoo.h"

@interface GTMFoo (PrivateDelegateHandling)

- (NSString *)doSomethingWithDelegate;  // Declare private method

@end

@implementation GTMFoo(PrivateDelegateHandling)
...

- (NSString *)doSomethingWithDelegate {
    // Implement this method
}

...
@end
```

可以使用私有Category保证公共头文件整洁  

示例
```
@interface GTMFoo () {
  ...
}
```

### 5.6. `#import` 与 `#include`  
**[强制]** 使用 `#import` 来引用 Objective-C/Objective-C++ 头文件，使用 `#include` 引用 C/C++ 头文件。

### 5.7. 使用根框架
**[强制]** 包含根框架，而非单独的文件。

示例
```
#import <Foundation/Foundation.h>     // good

#import <Foundation/NSArray.h>        // avoid
#import <Foundation/NSString.h>
...
```

### 5.8. 在 `init` 和 `dealloc` 中避免使用存取方法
**[建议]** 在 `init` 和 `dealloc` 方法执行的过程中，子类可能会处在一个不稳定状态，所以这些方法中应避免调用存取方法，应在这些方法中直接对成员变量进行赋值或释放操作。

示例

```
- (instancetype)init {
    self = [super init];
    if (self) {
        _bar = [[NSMutableString alloc] init];  // good
    }
    return self;
}

- (void)dealloc {
    [_bar release];                             // good
    [super dealloc];
}

- (instancetype)init {
    self = [super init];
    if (self) {
        self.bar = [NSMutableString string];    // avoid
    }
    return self;
}

- (void)dealloc {
    self.bar = nil;                             // avoid
    [super dealloc];
}
```

### 5.9. 按照声明顺序销毁实例变量
**[建议]** `dealloc` 中对象被释放的顺序应该与他们在 `@interface` 中声明的顺序一致，这有助于代码检查。

### 5.10. `setter` 中对 `NSString` 进行 `copy`
**[建议]** 接受 `NSString` 作为参数的 `setter`，应该 `copy` 它所接受的字符串。

示例

```
- (void)setFoo:(NSString *)aFoo {
    [_foo autorelease];
    _foo = [aFoo copy];
}
```

### 5.11. 避免抛出异常
**[建议]** 不要 `@throw` Objective-C 异常，但要注意从第三方的调用或者系统调用捕捉异常。如果确实使用了异常，请注释期望什么方法抛出异常。

### 5.12. BOOL的使用
**[强制]** 不要直接将 `BOOL` 值与 `YES` 、`NO` 进行比较。
**[建议]** 对 `BOOL` 使用逻辑运算符（`&&`, `||` 和 `!`）是合法的，返回值也可以安全地转换成 `BOOL`。

示例

```
- (BOOL)isBold {
    return [self fontTraits] && NSFontBoldTrait;
}

- (BOOL)isValid {
    return [self stringValue];
}
```
或
```
- (BOOL)isBold {
    return ([self fontTraits] && NSFontBoldTrait) ? YES : NO;
}

- (BOOL)isValid {
    return [self stringValue] != nil;
}

- (BOOL)isEnabled {
    return [self isValid] && [self isBold];
}
```

同样，不要直接比较  `YES`/`NO` 和 `BOOL` 变量。

示例

```
// 错误的
BOOL great = [foo isGreat];
if (great == YES) {
  // ...be great!
}

// 正确的
BOOL great = [foo isGreat];
if (great) {
  // ...be great!
}
```

### 5.13. 属性
#### 5.13.1. 命名
**[建议]** 属性所关联的实例变量的命名必须遵守以下划线作为前缀的规则。属性的名字应该与成员变量去掉下划线后缀的名字一模一样。@property后面不要留空格。

示例

```
@interface MyClass : NSObject
@property(copy, nonatomic) NSString *name;
@end

@implementation MyClass
// No code required for auto-synthesis, else use:
//  @synthesize name = _name;
@end
```

#### 5.13.2. 位置
**[强制]** 属性的声明必须紧靠着类接口中的实例变量语句块。属性的定义必须在 `@implementation` 的类定义的最上方。他们的缩进与包含他们的 `@interface` 以及 `@implementation` 语句一样。

示例

```
@interface MyClass : NSObject {
  @private
    NSString *_name;
}

@property(copy, nonatomic) NSString *name;

@end

@implementation MyClass

@synthesize name = _name;

- (instancetype)init {
  ...
}

@end
```

#### 5.13.3. 字符串应使用 `copy` 属性
**[强制]** 应总是用 `copy` 属性声明 `NSString` 属性.

### 5.14. 没有实例变量的接口
**[强制]** 没有声明任何实例变量的接口，应省略空大括号。

示例

```
@interface MyClass : NSObject

// Does a lot of stuff
- (void)fooBarBam;

@end

@interface MyClass : NSObject {
}

// Does a lot of stuff
- (void)fooBarBam;

@end

```
