# Competative Programming

#### Max Heap

```cpp
vector<int> v { ... };

// init
make_heap(v.begin(), v.end())

//push
v.push_back(n)
push_heap(v.begin(), v.end())

//pop
pop_heap(v.begin(), v.end())
n = v.back()
v.pop_back()
```

#### Deque

```cpp
deque<int> que;

// push
que.push_back(1);
// shift
que.push_front(1);

// pop
int x = que.back();
que.pop_back();

// unshift
int x = que.front();
que.pop_front();
```

#### Hash Maps

```cpp
unordered_map<string,int> map;

map["key"] = value;

if (map.find(key) != map.end()) //check for key in map

for (auto pair : map)
    cout << pair.first << pair.second << endl;
```

map is self balancing tree

#### Hash Sets

```cpp
unordered_set<string> s;

s.insert(key) //add key to set 

if (s.find(key) != s.end()) //check for set in map

for (auto key : s)
    cout << key << endl;
```

#### Vectors

```cpp
vector<int> vec;

for (auto i = vec.begin(); i != i.end(); i++)
    cout << *i << endl;

// sorting
sort(arr.begin(), arr.end());

// 2d vectors
vector<vector<int>> vec;
vec.push_back({ 1, 2, 3 });
```

| method               | functionality           |
| -------------------- | ----------------------- |
| size                 | length of vector        |
| push_back            | push                    |
| pop_back             | pop                     |
| resize(n)            | resize for n eles       |
| at(i)                | access member at i      |
| front, back          | access first and last   |
| v1.swap(v2)          | swap v1 and v2 elements |
| v1.erase(v1.begin()) | removes first ele       |

#### Speeding Up

speeds up execution time by 2 times

```cpp
ios::sync_with_stdio(false);
cin.tie(NULL);
cout.tie(NULL);
```
