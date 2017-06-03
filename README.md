# objc-tips

## Strings
```objective-c
char c = [b characterAtIndex:i];

for (int i = 0; i <= sourceSize - targetSize; i++) {
    NSRange range;
    range.length = targetSize;
    range.location = i;
    NSString *s = [source substringWithRange:range];
    if ([s isEqualToString:target]) {
        return i;
    }
}

int char_compare(const char* a, const char* b) {
    if(*a < *b) {
        return -1;
    } else if(*a > *b) {
        return 1;
    } else {
        return 0;
    }
}

NSString *sort_str(NSString *unsorted) {
    int len = [unsorted length] + 1;
    char *cstr = malloc(len);
    [unsorted getCString:cstr maxLength:len encoding:NSISOLatin1StringEncoding];
    qsort(cstr, len - 1, sizeof(char), char_compare);
    NSString *sorted = [NSString stringWithCString:cstr encoding:NSISOLatin1StringEncoding];
    free(cstr);
    return sorted;
}
```

## Sort
```objective-c
NSArray *b = [a sortedArrayUsingComparator:^NSComparisonResult(id  _Nonnull obj1, id  _Nonnull obj2) {
    int obj1V = [obj1 intValue];
    int obj2V = [obj2 intValue];
    if (obj1V > obj2V) {
        return NSOrderedDescending;
    } else if (obj1V < obj2V) {
        return NSOrderedAscending;
    }
    return NSOrderedSame;
}];

NSArray *b = [a sortedArrayUsingSelector:@selector(compare:)];
```

## Struct
```objective-c
typedef struct {
  int index;
  int value;
} NodeType;

NodeType node;
node.index = ++index;
node.value = v;
NSValue *value = [NSValue value:&node withObjCType:@encode(NodeType)];
[b addObject:value];

NSValue *v1 = obj1;
NodeType node1;
[v1 getValue:&node1];
```
