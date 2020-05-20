### 01背包

```java
import java.util.Scanner;

public class Main{
    public static void main(String[] args) throws Exception {
        // 读入数据的代码
        Scanner reader = new Scanner(System.in);
        // 物品的数量为N
        int N = reader.nextInt();
        // 背包的容量为V
        int V = reader.nextInt();
        // 一个长度为N的数组，第i个元素表示第i个物品的体积；
        int[] v = new int[N + 1] ;
        // 一个长度为N的数组，第i个元素表示第i个物品的价值；
        int[] w = new int[N + 1] ;

        for (int i=1 ; i <= N ; i++){
            // 接下来有 N 行，每行有两个整数:v[i],w[i]，用空格隔开，分别表示第i件物品的体积和价值
            v[i] = reader.nextInt();
            w[i] = reader.nextInt();
        }
        reader.close() ;
////////////////////////////正式代码
        int[] dp = new int[V+1];
        dp[0] = 0;
        for(int i = 1; i <= N; i++){
            for(int j = V; j >= v[i]; j--){
                dp[j] = Math.max(dp[j], dp[j-v[i]] + w[i]);
            }

        }
        System.out.println(dp[V]);
    }
}

```
### 完全背包

```java
import java.util.Scanner;

public class Main{
    public static void main(String[] args) throws Exception {
        // 读入数据的代码
        Scanner reader = new Scanner(System.in);
        // 物品的数量为N
        int N = reader.nextInt();
        // 背包的容量为V
        int V = reader.nextInt();
        // 一个长度为N的数组，第i个元素表示第i个物品的体积；
        int[] v = new int[N + 1] ;
        // 一个长度为N的数组，第i个元素表示第i个物品的价值；
        int[] w = new int[N + 1] ;

        for (int i=1 ; i <= N ; i++){
            // 接下来有 N 行，每行有两个整数:v[i],w[i]，用空格隔开，分别表示第i件物品的体积和价值
            v[i] = reader.nextInt();
            w[i] = reader.nextInt();
        }
        reader.close() ;

        int[] dp = new int[V+1];
        for(int j = 0; j <= V; j++){
                dp[j] = 0;
            }
        
        for(int i = 1; i <= N; i++){
            for(int j = v[i]; j <= V; j++){
                dp[j] = Math.max(dp[j], dp[j-v[i]] + w[i]);
            }

        }
        System.out.println(dp[V]);
    }
}

```

### 多重背包

```java
import java.util.Scanner;

public class Main{
    public static void main(String[] args) throws Exception {
        // 读入数据的代码
        Scanner reader = new Scanner(System.in);
        // 物品的数量为N
        int N = reader.nextInt();
        // 背包的容量为V
        int V = reader.nextInt();
        // 一个长度为N的数组，第i个元素表示第i个物品的体积；
        int[] v = new int[N + 1] ;
        // 一个长度为N的数组，第i个元素表示第i个物品的价值；
        int[] w = new int[N + 1] ;
        int[] s = new int[N + 1] ;

        for (int i=1 ; i <= N ; i++){
            // 接下来有 N 行，每行有两个整数:v[i],w[i]，用空格隔开，分别表示第i件物品的体积和价值
            v[i] = reader.nextInt();
            w[i] = reader.nextInt();
            s[i] = reader.nextInt();
        }
        reader.close() ;

        int[] dp = new int[V+1];
        for(int j = 0; j <= V; j++){
                dp[j] = 0;
            }
        
        for(int i = 1; i <= N; i++){
            if (s[i] >= V/v[i]){
                for(int j = v[i]; j <= V; j++){
                dp[j] = Math.max(dp[j], dp[j-v[i]] + w[i]);
               
            }
                continue;
            }
            int k = 1;
            
            while (k < s[i]){
                for(int j = V; j >= v[i]*k; j--){
                dp[j] = Math.max(dp[j], dp[j-k*v[i]] + k*w[i]);
            }
                s[i] -= k;
                k = k << 1;
            }
            for(int j = V; j >= v[i]*s[i]; j--){
                dp[j] = Math.max(dp[j], dp[j-s[i]*v[i]] + s[i]*w[i]);
            }
            

        }
        System.out.println(dp[V]);
    }
}

```

### 混合3种背包问题
```java
import java.util.Scanner;

public class Main{
    
    public int[] ZeroOnePack(int[] dp, int V, int v, int w){
        for(int j = V; j >= v; j--){
            dp[j] = Math.max(dp[j], dp[j-v] + w);
        }
        return dp;
        
    }
    
    
    public int[] CompletePack(int[] dp, int V, int v, int w){
        for(int j = v; j <= V; j++){
            dp[j] = Math.max(dp[j], dp[j-v] + w);}
        return dp;
    }
    
    public int[] MultiplePack(int[] dp, int V, int v, int w, int s){
        if (s >= V/v){
            this.CompletePack(dp, V, v, w);
        }
        int k = 1;
        while (k < s){
            this.ZeroOnePack(dp, V, k*v, k*w);
            s -= k;
            k = k << 1;
        }
        this.ZeroOnePack(dp, V, s*v, s*w);
        return dp;
    }
    
    public static void main(String[] args) throws Exception {
        // 读入数据的代码
        Scanner reader = new Scanner(System.in);
        // 物品的数量为N
        int N = reader.nextInt();
        // 背包的容量为V
        int V = reader.nextInt();
        // 一个长度为N的数组，第i个元素表示第i个物品的体积；
        int[] v = new int[N + 1] ;
        // 一个长度为N的数组，第i个元素表示第i个物品的价值；
        int[] w = new int[N + 1] ;
        int[] s = new int[N + 1] ;

        for (int i=1 ; i <= N ; i++){
            // 接下来有 N 行，每行有两个整数:v[i],w[i]，用空格隔开，分别表示第i件物品的体积和价值
            v[i] = reader.nextInt();
            w[i] = reader.nextInt();
            s[i] = reader.nextInt();
        }
        reader.close() ;

        int[] dp = new int[V+1];
        for(int j = 0; j <= V; j++){
                dp[j] = 0;
            }
        Main solution = new Main();
        // 使用main函数里的方法必须先声明一个实例
        for (int i = 1; i <= N; i++){
            if (s[i] == -1){
                dp = solution.ZeroOnePack(dp,  V,  v[i],  w[i]);
            }
            else if (s[i] == 0){
                dp = solution.CompletePack(dp,  V,  v[i],  w[i]);
            }
            else{
                dp = solution.MultiplePack(dp,  V,  v[i],  w[i], s[i]);
            }
        }
        System.out.println(dp[V]);

        }
        
    }

```