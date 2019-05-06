# KMP算法

``
//获取next数组代码
void get_next(char T[],int next[]){
    i=1;
    next[1]=0;//第一个字符不匹配，next值设置为0
    j=0;
    //T[0]中存储的字符数组中字符的个数
    while(i<T[0]){//递推字符串各个位置
        if(j==0||T[i]==T[j]){
            ++i;
            ++j;
            next[i]=j;//如果i和j位置元素相同，j+1后再赋值给next的下一个位置值
        }else{
            j=next[j];//如果i和j位置元素不同，则去寻找更短的相同前后缀
        }
    }
}


//KMP代码
int KMP(char S[],char T[],int next[]){
    int i=1,j=1;
    while(i<S[0]&&j<=T[0]){
        if(j==0||S[i]==T[j]){
            ++i;
            ++j;
        }else{
            j=next[j];
        }
    }
    //判断是否已经匹配到
    if(j>T[0]){
        return i-T[0];
    }else{
        return 0;
    }
}
``
## 考研重点考察题型，手动算出next数组
> **要点：**
	* next数组值为最长相同前后缀长度+1；
	* 传本身不能作为前后缀；
	* next[1]=0(下表根据具体题目而定)


