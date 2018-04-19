### 常见iOS崩溃总结
#### 1. 数组下标越界: index x beyond bounds

```
NSArray *array = @[@"1", @"2"];
NSLog(@"%@", array[3]);
```

```
2016-11-30 15:17:13.568563 testCrash[5823:761012] *** Terminating app due to uncaught exception 'NSRangeException', reason: '*** -[__NSArrayI objectAtIndex:]: index 3 beyond bounds [0 .. 1]'
*** First throw call stack:
(
	0   CoreFoundation                      0x00007fffc721448b __exceptionPreprocess + 171
	1   libobjc.A.dylib                     0x00007fffdb976cad objc_exception_throw + 48
	2   CoreFoundation                      0x00007fffc71372fc -[__NSArrayI objectAtIndex:] + 156
	3   testCrash                           0x0000000100001306 main + 134
	4   libdyld.dylib                       0x00007fffdc255255 start + 1
	5   ???                                 0x0000000000000003 0x0 + 3
)
libc++abi.dylib: terminating with uncaught exception of type NSException

```
> 解决方法：
- 仔细检查数组下标，尤其是以变量作为数组下标的情况。访问某个下标时增加下标检查，防止下标越界访问，难以定位的可以尝试单步调试。

#### 2. 对象无法识别/响应该方法: unrecognized selector sent to instance

```
id obj = [NSNull null];
[obj intValue];

```

```
2016-11-30 15:49:12.323250 testCrash[6050:884242] -[NSNull intValue]: unrecognized selector sent to instance 0x7fffe1a69f70
2016-11-30 15:49:12.324779 testCrash[6050:884242] *** Terminating app due to uncaught exception 'NSInvalidArgumentException', reason: '-[NSNull intValue]: unrecognized selector sent to instance 0x7fffe1a69f70'
*** First throw call stack:
(
	0   CoreFoundation                      0x00007fffc721448b __exceptionPreprocess + 171
	1   libobjc.A.dylib                     0x00007fffdb976cad objc_exception_throw + 48
	2   CoreFoundation                      0x00007fffc7295c94 -[NSObject(NSObject) doesNotRecognizeSelector:] + 132
	3   CoreFoundation                      0x00007fffc7186b55 ___forwarding___ + 1061
	4   CoreFoundation                      0x00007fffc71866a8 _CF_forwarding_prep_0 + 120
	5   testCrash                           0x00000001000013ab main + 75
	6   libdyld.dylib                       0x00007fffdc255255 start + 1
	7   ???                                 0x0000000000000003 0x0 + 3
)
libc++abi.dylib: terminating with uncaught exception of type NSException
```
> 解决方法：通常定位到代码行更改方法调用即可解决问题，但是有一种情况比较诡异：就是访问已经释放的内存对象，这时的指针是个野指针，但他可能刚好指向了某个对象，而这个对象是不能响应这个方法的，于是抛出unrecognized selector异常。由于每次执行时野指针可能指向各种类型的对象，于是就出现：各种类型的对象都抛出了相同的「不能响应该方法」的异常。

- 调用对象的copy方法，而对象没有实现NSCopying协议

```
TestObj *vc = [[TestObj alloc] init];
[vc copy];
```

```
2016-11-30 16:01:38.114463 testCrash[6245:941391] -[TestObj copyWithZone:]: unrecognized selector sent to instance 0x608000000040
2016-11-30 16:01:38.116051 testCrash[6245:941391] *** Terminating app due to uncaught exception 'NSInvalidArgumentException', reason: '-[TestObj copyWithZone:]: unrecognized selector sent to instance 0x608000000040'
*** First throw call stack:
(
	0   CoreFoundation                      0x00007fffc721448b __exceptionPreprocess + 171
	1   libobjc.A.dylib                     0x00007fffdb976cad objc_exception_throw + 48
	2   CoreFoundation                      0x00007fffc7295c94 -[NSObject(NSObject) doesNotRecognizeSelector:] + 132
	3   CoreFoundation                      0x00007fffc7186b55 ___forwarding___ + 1061
	4   CoreFoundation                      0x00007fffc71866a8 _CF_forwarding_prep_0 + 120
	5   testCrash                           0x00000001000013a5 main + 85
	6   libdyld.dylib                       0x00007fffdc255255 start + 1
	7   ???                                 0x0000000000000003 0x0 + 3
)
libc++abi.dylib: terminating with uncaught exception of type NSException
```

- 将自定义对象归档，而该对象没有实现NSCoding协议
```
TestObj *vc = [[TestObj alloc] init];
[NSKeyedArchiver archivedDataWithRootObject:vc];

```

