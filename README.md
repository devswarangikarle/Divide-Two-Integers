# Divide-Two-Integers
Given two integers dividend and divisor, divide two integers without using multiplication, division, and mod operator.  The integer division should truncate toward zero, which means losing its fractional part. For example, 8.345 would be truncated to 8, and -2.7335 would be truncated to -2.  Return the quotient after dividing dividend by divisor.

class Solution:
    def divide(self, dividend, divisor):
        INT_MAX = 2**31 - 1
        INT_MIN = -2**31

        # Handle edge cases
        if divisor == 0:
            return INT_MAX
        if dividend == 0:
            return 0

        # Handle overflow cases
        if dividend == INT_MIN and divisor == -1:
            return INT_MAX

        # Determine the sign of the result
        sign = -1 if (dividend < 0) ^ (divisor < 0) else 1

        # Take the absolute values of dividend and divisor
        dividend, divisor = abs(dividend), abs(divisor)

        quotient = 0
        while dividend >= divisor:
            temp, multiple = divisor, 1
            while dividend >= (temp << 1):
                temp <<= 1
                multiple <<= 1

            dividend -= temp
            quotient += multiple

        return min(max(sign * quotient, INT_MIN), INT_MAX)

# Example usage:
sol = Solution()

dividend1, divisor1 = 10, 3
print(sol.divide(dividend1, divisor1))  # Output: 3

dividend2, divisor2 = 7, -3
print(sol.divide(dividend2, divisor2))  # Output: -2

dividend3, divisor3 = 2147483647, 1
print(sol.divide(dividend3, divisor3))  # Output: 2147483647

        
