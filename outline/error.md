# CodeGreenBook

 meituan

## 统计0~n之间的数字二进制的1的个数

```
思路：记忆存储，模拟二进制进位；
规律：f(2^n)=1;
f(n) = f(2^a)+f(n-2^a)；
pow2记为当前的2的幂数；before为幂数之后的个数；
由于之前二进制个数存储在res数组已知，在2幂次数之后，1+res[before]；
举例：
2->1;3->f(2)+f(1)=1+res[1]=2;
5->f(4)+f(1)=2;6=f(4)+f(2)=2;7->f(4)+f(3)=3;
```

```
 public int[] countBits(int num){
        int[] res = new int[num + 1];
        int pow2 = 1;
        int before = 1;
        for(int i = 1; i <= num;i++){
            if(i == pow2){
                before = res[i]  = 1;
                pow2=pow2*2;
            }else{
                res[i] = res[before] + 1;
                before += 1;
            }
        }
        return res;
    }
```





sql：