```
2016-11-30 16:06:41.923265 testCrash[6295:972480] -[TestObj encodeWithCoder:]: unrecognized selector sent to instance 0x6000000000b0
2016-11-30 16:06:41.926106 testCrash[6295:972480] *** Terminating app due to uncaught exception 'NSInvalidArgumentException', reason: '-[TestObj encodeWithCoder:]: unrecognized selector sent to instance 0x6000000000b0'
*** First throw call stack:
(
	0   CoreFoundation                      0x00007fffc721448b __exceptionPreprocess + 171
	1   libobjc.A.dylib                     0x00007fffdb976cad objc_exception_throw + 48
	2   CoreFoundation                      0x00007fffc7295c94 -[NSObject(NSObject) doesNotRecognizeSelector:] + 132
	3   CoreFoundation                      0x00007fffc7186b55 ___forwarding___ + 1061
	4   CoreFoundation                      0x00007fffc71866a8 _CF_forwarding_prep_0 + 120
	5   Foundation                          0x00007fffc8be00ca _encodeObject + 1241
	6   Foundation                          0x00007fffc8c1bbc2 +[NSKeyedArchiver archivedDataWithRootObject:] + 156
	7   testCrash                           0x000000010000137f main + 111
	8   libdyld.dylib                       0x00007fffdc255255 start + 1
	9   ???                                 0x0000000000000003 0x0 + 3
)
libc++abi.dylib: terminating with uncaught exception of type NSException
```




#### 3. NSArray/ NSDictionary插入nil: attempt to insert nil object from objects

```
NSString *str = nil;
NSArray *array = @[str, @"test"];

```

```
2016-11-30 15:52:56.030310 testCrash[6122:886439] *** Terminating app due to uncaught exception 'NSInvalidArgumentException', reason: '*** -[__NSPlaceholderArray initWithObjects:count:]: attempt to insert nil object from objects[0]'
*** First throw call stack:
(
	0   CoreFoundation                      0x00007fffc721448b __exceptionPreprocess + 171
	1   libobjc.A.dylib                     0x00007fffdb976cad objc_exception_throw + 48
	2   CoreFoundation                      0x00007fffc710a3b4 -[__NSPlaceholderArray initWithObjects:count:] + 276
	3   CoreFoundation                      0x00007fffc7111f24 +[NSArray arrayWithObjects:count:] + 52
	4   testCrash                           0x0000000100001353 main + 99
	5   libdyld.dylib                       0x00007fffdc255255 start + 1
	6   ???                                 0x0000000000000003 0x0 + 3
)
libc++abi.dylib: terminating with uncaught exception of type NSException
```


```
NSString *str = nil;
NSDictionary *array = @{@"key" : str, @"key2" : @"value2"};

```

```
2016-11-30 15:55:36.353606 testCrash[6165:898099] *** Terminating app due to uncaught exception 'NSInvalidArgumentException', reason: '*** -[__NSPlaceholderDictionary initWithObjects:forKeys:count:]: attempt to insert nil object from objects[0]'
*** First throw call stack:
(
	0   CoreFoundation                      0x00007fffc721448b __exceptionPreprocess + 171
	1   libobjc.A.dylib                     0x00007fffdb976cad objc_exception_throw + 48
	2   CoreFoundation                      0x00007fffc71116a0 -[__NSPlaceholderDictionary initWithObjects:forKeys:count:] + 352
	3   CoreFoundation                      0x00007fffc711150b +[NSDictionary dictionaryWithObjects:forKeys:count:] + 59
	4   testCrash                           0x000000010000132f main + 127
	5   libdyld.dylib                       0x00007fffdc255255 start + 1
	6   ???                                 0x0000000000000003 0x0 + 3
)
libc++abi.dylib: terminating with uncaught exception of type NSException
```

> 解决方法：
- 检查数组或字典的元素是否为nil, 在每次添加元素到数组或字典时都要执行非nil检查，可以给数组或字典添加一个类别方法，用于安全地添加元素，在方法内部做非nil检查。

#### 4. NSUserDefaults存储非法对象: Attempt to set a non-property-list object

```
TestObj *vc = [[TestObj alloc] init];
[[NSUserDefaults standardUserDefaults] setObject:vc forKey:@"vc"];

```

