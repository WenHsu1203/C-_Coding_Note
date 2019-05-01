# Dynamic Programming

* Maximum Subarray [53]

```C++
int maxSubArray(vector<int>& nums) {
	int dp[nums.size()];
	int maxSub = nums[0];
	dp[0] = nums[0];
	for (int i = 1 ; i < nums.size(); i++) {
		dp[i] = nums[i] + (dp[i-1] > 0 ? dp[i-1]:0);
		maxSub = max(maxSub, dp[i]);
	}
	return maxSub;
}
```