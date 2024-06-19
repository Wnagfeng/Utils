<div  class="box"  style="    display: flex;    justify-content: center;    align-items: center;    flex-direction: column; ">  <h1 align="center">Welcome to VuecomponentLibs 👋</h1> 
     <h2 align="center"> 一个在前端开发中常用的工具库  😀</h2> 
     <h2 align="center"> CoderJoon  🐂</h2> 


涵盖了数组操作、类型检查、日期处理、随机数生成、加密以及URL解析等功能

## 数组操作

### 1. 取并集 `getB`

```typescript
/**
 * 根据两个列表取并集
 * @param {number[]} list1
 * @param {number[]} list2
 * @return {number[]}
 */
export const getB = (list1: number[], list2: number[]): number[] => {
  return [...list1, ...list2];
};

// 使用案例
const list1 = [1, 2, 3];
const list2 = [3, 4, 5];
console.log(getB(list1, list2)); // [1, 2, 3, 3, 4, 5]
```

### 2. 取交集 `getJ`

```typescript
/**
 * 两个列表取交集
 * @param {number[]} list1
 * @param {number[]} list2
 * @return {number[]}
 */
export const getJ = (list1: number[], list2: number[]): number[] => {
  if (list1.length > list2.length) {
    return list1.filter((item) => list2.includes(item));
  } else {
    return list2.filter((item) => list1.includes(item));
  }
};

// 使用案例
const list1 = [1, 2, 3];
const list2 = [3, 4, 5];
console.log(getJ(list1, list2)); // [3]
```

### 3. 取差集 `getC`

```typescript
/**
 * 两个列表取差集
 * @param {number[]} list1
 * @param {number[]} list2
 * @return {number[]}
 */
export const getC = (list1: number[], list2: number[]): number[] => {
  if (list1.length > list2.length) {
    return list1.filter((item) => !list2.includes(item));
  } else {
    return list2.filter((item) => !list1.includes(item));
  }
};

// 使用案例
const list1 = [1, 2, 3];
const list2 = [3, 4, 5];
console.log(getC(list1, list2)); // [1, 2, 4, 5]
```

## 类型检查

### 4. 判断是否为对象 `isObject`

```typescript
/**
 * 严格的对象类型检查。只有普通的 JavaScript 对象会返回 true。
 */
export const isObject = (obj: any) => {
  return Object.is(toString.call(obj), '[object Object]');
};

// 使用案例
console.log(isObject({})); // true
console.log(isObject([])); // false
```

### 5. 判断是否为正则表达式 `isRegExp`

```typescript
export const isRegExp = (v: any) => {
  return Object.is(toString.call(v), '[object RegExp]');
};

// 使用案例
console.log(isRegExp(/abc/)); // true
console.log(isRegExp('abc')); // false
```

### 6. 判断是否为有效的数组索引 `isValidArrayIndex`

```typescript
export const isValidArrayIndex = (val: number) => {
  const n = parseFloat(String(val));
  return n >= 0 && Math.floor(n) === n && isFinite(val);
};

// 使用案例
console.log(isValidArrayIndex(0)); // true
console.log(isValidArrayIndex(-1)); // false
```

### 7. 判断是否为字符串 `isString`

```typescript
export const isString = (str: any) => {
  return Object.is(toString.call(str), '[object String]');
};

// 使用案例
console.log(isString('hello')); // true
console.log(isString(123)); // false
```

### 8. 判断是否为UUID `isUUID`

```typescript
export const isUUID = (str: string) => {
  return /\w{8}(-\w{4}){3}-\w{12}/.test(str);
};

// 使用案例
console.log(isUUID('123e4567-e89b-12d3-a456-426614174000')); // true
console.log(isUUID('invalid-uuid')); // false
```

## 日期处理

### 9. 格式化日期 `formatDate`

