# DFS-I

##### 基础题：

[78.子集](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode78_%E5%AD%90%E9%9B%86.md)

[79.子集II](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode79_%E5%AD%90%E9%9B%86II.md)

输入: nums = [1,2,3] 输出: [ [3], [1], [2], [1,2,3], [1,3], [2,3], [1,2], [] ]

```
public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        ArrayList<Integer> tmp = new ArrayList();
        Arrays.sort(nums);
        res.add(tmp);
        dfs(nums,res,tmp,0);
        return res;

    }
    public void dfs(int[] nums,List<List<Integer>> res,ArrayList<Integer>  tmp,int pos){
        for(int i=pos;i<nums.length;i++){
            tmp.add(nums[i]);
            res.add(new ArrayList<Integer>(tmp));
            dfs(nums,res,tmp,i+1);
            tmp.remove(tmp.size()-1);
            while(i<nums.length-1&&nums[i]==nums[i+1]) i++;// 存在重复元素
        }
 }
```

[77.组合](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode77_%E7%BB%84%E5%90%88.md) 

输入: n = 4, k = 2 输出: [ [2,4], [3,4], [2,3], [1,2], [1,3], [1,4], ]

```
   public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> tmp = new ArrayList<>();
        dfs(res,tmp,n,k,1);
        return res;
    }
    void dfs(List<List<Integer>> res,List<Integer> tmp,int n,int k,int pos){
        if(k==0){
            res.add(new ArrayList<>(tmp));
            return;
        }
        for(int i=pos;i<=n;i++){
            tmp.add(i);
            dfs(res,tmp,n,k-1,i+1);
            tmp.remove(tmp.size()-1);
        }
    }
```

[46.全排列](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode46_%E5%85%A8%E6%8E%92%E5%88%97.md)

[47.全排列II](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode47_%E5%85%A8%E6%8E%92%E5%88%97II.md)

输入: [1,2,3] 输出: [ [1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], [3,2,1] ]

```
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        ArrayList<Integer> tmp = new ArrayList<>();
        Arrays.sort(nums);
        boolean [] visit = new boolean[nums.length];
        dfs(nums,res,tmp,visit);
        return  res;
    }
    public void dfs(int[] nums,List<List<Integer>> res,ArrayList<Integer> tmp,boolean [] visit){
        if(tmp.size()==nums.length){
            res.add(new ArrayList<>(tmp));
            return;
        }
        for(int i=0;i<nums.length;i++){
            if(visit[i]==false){
                tmp.add(nums[i]);
                visit[i]=true;
                dfs(nums,res,tmp,visit);
                tmp.remove(tmp.size()-1);
                visit[i]=false;
                while (i<nums.length-1&&nums[i]==nums[i+1]) i++;
            }
        }
    }
```

[59.组合总和](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode59_%E7%BB%84%E5%90%88%E6%80%BB%E5%92%8C.md)

[60.组合总和II](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode60_%E7%BB%84%E5%90%88%E6%80%BB%E5%92%8CII.md)

```
输入: candidates = [2,5,2,1,2], target = 5,
所求解集为:[[1,2,2],[5]]
```

```
   public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> tmp = new ArrayList<>();
        Arrays.sort(candidates);
        dfs(candidates,res,tmp,target,0);
        return res;
    }
    public void dfs(int[] candidates,List<List<Integer>> res,List<Integer> tmp,int target,int pos){
        if(target==0){
            res.add(new ArrayList<>(tmp));
            return;
        }
        if(target<0){
            return;
        }
        for(int i=pos;i<candidates.length;i++){
            tmp.add(candidates[i]);
            dfs(candidates,res,tmp,target-candidates[i],i+1);
            tmp.remove(tmp.size()-1);
            while(i<candidates.length-1 && candidates[i]==candidates[i+1]) i++;
        }
    }
```

#####  一维题目

[22.括号生成](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode22_%E6%8B%AC%E5%8F%B7%E7%94%9F%E6%88%90.md)

数字 n 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 有效的 括号组合。

```
public List<String> generateParenthesis(int n) {
        List<String> res = new ArrayList<>();
        if(n<=0)
            return res;
        dfs(res,"",n,n);
        return res;
    }
    public void dfs(List<String> res,String tmp,int left,int right){
        if(left==0&&right==0){
            res.add(tmp);
            return;
        }
        if(left>0){
            //String ntmp = tmp+"(";
            tmp = tmp+"(";
            dfs(res,tmp,left-1,right);
            tmp =  tmp.substring(0,tmp.length()-1);
        }
        if(right>left){
            tmp = tmp+")";
            dfs(res,tmp,left,right-1);
            tmp = tmp.substring(0,tmp.length()-1);
        }
    }
```

[17.电话号码的字符组合](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode17_%E7%94%B5%E8%AF%9D%E5%8F%B7%E7%A0%81%E7%9A%84%E5%AD%97%E6%AF%8D%E7%BB%84%E5%90%88.md)

给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合

