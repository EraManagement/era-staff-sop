# gPhone ATM Banking SOP

The gPhone ATM app lets players check balance, deposit cash, withdraw cash, withdraw all, and transfer ATM funds to another account. The client UI is in `classes/gui_phone_atm.gs2`; server-side money movement is in `weapons/Phones%2FATMPhone.gs2`.

## Player Actions

The ATM app supports:

- Balance refresh
- Deposit
- Withdraw
- Withdraw all
- Transfer to account or community name

Every action refreshes the displayed ATM balance after the server responds.

## Server Actions

Phone ATM actions are handled by `handleServerAction()`:

- `refreshATM`
- `phoneATMDeposit`
- `phoneATMWithdraw`
- `phoneATMWithdrawAll`
- `phoneATMCheckTransferAccount`
- `phoneATMTransfer`

## Deposits

Deposits move cash on hand into the player's bank balance.

Validation includes:

- Amount must be at least `$1`.
- Player must have enough cash on hand.
- Player cannot deposit while playing Poker.
- The script checks that cash actually decreased after removing it.

Successful deposits:

- Subtract from `player.rupees`
- Add to `DB_Bank` balance
- Log to `bankatm`
- Log to `atmlog.txt`

Large or suspicious exact-balance deposits can also log to `potential_atm.txt` and notify NC.

## Withdrawals

Withdrawals move bank balance into cash on hand.

Validation includes:

- Amount must be at least `$1`.
- Player must have enough bank balance.
- Cash on hand after withdrawal must stay under the hard cap check of `$3,670,015`.

Successful withdrawals:

- Add to `player.rupees`
- Subtract from `DB_Bank`
- Set `player.clientr.lastWithdraw`
- Log to `bankatm`
- Log to `atmlog.txt`

`Withdraw All` uses the full bank balance and sets the bank balance to zero if the cash cap check passes.

## Transfers

Transfers move bank balance from the sender to another account.

Validation includes:

- Sender cannot transfer to self.
- Target account must resolve through `Control_Accounts.getAccount()`.
- Target must have a bank account.
- Target cannot be trade-locked.
- Sender cannot be a new player.
- Amount must be at least `$1`.
- Sender must have enough ATM balance.

Successful transfers:

- Add to target bank balance.
- Subtract from sender bank balance.
- Log sender and receiver `bankatm` entries.
- Notify online receiver with an `addMessage()`.
- Send Bank of Era mail notifications to both sender and receiver.
- Log to `atmlog.txt`.
- Log transfers over `$750,000` to `atmlog_bigxfers.txt`.

## Staff Review Notes

For bank disputes, check:

- Player `bankatm` logs
- `atmlog.txt`
- `atmlog_bigxfers.txt` for large transfers
- Bank of Era mail notifications
- Current DB_Bank balance

Do not trust screenshots of the phone balance alone. The phone display is refreshed from the server, but the authoritative value is the bank balance server-side.

## Source Reference

- `weapons/Phones%2FATMPhone.gs2`
- `classes/gui_phone_atm.gs2`
- `classes/bank_functions.gs2`
- `npcs/DB_Bank.gs2`
