# hot100--note

哈希：

LC49字母异位词：
O(NKlogK) K is the largest string in strs，O(nk)

具体思路，我们可以吧每个字符串转成字符组，然后排序得到一个共同的字符串，然后用Map把所有拥有相同排序字符串的字符串组合起来，然后最后用List加入map的value即可。

***

LC128最长连续序列：

O(N), O(N)

思路：用map或者set给数组去重，因为重复的不考虑，然后遍历map或者set里面的数字，如果包含比此数字小一的数字，那么代表无需重复遍历此数字。如果不包含，那么持续找比此数字大一的数字，然后保存最大的连续上升长度。

***

双指针

LC42接雨水 Hard：

第一种解法，用栈来找出雨水的数量。首先设置栈，设置起始点为0然后遍历height，如果当前高度比栈顶的高度小，那么把当前高度推入栈。如果当前高度比栈顶大，那么弹出栈顶，如果栈里空了，那么代表是边界，不做考虑。如果不为空，那么代表找到有雨水的地方。首先先把弹出栈顶，也就是最低点的高度标记。然后找到现在栈顶和目前高度的最小值，也就是能装雨水的高度。然后找出宽度，也就是当前数标减去栈顶数标再减去一。然后乘起来加入和中。

O(N) 每个长度只会进出栈一次, O(N)栈空间不会超过N

第二种解法：左右指针，设置左右指针，然后保存左右的最大值，开启while循环，先更新最大值，注意边界不能装雨水。更新完最大值以后，如果左指针的最大值小比右指针的最大值小，那么代表左指针的右边有一个高度比左指针左边所有高度都要高，那么就用左指针的最大高度减去当前左指针高度就能得到能接的雨水。同时更新左指针位置反之，如果右指针最大值比左指针小，那么就用右指针最大值减去当前右指针高度即可。同时更新右指针位置。

O（N），O（1）

***

滑动窗口

LC3无重复最长子串

具体思路，用哈希表存入字符下标，用lastIndex来储存滑动窗口左边界，然后滑动右边界，把遍历到的字符下标更新到Map直到滑动到有重复的位置，更新最左边界为最左边界和当前字符前一次出现的地方的最大值。同时一直更新最长长度，直到遍历结束。

O(N), O(26)

***

LC438找到字符串中所有字母异位词

具体思路：创造两个数组哈希表，然后吧p包含的单词和s中p长度包含的单词输入哈希表，然后用Arrays.equals对比两个哈希表，如果相同，那么代表是异位字符串，加入下标。然后从p的长度开始遍历s，用哈希表模拟滑动窗口把新入的加上，减去窗口外的，然后对比两个哈希表，如果相等的话，把下标减去p长度加一加入结果。

O(M + (N - M * 26)), O(26)

***

LC560和为K的子数组

具体思路：前缀和解法，用一个哈希表来存前缀和和数量，先把(0, 1)存入防止第一个数字就满足条件但是找不到前缀。然后遍历数组，把sum加上当前的数字，如果当前数字减去target的值在前缀里面，那么代表找到一个满足的组合。结果加上前缀和数量，然后吧当前sum作为下一个数字的前缀加上。

O(N), O(N)

***

LC76最小覆盖子串

具体思路为：用一个map记录T出现的字符和数量，然后用滑动窗口遍历S，先走右指针，找到满足所有字符出现数量的终点，然后走左指针找到最短满足字符串。然后记录最短字符串，然后设置左指针为下一个字符，继续查找。维护一个need变量来记录还需要找到的字符数量。为了方便维护，所有与T不相关的字符也会被存入map，赋值为-1。

最多扫描两次S，所以时间复杂度为O(N)，空间复杂度为O(K)，K为S和T中的字符数集合。

***

数组

LC238除自身以外数组的乘积

具体思路：创立ans数组，ans[i]目前表示出了i以外i左边的所有乘积。ans[0] = 1因为第一个数字的乘积就是1，从下标1开始遍历数组，找到所有数字左边的乘积。然后设置temp = 1，temp为数字右边的乘积，然后从右到左找到数字右边的乘积再乘以数字左边的乘积得出最后答案。

LC41缺失的第一个正整数