```
    public List<String> letterCombinations(String digits) {
        // if(digits==null ||digits.length()==0)
        // return null;
        char[][] table = {{},{'a','b','c'},{'d','e','f'},{'g','h','i'},{'j','k','l'},{'m','n','o'},{'p','q','r','s'},{'t','u','v'},{'w','x','y','z'}};
        List<String> res = new ArrayList<String>();
        if(digits==null ||digits.length()==0)
         return res;
        dfs(digits,table,"",res);
        return res;
    }
    public void dfs(String digits,char[][] table,String tmp,List<String> res){
        if(digits.length()==0){
            res.add(tmp);
            return;
        }
        for(int i=0;i<table[digits.charAt(0)-'0'-1].length;i++){
            dfs(digits.substring(1),table,tmp+table[digits.charAt(0)-'0'-1][i],res);
        }
    }
```

[93.复原ip地址](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode93_%E5%A4%8D%E5%8E%9Fip%E5%9C%B0%E5%9D%80.md)

输入: "25525511135" 输出: ["255.255.11.135", "255.255.111.35"]

```
    public List<String> restoreIpAddresses(String s) {
        List<String> res = new ArrayList<String>();
        if(s.length()<4 || s.length()>12)
            return res;
        dfs(s,"",res,0);
        return res;
    }
    void dfs(String s,String tmp,List<String>  res,int count){
        if(count==3 && isIP(s)){
            res.add(tmp+s);
            return;
        }
        for(int i=1;i<4&&i<s.length();i++){
            String sub = s.substring(0,i);
            if(isIP(sub)) {
                dfs(s.substring(i), tmp + sub + '.', res, count+1);
            }
        }
    }
    boolean isIP(String s){
        if(s.charAt(0)=='0')
            return s.equals("0");
        int num = Integer.parseInt(s); //字符串转成十进制数
        return num<=255 && num>0;
    }
```



[131.分割回文串](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode131_%E5%88%86%E5%89%B2%E5%9B%9E%E6%96%87%E4%B8%B2.md)

输入: "aab" 输出: [ ["aa","b"], ["a","a","b"] ]

```
    public List<List<String>> partition(String s) {
        List<List<String>> res = new ArrayList<List<String>>();
        List<String> tmp = new ArrayList<>();
        dfs(s,res,tmp);
        return res;
    }
    void dfs(String s,List<List<String>> res, List<String> tmp){
        if(s.length()==0) {
            res.add(new ArrayList<>(tmp));
            //return;
        }
        for(int i=1;i<=s.length();i++){
            String sub = s.substring(0,i);
            if(isPal(sub)){
                tmp.add(sub);
                dfs(s.substring(i),res,tmp);
                tmp.remove(tmp.size()-1);

            }
        }
    }
    boolean isPal(String s){
        int l=0;
        int r=s.length()-1;
        while (l<r){
            if(s.charAt(l++)!=s.charAt(r--))
                return false;
        }
        return true;
    }
```

#### 二维题目

[130.被围绕的区域](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode130_%E8%A2%AB%E5%9B%B4%E7%BB%95%E7%9A%84%E5%8C%BA%E5%9F%9F.md)

找到所有被 'X' 围绕的区域，并将这些区域里所有的 'O' 用 'X' 填充。

```
    public void solve(char[][] board) {
        if(board==null || board.length==0)
            return;
        int row = board.length;
        int col = board[0].length;
        for(int i=0;i<row;i++){
            dfs(board,i,0);
            dfs(board,i,col-1);
        }
        for(int i=0;i<col;i++){
            dfs(board,0,i);
            dfs(board,row-1,i);
        }
        for(int i=0;i<row;i++){
            for(int j=0;j<col;j++){
                if(board[i][j]=='D'){
                    board[i][j]='O';
                }else if(board[i][j]=='O'){
                    board[i][j]='X';
                }
            }
        }
        return;

    }
    void dfs(char[][] board,int x,int y){
        if(x<0||x>board.length-1||y<0||y>board[0].length-1
        ||board[x][y]!='O') return;
        board[x][y]='D';
        dfs(board,x-1,y);
        dfs(board,x+1,y);
        dfs(board,x,y-1);
        dfs(board,x,y+1);
    }
```

[79.单词搜索](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode79_%E5%8D%95%E8%AF%8D%E6%90%9C%E7%B4%A2.md)

board = [ ['A','B','C','E'], ['S','F','C','S'], ['A','D','E','E'] ]

给定 word = "ABCCED", 返回 true 给定 word = "SEE", 返回 true 给定 word = "ABCB", 返回 false

```
    public boolean exist(char[][] board, String word) {
        if(board==null || board.length==0)
            return false;
        int row = board.length;
        int col = board[0].length;
        char c = word.charAt(0);
        for(int i=0;i<row;i++){
            for(int j=0;j<col;j++){
                if(board[i][j]==c){
                    board[i][j]=' ';
                    if(dfs(board,word.substring(1),i,j)) return true;
                    board[i][j]=c;
                }
            }
        }
        return false;
    }
    boolean dfs(char[][] board, String word,int x,int y){
        if(word.length()==0) return true;
        int[][] dir = {{-1,0},{1,0},{0,-1},{0,1}};
        char c = word.charAt(0);
        for(int in =0;in<4;in++){
            int i=x+dir[in][0];
            int j=y+dir[in][1];
            if(i>=0&&i<board.length&&j>=0&&j<board[0].length&&board[i][j]==c){
                board[i][j]=' ';
                if(dfs(board,word.substring(1),i,j)) return true;
                board[i][j]=c;
            }
        }
        return false;
    }
```



