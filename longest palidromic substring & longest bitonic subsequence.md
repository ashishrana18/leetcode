in longest palidromic substring,
we can solve this by 2 ways, 
1. DP
2. expanding around a index

one by DP,
solve like longest palindromic subsequence with substring change, and a additional check

second, go to each index and start expanding from that index
either palindrome can be even sized or odd sized, take both and compare which is larger

```java
class Solution {
    public String palindrome(String s,int left,int right){ //palindrome func.
        int n=s.length();
        while(left>=0 && right<n && s.charAt(left)==s.charAt(right)){
            left--;right++;
        }
        return s.substring(left+1,right);
    }

    public String longestPalindrome(String s) {
        int n=s.length();
        String max=s.substring(0,1);
        for(int i=0;i<n-1;i++){
            String oddLength = palindrome(s,i,i);
            String evenLength = palindrome(s,i,i+1);

            String temp=(oddLength.length()>evenLength.length() ? oddLength : evenLength);
            max = temp.length()>max.length() ? temp : max;
        }
        return max;
    }
}
```

same for longest bitonic subsequence,
its like a mountain structure, first strictly increasing then strictly decreasing, from same index, it should start decreasing

go to each index, and check for LIS, and LDS at that index and check which is highest 

```java
class Solution {
    public static int[] lis(int[] nums){
        int n=nums.length;
        int[] t=new int[n+1];
        Arrays.fill(t,1);t[0]=0;
        
        for(int i=2;i<n+1;i++){
            for(int j=1;j<i;j++){
                if(nums[i-1]>nums[j-1])   t[i]=Math.max(t[i],t[j]+1); 
            }
        }
        return t;
    }
    public static int longestBitonicSequence(int n, int[] nums) {
        int[] rev=new int[n];
        for(int i=0;i<n;i++)    rev[i]=nums[n-i-1];
        
        int[] lis=lis(nums);
        int[] lds=lis(rev);
        
        int max=0;
        for(int i=1;i<n+1;i++){
            if(lis[i]!=1 && lds[n-i+1]!=1)  max=Math.max(max,lis[i]+lds[n-i+1]-1);
        }
        return max;
    }
}
```
