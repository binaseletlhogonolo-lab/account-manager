class AccountManager {
  constructor() {
    this.balances = {};
    this.history = {};
  }

  initUser(user) {
    if (!(user in this.balances)) {
      this.balances[user] = 0;
      this.history[user] = [];
    }
  }

  deposit(user, amount) {
    this.initUser(user);
    this.balances[user] += amount;
    this.history[user].push({ amount, time: Date.now() });
    return this.balances[user];
  }

  withdraw(user, amount) {
    this.initUser(user);

    // RULE 1: Not Enough Money
    if (this.balances[user] < amount) {
      return "Blocked: Not Enough Money";
    }

    // RULE 2: Too Fast (3 in 10 seconds)
    const now = Date.now();
    let count = 0;
    for (const transaction of this.history[user]) {
      if (now - transaction.time < 10000) {
        count++;
      }
    }
    if (count >= 3) {
      return "Blocked: Too Fast (Rapid Withdrawals)";
    }

    // RULE 3: Unusual Spike (5x average)
    if (this.history[user].length > 0) {
      const sum = this.history[user].reduce((a, b) => a + b.amount, 0);
      const average = sum / this.history[user].length;
      if (amount > average * 5) {
        return "Blocked: Unusual Spending Spike";
      }
    }

    // If all checks pass
    this.balances[user] -= amount;
    this.history[user].push({ amount, time: now });
    return this.balances[user];
  }

  transfer(fromUser, toUser, amount) {
    this.initUser(fromUser);
    this.initUser(toUser);

    const result = this.withdraw(fromUser, amount);
    if (typeof result === 'string' && result.includes('Blocked')) {
      return result;
    }

    this.deposit(toUser, amount);
    return this.balances[fromUser];
  }
}

module.exports = AccountManager;
