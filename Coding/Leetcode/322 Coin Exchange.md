### Description

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return _the fewest number of coins that you need to make up that amount_. If that amount of money cannot be made up by any combination of the coins, return `-1`.

You may assume that you have an infinite number of each kind of coin.

**Example 1:**

**Input:** coins = [1,2,5], amount = 11
**Output:** 3
**Explanation:** 11 = 5 + 5 + 1

**Example 2:**

**Input:** coins = [2], amount = 3
**Output:** -1

**Example 3:**

**Input:** coins = [1], amount = 0
**Output:** 0

**Constraints:**

- `1 <= coins.length <= 12`
- `1 <= coins[i] <= 231 - 1`
- `0 <= amount <= 104`

### Algorithm ([[Dynamic Programming]])

Use a bottom up approach where we calculate the min number of coins required from i to amount

1. sort the coins
2. create a map for `required_coins_for_each_num` and set 0 to 0 as it take 0 coins to get to 0 amount
3. outer loop i to amount
4. inner loop over the coins
5. find the diff = i - coin
	1. if the diff is negative, break out of the inner loop as there are no more coins that are small enough
	2. else find the min coins it takes to reach the diff by doing `required_coins_for_each_num[diff]` + 1 (to account for the current coin)

Gotchas

1. when iterating over the coins, if we find a -1 in the `required_coins_for_each_num`, continue the loop rather than breaking 
	1. this just signifies that the number that we are iterating over can not possibly be used to find the current amount
2. 

### Solution

```
# time - O(a * c) where a is the amount and c is the number of coins since we are for looping from 1 to amount  
#               and iterating up to all coins  
# space - O(a) where a is the amount since we are creating a map of sums from i to a  
class Solution:  
  
    #  
    #  coins = [1, 6, 7, 9] , amount = 13    
    #    
    #  min_coins_for_this_sum = { 0: 0 }    
    #                           { 1 : 1 } 1 is in the array    
    #                           { 2 : 2 } 2 1's    
    #                           { 3 : 3 } 3 1's    
    #                           { 4 : 4 } 4 1's    
    #                           { 5 : 5 } 5 1's    
    #                           { 6 : 1 } 6 is in the array    
    #                           { 7 : 1 } 7 is in the array    
    #                           { 8 : 2 } 8 - 7 coin == 1. 1 is mapped to 1. 1 + 1    
    #                           { 9 : 1 } 9 is in the array    
    #                           { 10: 2 } 10 - 9 count == 1. 1 is mapped to 1, 9 to 1. 1 + 1    
    #                           { 11: 3 } 11 - 9 count == 2. 2 is mapped to 2, 9 to 1. 2 + 1 = 3    
    #                           { 12: 2 } 12 - 6 count == 6. 6 is mapped to 1. 1 + 1 = 2    
    #                           { 13: 2} 13-6 count == 7. 7 is mapped to 1, 6 to 1. 1 + 1 = 2    
    #    def coinChange(self, coins: List[int], amount: int) -> int:  
	# build the min sums bottom up starting at 0  
    #    i.e. it takes 0 coins to get 0 amount        
    # outer loop to calculate bottom up sums including 0        
    # loop over the coins        
    # take the sum we are currently on and subtract from each coin        
    #     if that sum is negative, break out of the loop        
    #     if the sum is positive, get the value from our array and add 1 for this coin  
        sorted_coins = sorted(coins)  
        required_coins_for_each_num = { 0: 0 }  
  
    # calculate min required for each num up until amount  
    # i.e. calculate min sum required for target of 0,1,2,3,4 until amount        for target in range (1, amount + 1):  
            # this is essentially Int.max  
            min_coins_required = target + 1  
            # loop through coins  
            for coin in sorted_coins:  
                diff = target - coin  
                if diff >= 0:  
                    # the required value is missing (-1)  
                    if required_coins_for_each_num[diff] < 0:  
                        continue  
                    curr_min = 1 + required_coins_for_each_num[diff]  
                    min_coins_required = min(min_coins_required, curr_min)  
                else:  
                    break  
            if min_coins_required == target + 1:  
                required_coins_for_each_num[target] = -1  
            else:  
                required_coins_for_each_num[target] = min_coins_required  
        return required_coins_for_each_num[amount]
```

