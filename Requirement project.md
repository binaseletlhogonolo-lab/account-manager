Account Manager Algorithm 

Your app does 3 main things: Track funds, Transfer, Withdraw.

*Algorithm is step-by-step logic:*

*1. DEPOSIT Algorithm:*
- Start
- Get username and amount
- Check if amount is valid ( > 0 )
- If user doesn't exist, create new user with 0 balance
- Add amount to user balance
- Save transaction in history with time
- Show success message
- End

*2. WITHDRAW Algorithm:*
- Start
- Get username and amount
- Check if amount is valid
- Check if user exists
- Check if user has enough balance
- *Check fraud rules:* 
    - Count withdrawals in last 10 seconds
    - If > 3, Block - Too Fast
    - If withdrawal amount > 3x last deposit, Block - Suspicious
- If blocked, show red error, don't change balance
- If not blocked, subtract amount from balance
- Save transaction in history
- Show success
- End

*3. TRANSFER Algorithm:*
- Start
- Get fromUser, toUser, amount
- Check both users exist and amount valid
- Check fromUser has enough money
- Check fraud rules for fromUser
- If blocked, show error
- If not blocked:
    - Subtract from fromUser
    - Add to toUser
    - Save 2 history records
- Show success
- End

*Overall System:*
- Maintain list of balances
- Maintain list of all transactions with timestamp
- Every action goes through validation -> fraud check -> update

   End
