ACCOUNT MANAGER - Step by Step

*1. WHAT THE SYSTEM STORES*

For every user, store two things:
- Balance: how much money they have
- History: list of all past transactions with amount and time

If a new user comes, create them with balance 0 and empty history.

*2. DEPOSIT MONEY*

Step 1: Check if user exists, if not, create them
Step 2: Add the amount to their balance
Step 3: Save this transaction in history with current time
Step 4: Return new balance

*3. WITHDRAW MONEY*

Step 1: Check if user exists
Step 2: *RULE 1 - Not Enough Money*
- If balance is less than amount you want to withdraw, STOP and block. Return "Not Enough Money"

Step 3: *RULE 2 - Too Fast*
- Get current time
- Look at history, count how many transactions happened in last 10 seconds
- If count is 3 or more, STOP and block. Return "Too Fast"

Step 4: *RULE 3 - Unusual Spike*
- If history is not empty, calculate average of all past transaction amounts
- Average = total of all past amounts divided by number of transactions
- If current amount is greater than average times 5, STOP and block. Return "Unusual Spending Spike"

Step 5: If none of the rules blocked:
- Subtract amount from balance
- Save transaction in history with current time
- Return new balance

*4. TRANSFER MONEY (From A to B)*

Step 1: Make sure both users exist
Step 2: Try to withdraw from first user - this will automatically check all 3 fraud rules
Step 3: If withdraw is blocked, stop the transfer and return the block message
Step 4: If withdraw succeeded, deposit the same amount to second user
Step 5: Return new balance of first user
