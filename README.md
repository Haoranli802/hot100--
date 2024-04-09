# hot100--note

LC49字母异位词：
O(NKlogK) K is the largest string in strs
O(nk)
具体思路，我们可以吧每个字符串转成字符组，然后排序得到一个共同的字符串，然后用Map把所有拥有
相同排序字符串的字符串组合起来，然后最后用List加入map的value即可。
