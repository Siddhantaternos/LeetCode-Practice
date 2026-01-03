Concatenation of Arrays

class Solution:
    def getConcatenation(self, nums):
        # nums is the input list
        # Example: nums = [1, 2, 1]

        # n stores the length of the input array
        # If nums = [1, 2, 1], then n = 3
        n = len(nums)

        # Create a new list 'ans' of size 2 * n
        # Initially filled with 0s
        # Here: ans = [0, 0, 0, 0, 0, 0]
        ans = [0] * (2 * n)

        # Loop through each index of the original array
        for i in range(n):
            # Place the element nums[i] at index i in ans
            # This fills the first half of ans
            # Example: ans[0] = nums[0] → 1
            ans[i] = nums[i]

            # Place the same element nums[i] at index i + n
            # This fills the second half of ans
            # Example: ans[0 + 3] = nums[0] → ans[3] = 1
            ans[i + n] = nums[i]

        # After the loop:
        # ans = [nums[0], nums[1], ..., nums[n-1],
        #        nums[0], nums[1], ..., nums[n-1]]

        # Return the final concatenated array
        return ans
