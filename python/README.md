# Python

[Monadic error handling](https://www.youtube.com/watch?v=J-HWmoTKhC8)  
[Structural pattern matching](https://earthly.dev/blog/structural-pattern-matching-python/)  
[Project layout](./project-layout.md)  
[Setup emvironment](./setup-environment.md)  

## Setup environment
Install Python 3
```
sudo apt python3 python3-pip
export PATH="$PATH:/home/$USER/.local/bin"
```
Install Jupyter notebook
```
pip3 install notebook
jupyter notebook --ip 0.0.0.0 --port 8888 --no-browser
```
Install python auto format
```
pip3 install autopep8
```

## Install dependencies and run apps
```
pip3 install -r requirements.txt
PYTHONPATH=path/to/lib python3 path/to/src/app.py x y z
```

## Reflection
```
type(x) -> <class X>
```

## Variable args
```
fn = lambda *args: args
fn(x,...) -> (x,...)

fn = lambda **kwargs: kwargs
fn(x=y,...) -> {'x':y,...}
```

## For-loop idioms
```
for i in range(n): ...
for i in range(b,e,k): ...
for x in itx: ...
for i,x in enumerate(itx): ...
```

## Comprehensions
```
list(fn(x) for x in itx if p(x))            [fn(x) for x in itx if p(x)]
tuple(fn(x) for x in itx if p(x))           (fn(x) for x in itx if p(x))
set(fn(x) for x in itx if p(x))             {fn(x) for x in itx if p(x)}
dict((key(x),fn(x)) for x in itx if p(x))   {key(x):fn(x) for x in itx if p(x)}
```

## Regular expressions
```
(parse = re.compile(r).search)(s) -> None | m
m.group(0) -> s           -- matched substring
m.group(i) -> s           -- matched group i
m.groups() -> (s,...)     -- matched groups
```

## Random
```
random.randint(l, r) -> n                   l <= n <= r
random.choice('abcd') -> 'a' | 'b' | ...
random.choices('abcd', k=k) -> ['a',...]

string.ascii_letters
string.digits
string.ascii_uppercase
string.ascii_lowercase
```

## Functional
```
map(fn= x->y, itx) -> ity
filter(p= x->t, itx) -> itx
(fold = functools.reduce)(fn= (y,x)->y', itx, y0) -> y
(flatten = itertools.chain.from_iterable)(itxs) -> itx
(flatmap = lambda fn,xs: flatten(map(fn,xs)))(fn= x->[y], itx) -> ity
(slice = itertools.islice)(itx,b,e,k) -> itx
(pair = itertools.pairwise)(itx) -> it (xi,xi+1)
(group = itertools.groupby)(sorted(itx), key=x->y) -> it (y,itx)
(scan = itertools.accumulate)(itx, func= (x',x)->x", initial=None) -> itx'

(pipe = lambda *fns: reduce(lambda g,f: lambda x: f(g(x)), fns))(fn,...) -> fn

list(flatmap(lambda x:[10*x] if x%2==0 else [], range(10))) -> [0,20,40,60,80]
pipe(lambda x:10*x, str, lambda x:'a'+x)(1) -> 'a10'
```

## List / Sequence
```
xs[i]
xs[b:e:k]
xs[b:e] = xs'
del xs[b:e]
n * [None]

x in xs
x not in xs

len(xs) -> n
min/max(xs) -> x

xs.sort(key= x->y, reverse= t)
sorted(itx, key= x->y, reverse= t) -> xs'

xs.reverse()
reversed(xs) -> itx

xs.index(x,b,e) -> i  ValueError
xs.count(x) -> n

xs.append(x)      xs[n:n] = [x]
xs.extend(itx)    xs[n:] = itx, xs += itx
xs.insert(i,x)    xs[i:i] = [x]
xs.remove(x)      del xs[s.index(x)]   ValueError
xs.copy() -> xs'  xs' = xs[:]
xs.clear()        del xs[:]
```

## String
```
str(x) -> s       x.__str__() -> s

f'...{expr:n}...' -> s
'...{i}...'.format(x,...) -> s
'...{x}'.format_map({x:y,...}) -> s

s.center(n,ch) -> s'
s.l/rjust(n,ch) -> s'
s.l/r/strip(chs) -> s'

len(s) -> n

s.index(u,b,e) -> i
s.count(u,b,e) -> n
s.r/find(u,b,e) -> i

s.encode('utf8') -> bs
bs.decode('utf8') -> s

chr(s) -> n
ord(n) -> s

s.removeprefix/suffix(u) -> s'
s.starts/endswith(u,b,e) -> t

s.replace(u',u",n)

s.r/split(u) -> [s',...]
s.splitlines(keeprn= t) -> [s',...]
s.r/partittion(u) -> (s',u,s")
s.join(itx) -> s'

s.upper/lower() -> s'
s.swapcase/title/capitalize() -> s'
```

## Bytes, bytearray, memoryview
```
byte(src, encoding= 'utf8')         -- immutable
bytearray(src, encoding= 'utf8')    -- mutable     

fromhex(s) ->bs
bs.hex() -> s

s.encode('utf8') -> bs
bs.decode('utf8') -> s

memoryview(bs) -> xs
```

## Set
```
set(itx) -> s

x in s
x not in s

s.isdisjoint(u) -> t
s.issubset(u) -> t                  s <= u,   s < u
s.issuperset(u) -> t                s >= u,   s > u
s.union(u,...) -> s'                s | u | ...
s.intersection(u,...) ->s'          s & u & ...
s.difference(u,...) -> s'           s - u - ...
s.symmetric_difference(u)           s ^ u
s.update(u,...)                     s |= u | ...
s.symmetric_difference_update(u)    s ^= u

s.copy() -> s'
s.add(x)
s.remove(x)     KeyError
s.discard(x)
s.pop()
s.clear()
```

## Dictionary
```
dict( it ('x',y) )
dict(x=y,...)

len(d) -> n

list(d) -> [x,...]
d.keys() -> it x
d.items() -> it (x,y)
d.values() -> it y

d[x] -> y               KeyError
d[x] = y
del d[x]                KeyError
d.pop(x, y0) -> y|y0

d.setdefault(x,y0) -> y  --mutates
d.get(x,y0) -> y|y0
```