```typescript
import moment from 'moment';

/**
 * 格式化日期
 * @param dateNum 时间
 * @param isDue 是否显示时分秒
 * @return {string}
 */
export const formatDate = (dateNum: string | number, isDue = false): string => {
  if (isDue) {
    return moment(dateNum).format('YYYY-MM-DD HH:mm:ss');
  } else {
    return moment(dateNum).format('YYYY-MM-DD');
  }
};

// 使用案例
console.log(formatDate('2023-05-20', true)); // '2023-05-20 00:00:00'
console.log(formatDate('2023-05-20')); // '2023-05-20'
```

### 10. 获取年月日 `getDay`

```typescript
export const getDay = (date: Date = new Date()): string => {
  return moment(date).format('YYYYMMDD');
};

// 使用案例
console.log(getDay(new Date())); // '20230607'
```

### 11. 获取当前时间戳 `getTime`

```typescript
export const getTime = (): number => {
  return new Date().getTime();
};

// 使用案例
console.log(getTime()); // 当前时间戳
```

### 12. 根据生日计算年龄 `birthdayYear`

```typescript
export const birthdayYear = (date: Date): string | null => {
  try {
    return date ? `${moment().diff(date, 'years')}` : null;
  } catch (e) {
    console.log(e);
    return null;
  }
};

// 使用案例
console.log(birthdayYear(new Date('1990-01-01'))); // '34' (假设当前年份为2024)
```

### 13. 传递时间距离现在多少毫秒过期 `dueDateMillisecond`

```typescript
export const dueDateMillisecond = (date: string): number => {
  const currentTime = Number.parseInt(String(new Date().getTime() / 1000));
  const futureTime = Number.parseInt(String(new Date(date).getTime() / 1000));
  if (futureTime <= currentTime) {
    return 0;
  } else {
    return (futureTime - currentTime) * 1000;
  }
};

// 使用案例
console.log(dueDateMillisecond('2024-12-31 23:59:59')); // 距离指定时间的毫秒数
```

## 随机数生成与加密

### 14. 随机生成指定范围内的随机数 `getRandomNum`

```typescript
export const getRandomNum = (min: number, max: number): number => {
  return Math.floor(min + Math.random() * (max - min));
};

// 使用案例
console.log(getRandomNum(1, 10)); // 1到10之间的随机数
```

### 15. 生成随机长度的字符串 `randomString`

```typescript
import crypto from 'crypto';

export const randomString = (length: number): string => {
  return crypto.randomBytes(length).toString('hex').slice(0, length);
};

// 使用案例
console.log(randomString(10)); // 随机生成10位长度的字符串
```

### 16. 字符串MD5加密 `strToMd5`

```typescript
import crypto from 'crypto';

export const strToMd5 = (str: string): string => {
  const md5 = crypto.createHash('md5');
  return md5.update(str).digest('hex');
};

// 使用案例
console.log(strToMd5('hello')); // '5d41402abc4b2a76b9719d911017c592'
```

## URL解析

### 17. 获取URL中的query值 `getUrlQuery`

```typescript
import { URL } from 'url';

export const getUrlQuery = (urlPath: string, key: string): string | null => {
  const url = new URL(urlPath, 'https://www.');
  const params = new URLSearchParams(url.search.substring(1));
  return params.get(key);
};

// 使用案例
console.log(getUrlQuery('https://example.com?name=John', 'name')); // 'John'
```

## Map转换

### 18. 将Map转换为对象 `mapToObj`

```typescript
type ObjectType = Record<string, number | string | boolean>;

/**
 * 将map转换为对象
 * @param {Map<string, any>} map
 * @return {ObjectType}
 */
export const mapToObj = (map: Map<string, any>): ObjectType => {
  const obj: ObjectType = {};
  for (const [k, v] of map) {
    obj[k] = v;
  }
  return obj;
};

// 使用案例
const map = new Map<string, any>([['name', 'John'], ['age', 30]]);
console.log(mapToObj(map)); // { name: 'John', age: 30 }
```

