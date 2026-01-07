1. `string.trim()` : to trim leading and trailing whitespaces/new lines `"   ashish rana   " -> "ashish rana"`
2. `.equals()` functions is used for non-primitive inbuilt objects (starts with capital letters)

### Inbuilt
-> non-primitive (Objects) : Integer, String, Character, HashMap, Stack, ArrayList, HashSet, etc...

-> primitive : int, char, boolean, byte, short, long, double, float

### user-defined Objects 
-> Info class

3. to compare two user-defined objects by value, we have to override .equals() function
4.  `==` compares reference of two objects (memmory location), `map.equals(map2), Arrays.equals(arr1,arr2)` compares values inside two objects (user-defined/inbuilt)

``` java
import java.util.*;
class Main {
    public static class Info implements Comparable<Info>{
        char c;
        int n;
        public Info(char c,int n){
            this.c=c;
            this.n=n;
        }
        @Override
        public int compareTo(Info i){
            return this.n-i.n;
        }
        public boolean equals(Object other){
            Info i=(Info) other; // casting object type to Info
            return this.c==i.c && this.n==i.n;
        }
    }
    public static void main(String[] args) {
        Info info=new Info('a',1);
        Info info2=new Info('a',1);
        System.out.println(info.compareTo(info2)); //0
        System.out.println(info.equals(info2)); //true

        int[] arr={1,2,3};
        System.out.println(Arrays.equals(arr,new int[]{1,2,3})); //true
    }
}
```
