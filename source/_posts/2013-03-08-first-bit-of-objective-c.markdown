---
layout: post
title: "First bit of Objective-C"
date: 2013-03-08 00:20
comments: true
categories: code
---

I think I know very basics of Objective-C for objective way.

```
using namespace Cedar::Matchers;
using namespace Cedar::Doubles;

@interface Greeter : NSObject
- (id)initWithName:(NSString *)name;
- (NSString *)sayHello;
@property (copy) NSString *name;
@property (assign) NSString *helloWord;
@end

@interface Greeter ()
- (void)setWord;
@end

@implementation Greeter
- (id)initWithName:(NSString *)name {
  self = [super init];
  self.name = name;
  return self;
}

- (NSString *)sayHello {
  [self setWord];
  return self.helloWord;
}

- (void)setWord {
  NSMutableString *word = [NSMutableString stringWithString:@"hello"];
  if (self.name != nil) {
    [word appendString:@", "];
    [word appendString:self.name];
  } else {
    [word appendString:@" !"];
  }
  self.helloWord = word;
}
@end

SPEC_BEGIN(Sandbox)

describe (@"Greeter", ^{
  it (@"can be initialized with name", ^{
    Greeter *man = [[Greeter alloc] initWithName:@"shin1ohno"];
    man.name should equal(@"shin1ohno");
    [man sayHello] should equal(@"hello, shin1ohno");
  });

  it (@"says hello", ^{
    Greeter *man = [[Greeter alloc] init];
    [man sayHello] should equal(@"hello !");
  });
});

SPEC_END
```