具体思路：
我们想找缺失的正整数，那么我们就要让所有的正整数都在他对应的位置上，比如1就应该下标0处，因为第一个正整数就是1，然后2在下标1中，以此类推。这道题目不允许我们使用额外空间，那么最好的办法就是原地哈希。遍历数字，如果当前数字在1到数组长度的范围中，那么我们就可以原地哈希给他找到对应位置。原地哈希的办法就是把当前数字和对应位置数字交换。注意如果本来就在对应位置上，那么就不用交换。注意要用while loop来交换，因为交换过来的数字可能也需要原地hash重新找到位置。全部遍历完之后，重新遍历数组，找到第一个不对应下标的数字，返回下标加一即可。

O(N)虽然有while loop但是我们的限制确定了每个数字只会被遍历到一次， O(1)

***

矩阵

LC73矩阵置零

O(NM), O(1), in place算法，用数组的第一行和第一列来记录哪一行和哪一列需要被覆盖0。同时先要记录第一行和第一列有没有0以便于最后覆盖第一行和第一列。

***

二叉树

LC543二叉树直径

具体思路：用树形dp解决，一个节点的最大直径就是这个节点左右的最大深度相加。然后这个节点的最大深度就是左右最大深度的最大值加一。

O(N), O(H)

LC437路径总和III

具体思路：用一个前缀表来记录当前节点之前的路径和，如果找到符合(当前节点长度减去目标值等于表里的某一个值)那么代表有一条路线是target为长度的。那么加上表里此前缀的值。然后更新前缀表，遍历左右节点然后把左右节点的结果也加上，注意遍历完当前节点之后，要回溯表里前缀的值避免不是同一条路线的节点错误加上。最后返回结果即可。

O(N), O(H)

***

图论

LC994腐烂的橘子

具体做法：bfs，先遍历第一遍数组，把新鲜橘子的数量记着，然后吧腐烂的橘子放入队列。然后每次对同一批烂橘子进行bfs搜索，查找这一轮可以感染的新鲜橘子，减去数量，标记为烂橘子，然后放入队列。不断深搜知道新鲜橘子数量为0或者队列为空，如果新鲜橘子数量不为0，那么代表有橘子永远没被感染。如果为0，那么返回感染的轮数。

O(NM), O(NM)

LC207课程表

首先先记录所有课程的进度表，然后记录每个点的出度点，然后找到进度为0的点，加入队列。然后进行bfs拓扑排序。拓扑排序就是找到进度为0的点，然后找到他们的出点，把出点的入度减一，这是代表parent已经处理完毕。如果有新的入度为0的点，那么加入到队列，遍历直到队列为空。然后返回剩余的课程数量，如果为0代表可以满足。

O(n + m) n = num of courses, m = num of prerequisites， O(n + m)

***

回溯

LC79单词搜索

O(MN3^L)因为每次最差要判断三次，L是目标单词长度。O(MN)

具体思路：dfs + 回溯剪枝。每个点进行dfs查找是否满足当前字母等于目标字符串对应的下标字母，如果是的话把当前字母设为一个阻挡字母避免路线往回走，然后dfs剩下的方向，最后把当前字母设置回来。直到找到满足长度的字符串，返回true，不然返回false。

***

二分查找

模版

```
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0, right = nums.length - 1; // 注意
        while(left <= right) { // 注意
            int mid = (left + right) / 2; // 注意
            if(nums[mid] == target) { // 注意
                // 相关逻辑
            } else if(nums[mid] < target) {
                left = mid + 1; // 注意
            } else {
                right = mid - 1; // 注意
            }
        }
        // 相关返回值
        return 0;
    }
}
```

LC35搜索插入位置

具体思路：二分查找模版题，但是注意最后返回的时候返回left，证明如下：

      *  以上while循环中，若找到了target直接返回

      *  当原数组不包含target时，考虑while循环最后一次执行的总是 left=right=mid,

      *  此时nums[mid] 左边的数全部小于target，nums[mid]右边的数全部大于target,

      *  则此时我们要返回的插入位置分为两种情况：

      *  ①就是这个位置，即nums[mid]>target时，此时执行了right=mid-1，返回left正确

      *  ②是该位置的右边一个，即nums[mid]<target时，此时执行了left=mid+1,返回left也正确

***

LC33搜索旋转数组

具体思路：跟二分查找类似，当mid == target的时候，直接返回。然后就要确认mid是数组的左段还是右段了，如果最左值小于等于mid，那么代表mid在左段，反之在右段。如果在左段，判断target在不在左段中，如果在那么缩小右边界，如果不在缩小左边界。如果在右段，判断target在不在右段中，如果在缩小左边界，如果不在缩小右边界。最后如果一直找不到返回-1.