```
2016-11-30 15:58:29.069742 testCrash[6201:917973] [User Defaults] Attempt to set a non-property-list object <TestObj: 0x6080000000b0> as an NSUserDefaults/CFPreferences value for key vc
2016-11-30 15:58:29.072620 testCrash[6201:917973] *** Terminating app due to uncaught exception 'NSInvalidArgumentException', reason: 'Attempt to insert non-property list object <TestObj: 0x6080000000b0> for key vc'
*** First throw call stack:
(
	0   CoreFoundation                      0x00007fffc721448b __exceptionPreprocess + 171
	1   libobjc.A.dylib                     0x00007fffdb976cad objc_exception_throw + 48
	2   CoreFoundation                      0x00007fffc729296d +[NSException raise:format:] + 205
	3   CoreFoundation                      0x00007fffc714cd66 _CFPrefsValidateValueForKey + 278
	4   CoreFoundation                      0x00007fffc71c496d -[CFPrefsPlistSource sendMessageSettingValue:forKey:] + 573
	5   CoreFoundation                      0x00007fffc72ee6a1 -[CFPrefsPlistSource alreadylocked_setValues:forKeys:count:] + 1089
	6   CoreFoundation                      0x00007fffc726c356 -[CFPrefsSource setValues:forKeys:count:removeValuesForKeys:count:] + 262
	7   CoreFoundation                      0x00007fffc714cc40 -[CFPrefsSource setValues:forKeys:count:] + 32
	8   CoreFoundation                      0x00007fffc72b9d5b -[CFPrefsSearchListSource alreadylocked_setValues:forKeys:count:] + 523
	9   CoreFoundation                      0x00007fffc726c356 -[CFPrefsSource setValues:forKeys:count:removeValuesForKeys:count:] + 262
	10  CoreFoundation                      0x00007fffc714cc40 -[CFPrefsSource setValues:forKeys:count:] + 32
	11  CoreFoundation                      0x00007fffc71975ea -[CFPrefsSource setValue:forKey:] + 58
	12  CoreFoundation                      0x00007fffc72bba12 __108-[_CFXPreferences(SearchListAdditions) withSearchListForIdentifier:container:cloudConfigurationURL:perform:]_block_invoke + 290
	13  CoreFoundation                      0x00007fffc72bb889 -[_CFXPreferences(SearchListAdditions) withSearchListForIdentifier:container:cloudConfigurationURL:perform:] + 345
	14  CoreFoundation                      0x00007fffc72e8125 -[_CFXPreferences setValue:forKey:appIdentifier:container:configurationURL:] + 261
	15  CoreFoundation                      0x00007fffc7197534 _CFPreferencesSetAppValueWithContainer + 68
	16  Foundation                          0x00007fffc8b9ebbf -[NSUserDefaults(NSUserDefaults) setObject:forKey:] + 55
	17  testCrash                           0x0000000100001364 main + 148
	18  libdyld.dylib                       0x00007fffdc255255 start + 1
	19  ???                                 0x0000000000000003 0x0 + 3
)
libc++abi.dylib: terminating with uncaught exception of type NSException

```

> The NSUserDefaults class provides convenience methods for accessing common types such as floats, doubles, integers, Booleans, and URLs. A default object must be a property list, that is, an instance of (or for collections a combination of instances of): NSData, NSString, NSNumber, NSDate, NSArray, or NSDictionary. If you want to store any other type of object, you should typically archive it to create an instance of NSData. For more details, see Preferences and Settings Programming Guide.

> 解决方法：
- 目前NSUserDefaults支持的数据类型：floats，doubles，integers，Booleans，URLs，NSData，NSString，NSNumber，NSDate，NSArray，NSDictionary。如果是其他对象类型要保存到NSUserDefaults，可以将对象归档成NSData再存入（注：自定义对象要归档需要实现NSCoding协议）。



#### 5. 同时遍历并修改集合的元素：Collection <__NSArrayM: 0x6000000401b0> was mutated while being enumerated.


```
NSMutableArray *array = [[NSMutableArray alloc] initWithObjects: @"1", @"2", @"3", @"4", nil];
for (NSString *str in array) {
    if ([str isEqualToString:@"2"]) {
        [array removeObject:str];
    }
}

```

```

2016-11-30 16:26:02.074905 testCrash[6498:1072145] *** Terminating app due to uncaught exception 'NSGenericException', reason: '*** Collection <__NSArrayM: 0x6000000401b0> was mutated while being enumerated.'
*** First throw call stack:
(
	0   CoreFoundation                      0x00007fffc721448b __exceptionPreprocess + 171
	1   libobjc.A.dylib                     0x00007fffdb976cad objc_exception_throw + 48
	2   CoreFoundation                      0x00007fffc7292616 __NSFastEnumerationMutationHandler + 294
	3   testCrash                           0x00000001000011e9 main + 441
	4   libdyld.dylib                       0x00007fffdc255255 start + 1
	5   ???                                 0x0000000000000003 0x0 + 3
)
libc++abi.dylib: terminating with uncaught exception of type NSException
```

> 解决方法：
- 引入一个临时数组，临时数组用来遍历，原数组用来操作。

```
NSMutableArray *array = [[NSMutableArray alloc] initWithObjects: @"1", @"2", @"3", @"4", nil];
NSArray *tempArray = [[NSArray alloc] initWithArray:array];//临时数组
for (NSString *str in tempArray) {
    if ([str isEqualToString:@"2"]) {
        [array removeObject:str];
    }
}


```


#### 6. 访问已经释放的对象: EXC_BAD_ACCESS

> 解决方法：
- 这个崩溃通常是由于访问已经释放的内存造成的，使用ARC之后这种情况已经比较少了，出现时可以通过打开NSZombie（僵尸对象）来定位问题。（注：设置NSZombie环境变量后，一个对象销毁时会被转化为 _NSZombie，当你向一个已经释放的对象发送消息，这个对象就不会向之前那样Crash或者产生 一个难以理解的行为，而是放出一个错误消息，然后以一种可预测的可以产生debug断点的方式消失， 因此我们就可以找到具体或者大概是哪 个对象被错误地释放了。）


打开NSZombie： Edit Schema -> Run -> Diagnostics, 勾选Zombie Objects

![image](http://img1.ph.126.net/-BXRqG-dMhiIWLj6Du0vrA==/6631491077679047356.png)
![image](http://img1.ph.126.net/9RGqblw81EU2rVhZ9b67Yw==/6631793443376679970.png)
