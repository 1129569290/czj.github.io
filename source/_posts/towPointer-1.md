---
title: towPointer-1
date: 2020-08-06 14:51:31
tags:
categories:
- 算法题
- twoPointer
---
## 保留k个元素Leetcode26,80

就是给定一个排序好的数组，做删除操作，保留每个数字最多只出现了k次，返回新数组的长度</br>
必须原地操作

### 思路

双指针，用back来标定新数组的结尾位置，那么back肯定要初始化为k-1</br>
back-k+1来进行标定新数组最后一个元素的开始位置,
从index位置开始枚举 新元素与nums[back-k+1]做比较，如果不同则加入</br>

## Leetcode75颜色分类

```cpp
//i用来遍历数组，会保证[0~j)都是0,[j,i)都是1,[i,end)都是2
    void sortColors(vector<int>& nums) {
        for(int i = 0, j = 0, k = nums.size() - 1; i <= k; ){
            if(nums[i] == 0)swap(nums[i++], nums[j++]);
            else if(nums[i] == 2)swap(nums[k--], nums[i]);
            else i++;
            cout<<"i:"<<i<<"   j:"<<j<<"    k:"<<k<<endl;
        }
    }



```

## 三数之和 Leetcode15

枚举每个数字，找其他两个数

```cpp

class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        if(nums.size()<3)return {};
        vector<vector<int>>res;
        sort(nums.begin(),nums.end());
        for(int i=0;i<nums.size()-2;i++){
            if(nums[i]>0)break;                      //去重
            if(i==0||(i>0&&nums[i-1]!=nums[i])){     //去重
                int c=-nums[i];
                int j=i+1,k=nums.size()-1;
                while(j<k){
                    if(nums[j]+nums[k]==c){
                        res.push_back({nums[i],nums[j],nums[k]});
                        while(j<k&&nums[j+1]==nums[j])j++;//关键去重 类似情况 -1 0 0 1 1
                        while(j<k&&nums[k]==nums[k-1])k--;
                        j++,k--;
                    }
                    else if(nums[j]+nums[k]>c)k--;
                    else j++;

                }
            }
        }
        return res;
    }
};
```

## 四数之和

和上面一个一样，关键是过滤相同的过程

```cpp
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        if(nums.size() < 4)return {};
        sort(nums.begin(), nums.end());
        vector<vector<int>> res;
        for(int i = 0; i < nums.size() - 3 ; i++){
            if(i == 0 || (i > 0 && nums[i] != nums[i-1]) ) {
                for(int j = i+1; j < nums.size() - 2; j++){
                    if( j == i+1 || ( j > i+1 && nums[j] != nums[j-1])){
                        int tmp = target - ( nums[i] + nums[j] );
                        int l = j+1, r= nums.size() - 1 ;
                        while(l < r){
                            int sum = nums[l] + nums[r];
                            if(sum == tmp){
                                res.push_back({nums[i], nums[j], nums[l], nums[r]});
                                while(l < r && nums[l] == nums[l+1])l++;
                                while(l < r && nums[r] == nums[r-1])r--;
                                l++, r--;
                            }
                            else if(sum > tmp) r--;
                            else l++;
                        }
                    }
                }
            }
        }
        return res;
    }
};

```

## 最接近的三数之和 LeetCode16

从一个数组里面求出三和元素的和， 和给定的target距离最近

### 思路

如果单纯上来就枚举，因为三个数，所以时间复杂度n^3
先排序（O(nlogn)），枚举每个元素， 对后面的元素进行双指针遍历(n^2),得到一个sum与res比较

```cpp
int threeSumClosest(vector<int>& nums, int target) {
        sort(nums.begin(), nums.end());
        int res = nums[0] + nums[1] + nums[2];
        for(int i = 0; i < nums.size()-2; i++){
            int l = i + 1,r = nums.size() - 1;
            while( l < r ){
                int sum = nums[i] + nums[l] + nums[r];
                if (abs(sum - target) < abs( res - target ))
                    res = sum;
                if(sum > target)
                    r-- ;
                else if(sum < target)l++;
                else return sum;
            }
        }
        return res;
    }
```