***

LC4寻找两个有序数组的中位数

```
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int n = nums1.length;
        int m = nums2.length;
        //如果是奇数长度，那么leftM == rightM，如果不是的话，那么就需要找leftM和rightM的平均值了。
        int leftM = (n + m + 1) / 2;
        int rightM = (n + m + 2) / 2;
        return (getKth(nums1, 0, n - 1, nums2, 0, m - 1, leftM) + getKth(nums1, 0, n -1, nums2, 0, m - 1, rightM)) * 0.5;
    
    } 
    private int getKth(int[] nums1, int start1, int end1, int[] nums2, int start2, int end2, int k){
        //首先判断数组1和数组2的剩余长度
        int len1 = end1 - start1 + 1;
        int len2 = end2 - start2 + 1;
        //要把最短的数组放到前面，这样如果有一个数组长度为0的话那么一定是前面的那个数组。
        if(len1 > len2) return getKth(nums2, start2, end2, nums1, start1, end1, k);
        //如果有数组长度为0，就直接找剩余数组第k大的数字即可
        if(len1 == 0){
            return nums2[start2 + k - 1];
        }
        //如果k只剩一，那么只需要找一个数组，就比对数组1和数组2的当前数字即可。
        if (k == 1) return Math.min(nums1[start1], nums2[start2]);
        //如果k/2大于数组长度，那么就用数组长度
        int i = start1 + Math.min(len1, k / 2) - 1;
        int j = start2 + Math.min(len2, k / 2) - 1;
        //如果数组1第k大的数大于数组2第k大的数，那么就舍去数组2的前k个数，然后更新舍去的k的数量
        if(nums1[i] > nums2[j]){
            return getKth(nums1, start1, end1, nums2, j + 1, end2, k - (j - start2 + 1));
        }
        else{
            return getKth(nums1, i + 1, end1, nums2, start2, end2, k - (i - start1 + 1));
        }
    }  
}
```

***

单调栈

LC84最大矩形面积

1.单调栈做法
首先我们要设置一个新的数组，就是原数组收尾加上0，来用于边界的判断。然后我们创建一个stack，把0也就是边界加入stack，然后开始遍历，如果遍历到当前高度小于栈顶高度，那么我们就找到了一个矩形的右边界，这时候我们把栈顶弹出，栈顶就是这个矩形的基准高度。然后找这个矩形的左边界，也就是新的栈顶，计算出宽度，然后用高度乘与宽度计算出矩形面积，然后更新最大值。如果新的高度还是小于栈顶，继续判断直到边界，然后把新的高度弹入栈，遍历下一个高度直到边界。

O(N), O(N)

2.双指针

双指针：建立两个数组分别保存当前高度最左边的第一个比它小的高度和当前高度右边第一个比它小的高度。初始的时候左边第一个高度比它小的设为-1，然后右边第一个高度比它小的设为数组长度，方便后面计算。然后遍历高度数组，根据左右第一个比它小的高度算出宽度，更新最大矩形面积即可。

O(N), O(N)

***

堆

LC215数组中第K大的元素

第一种办法，使用小顶堆，具体算法如下，维护一个长度为k的优先队列，数组比较方式为小顶堆。然后放入数字当放入数字时，队列长度大于k时，判断当前数字是否比队列顶部数字要大，如果大的话，那么弹出顶部，然后放入当前数字。最后队列的头部就是第k大的数字。返回即可。

O(nlogk), O(k)

第二种办法，快排之快速选择

快速选择，用一个随机数来确定哨兵，然后把每个数组化为三个区间(最好用ArrayList，方便操作计算)，大于哨兵，等于哨兵和小于哨兵。然后再根据k的值判断k在哪个数组里面，如果在大于或者小于里面，那么接着快排，如果在等于里面，那么返回哨兵。

O(N)，复杂度为(2N - 1) 所以平均情况下复杂度为O(N)， O(logN) 递归深度为logN

***

LC347前k个高频数组

第一种办法，直接用优先队列模拟最小堆，返回优先队列里面所有的值即可。

O(NlogK), O(K)

第二种办法，桶排序

桶排：首先先把值和出现频率放入哈希表。然后创建一个数组，每个数组都是一个list，将频率作为数组下标把频率对应的值存入下标里的list即可。然后反向遍历频率list，加入结果数组返回。

O(N), O(N)
