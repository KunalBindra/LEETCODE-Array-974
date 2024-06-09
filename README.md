# LEETCODE-Array-974
Sure, let's do a dry run of the `subarraysDivByK` method with a sample input to understand how it works. We'll trace each step and variable change.

Let's consider the input:
- `nums = [4, 5, 0, -2, -3, 1]`
- `k = 5`

Here is the code with additional comments for clarity:

```java
public class Solution {
  public int subarraysDivByK(int[] nums, int k) {
    int ans = 0;
    int prefix = 0;
    int[] count = new int[k];
    count[0] = 1;

    for (final int num : nums) {
      prefix = (prefix + num % k + k) % k;
      ans += count[prefix];
      ++count[prefix];
    }

    return ans;
  }
}
```

### Dry Run:

#### Initialization:
- `ans = 0`
- `prefix = 0`
- `count = [1, 0, 0, 0, 0]` (since `count[0] = 1`)

#### Iteration 1:
- `num = 4`
- `prefix = (0 + 4 % 5 + 5) % 5 = (0 + 4 + 5) % 5 = 9 % 5 = 4`
- `ans += count[4] = 0` (since `count[4] = 0`)
- `++count[4]` => `count = [1, 0, 0, 0, 1]`

#### Iteration 2:
- `num = 5`
- `prefix = (4 + 5 % 5 + 5) % 5 = (4 + 0 + 5) % 5 = 9 % 5 = 4`
- `ans += count[4] = 1` (since `count[4] = 1`)
- `++count[4]` => `count = [1, 0, 0, 0, 2]`

#### Iteration 3:
- `num = 0`
- `prefix = (4 + 0 % 5 + 5) % 5 = (4 + 0 + 5) % 5 = 9 % 5 = 4`
- `ans += count[4] = 2` (since `count[4] = 2`)
- `++count[4]` => `count = [1, 0, 0, 0, 3]`

#### Iteration 4:
- `num = -2`
- `prefix = (4 + (-2) % 5 + 5) % 5 = (4 - 2 + 5) % 5 = 7 % 5 = 2`
- `ans += count[2] = 0` (since `count[2] = 0`)
- `++count[2]` => `count = [1, 0, 1, 0, 3]`

#### Iteration 5:
- `num = -3`
- `prefix = (2 + (-3) % 5 + 5) % 5 = (2 - 3 + 5) % 5 = 4 % 5 = 4`
- `ans += count[4] = 3` (since `count[4] = 3`)
- `++count[4]` => `count = [1, 0, 1, 0, 4]`

#### Iteration 6:
- `num = 1`
- `prefix = (4 + 1 % 5 + 5) % 5 = (4 + 1 + 5) % 5 = 10 % 5 = 0`
- `ans += count[0] = 1` (since `count[0] = 1`)
- `++count[0]` => `count = [2, 0, 1, 0, 4]`

### Final Result:
- `ans = 1 (from iteration 2) + 2 (from iteration 3) + 3 (from iteration 5) + 1 (from iteration 6) = 7`

So, the method will return `7`.

### Explanation:
- The prefix sum modulo `k` keeps track of the running sum modulo `k`.
- The `count` array records the frequency of each possible modulo value.
- For each element in the array, the prefix sum modulo `k` is updated and used to find how many previous prefix sums have the same modulo value, indicating subarrays that sum to a multiple of `k`.
- By incrementing the corresponding count in the `count` array, we ensure that future prefix sums can also check against this current prefix sum.

This algorithm efficiently calculates the number of subarrays divisible by `k` by leveraging the properties of prefix sums and modular arithmetic.
