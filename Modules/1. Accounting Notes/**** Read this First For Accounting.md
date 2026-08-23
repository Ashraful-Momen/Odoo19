একদম জীবনে না ভোলার মতো সহজভাবে বুঝাই। Odoo/Accounting-এর সবচেয়ে বড় ভয় “Debit/Credit” — আসলে এটা + / - না, এটা কোন পাশে লিখছো সেটার নাম।

### ১. Accounting-এর মূল সমীকরণ

Asset = Liability + Equity

বাংলায়:

* Asset = ব্যবসার যা আছে (Cash, Bank, Stock, Computer)

* Liability (L) = অন্যের কাছে দেনা (Loan, Payable)

* Equity (E) = মালিকের টাকা

ধরো:

| Asset         | Amount |
| ------------- | ------ |
| Cash          | $1,000 |
| Total Asset   | $1,000 |
| Owner Capital | $1,000 |
| Total L+E     | $1,000 |

সমীকরণ ঠিক আছে।

### ২. Debit/Credit আসলে কী?

ভাবো প্রতিটি account-এর দুইটা কলাম আছে:

Debit (Dr)

Credit (Cr)

বাম পাশ

ডান পাশ

Debit = Left side Credit = Right side

এটাই আসল সংজ্ঞা। Debit মানেই + না, Credit মানেই - না।

কোন account-এ কোন পাশ বাড়ে সেটা মুখস্থ করতে হয়।

### ৩. সবচেয়ে গুরুত্বপূর্ণ টেবিল (এটা মুখস্থ করো)

| Account Type | Increase | Decrease |
| ------------ | -------- | -------- |
| Asset        | Debit    | Credit   |
| Expense      | Debit    | Credit   |
| Liability    | Credit   | Debit    |
| Equity       | Credit   | Debit    |
| Income       | Credit   | Debit    |

এক লাইনে মনে রাখো:

* Asset/Expense বাড়লে Debit

* Liability/Equity/Income বাড়লে Credit

### ৪. কেন এমন?

### উদাহরণ ১: মালিক টাকা দিল

মালিক ব্যবসায় $1,000 দিল।

ব্যবসার Cash বাড়ল → Asset বাড়ল → Debit

মালিকের Capital বাড়ল → Equity বাড়ল → Credit

```
Cash.............Dr 1,000
    Owner Capital.....Cr 1,000
```

সমীকরণ:

* Asset = 1,000

* Equity = 1,000

ঠিক আছে।

### উদাহরণ ২: ব্যাংক ঋণ নিল

ব্যাংক থেকে $500 ঋণ নিলে:

* Cash বাড়ল → Debit

* Loan বাড়ল → Credit

  Cash.............Dr 500
  Bank Loan.........Cr 500

এখন:

* Asset = 1,500

* Liability = 500

* Equity = 1,000

মোট = 1,500 ✔️

### উদাহরণ ৩: অফিস ভাড়া দিল

ভাড়া $100 নগদে দিল।

* Rent Expense বাড়ল → Debit

* Cash কমল → Credit

  Rent Expense.....Dr 100
  Cash..............Cr 100

Cash কমে গেল, তাই Asset কমাতে Credit।

### ৫. “Debit = +” কখন মনে হয়?

কারণ Asset account-এ Debit দিলে balance বাড়ে। তাই অনেকেই ভাবে Debit মানেই plus।

কিন্তু Loan account-এ দেখো:

Loan শুরু 0।

* Credit 500 → balance 500

* Debit 200 → balance 300

এখানে Credit বাড়িয়েছে। তাই Debit/ Credit কখনো universal plus-minus না।

### ৬. Odoo account type কেন গুরুত্বপূর্ণ?

Odoo-তে প্রতিটি account-এর একটা Account Type থাকে। যেমন:

| Odoo Account Type   | বাস্তব অর্থ |
| ------------------- | ----------- |
| Receivable          | Asset       |
| Payable             | Liability   |
| Bank                | Asset       |
| Cash                | Asset       |
| Current Assets      | Asset       |
| Current Liabilities | Liability   |
| Income              | Income      |
| Expenses            | Expense     |
| Equity              | Equity      |

Odoo এই type দেখে বুঝে:

* balance কোন পাশে স্বাভাবিক,

* Balance Sheet-এ কোথায় দেখাবে,

* Profit & Loss-এ যাবে কি না,

* aged receivable/payable রিপোর্টে আসবে কি না।

### ৭. Journal কেন Debit/Credit নেয়?

Journal হলো transaction log। প্রতিটি transaction-এ কমপক্ষে দুইটা account লাগে।

ধরো Customer cash দিয়ে পণ্য কিনল $200।

### Odoo Journal Entry

| Account        | Debit | Credit |
| -------------- | ----- | ------ |
| Cash (Asset)   | 200   | 0      |
| Sales (Income) | 0     | 200    |
| Total          | 200   | 200    |

Odoo বাধ্য করে:

∑Debit=∑Credit

এতে সমীকরণ সবসময় ব্যালান্স থাকে।

### ৮. Odoo Journal Types সহজভাবে

| Journal Type  | কাজ                  |
| ------------- | -------------------- |
| Sales         | Customer invoice     |
| Purchase      | Vendor bill          |
| Bank          | Bank transaction     |
| Cash          | Cash transaction     |
| Miscellaneous | Manual journal entry |

Journal type মূলত UI ও workflow ঠিক করে; debit/credit rule বদলায় না।

### ৯. Invoice-এ Odoo নিজে কী entry করে?

ধরো তুমি $500 invoice করলে।

### Customer Invoice Post

| Account             | Debit | Credit |
| ------------------- | ----- | ------ |
| Accounts Receivable | 500   | 0      |
| Sales Revenue       | 0     | 500    |

Customer এখন তোমাকে টাকা দেবে, তাই Receivable (Asset) বেড়েছে → Debit।

### ১০. Payment পেলেই কী হয়?

Customer টাকা দিল $500।

| Account             | Debit | Credit |
| ------------------- | ----- | ------ |
| Bank                | 500   | 0      |
| Accounts Receivable | 0     | 500    |

Bank বাড়ল → Debit Receivable কমল → Credit

### ১১. Laravel mindset দিয়ে ১০ সেকেন্ডে চিনো

ভাবো account balance stored আছে।

### Asset account

PHP

```
// Cash account
balance += debit;
balance -= credit;
```

### Liability account

PHP

```
// Loan account
balance += credit;
balance -= debit;
```

Accounting software ভিতরে প্রায় এই logic-ই ব্যবহার করে।

### ১২. সবচেয়ে সহজ mnemonic

D

DEA

Debit increases Expense and Asset

C

CLI

Credit increases Liability, Income, and owner’s equity (Capital)

DEA → Debit CLI → Credit

এটা মনে থাকলে ৮০% accounting শেষ।

### ১৩. ৩০ সেকেন্ড টেস্ট

* Cash বাড়ে → Debit ✔️

* Bank Loan বাড়ে → Credit ✔️

* Sales বাড়ে → Credit ✔️

* Salary Expense বাড়ে → Debit ✔️

* Accounts Payable কমে → Debit ✔️

* Owner Capital কমে → Debit ✔️

সব ঠিক হলে তুমি debit/credit-এর মূল ধারণা ধরে ফেলেছ।

### শেষ কথা

Debit/Credit = Left/Right side Plus/Minus নয়।

Odoo account type বলে দেয় কোন account স্বাভাবিকভাবে Debit balance নাকি Credit balance বহন করবে। Journal entry-এর উদ্দেশ্য হলো প্রতিটি transaction-এ এমন দুই পাশ লেখা যাতে Total Debit = Total Credit থাকে এবং Asset = Liability + Equity সমীকরণ কখনো ভাঙে না।


===================== Main Note for Dr/Cr ================================

এটাই সবাই প্রথমে কনফিউজ হয়। কারণ সবাই **DAE/LIC মুখস্থ করে**, কিন্তু **কোন account কোন group-এ পড়ে** সেটা শেখে না।

আমি তোমাকে একটা **বাস্তব ব্যবসা (Shop/Company)** দিয়ে বুঝাই।

---

# Step 1: প্রথমে প্রশ্ন করো

যে জিনিসটা দেখছো সেটা কি?

```
এটা কি আমার?
নাকি
অন্যের?
নাকি
আমি খরচ করলাম?
নাকি
আমি আয় করলাম?
```

এই ৪টা প্রশ্নের উত্তর দিলেই Debit/Credit বের হয়ে যাবে।

---

# Step 2: Account Classification

## 🟢 A = Asset (আমার যা আছে)

যদি কোম্পানির **কোনো কিছু থাকে**, তাহলে Asset।

উদাহরণ

```
Cash
Bank
Petty Cash
Inventory (Stock)
Furniture
Computer
Laptop
Vehicle
Building
Land
Accounts Receivable
Advance to Supplier
Prepaid Rent
```

এগুলো সব **DAE**

অর্থাৎ

```
Increase = Debit
Decrease = Credit
```

---

## 🔴 L = Liability (অন্যের টাকা)

যদি **অন্যের কাছে আমার দেনা থাকে**

```
Loan
Bank Loan
Accounts Payable
VAT Payable
Salary Payable
Tax Payable
Customer Advance
```

এগুলো **LIC**

```
Increase = Credit
Decrease = Debit
```

---

## 🟡 E = Equity

Owner-এর টাকা

```
Capital
Owner Equity
Retained Earnings
Current Year Earnings
```

সব **LIC**

---

## 🔵 I = Income

যখন ব্যবসা টাকা **উপার্জন করে**

```
Sales
Service Revenue
Consulting Income
Interest Income
Commission Income
Rental Income
```

সব **LIC**

---

## 🟠 E = Expense (Cost)

এখানেই সবাই ভুল করে।

**যা খরচ হয়, সব Expense।**

যেমন

```
Salary Expense
Rent Expense
Electricity Bill
Gas Bill
Internet Bill
Fuel Expense
Marketing Expense
Office Expense
Stationery
Software Subscription
Hosting Cost
AWS Cost
Google Cloud Cost
Facebook Ads
Google Ads
Travel Expense
Repair Expense
Food Expense
Tea Expense
Courier Expense
Printing Expense
Telephone Expense
Insurance Expense
Depreciation Expense
```

সব **DAE**

```
Increase = Debit
Decrease = Credit
```

---

# তাই Cost গুলো সব Debit?

**হ্যাঁ।**

যদি Expense বাড়ে

➡ Debit

---

ধরো

Office Rent = $500

```
Rent Expense      Dr 500
Cash                   Cr 500
```

Rent Expense বাড়ছে

⇒ Debit

Cash কমছে

⇒ Credit

---

Salary দিলে

```
Salary Expense    Dr 1000
Cash                  Cr 1000
```

---

Electricity Bill

```
Electricity Expense Dr
Cash                 Cr
```

---

Internet Bill

```
Internet Expense Dr
Cash              Cr
```

---

AWS Bill

```
Cloud Expense Dr
Bank          Cr
```

---

# তাহলে Credit কবে হবে?

যখন

```
Loan বাড়বে

Sales হবে

Capital বাড়বে

Customer Advance আসবে

Payable বাড়বে
```

---

# একটা Shortcut

যদি **টাকা বের হয়**

সাধারণত

```
Expense Dr
Cash Cr
```

---

যদি **টাকা আসে ব্যবসায়**

সাধারণত

```
Cash Dr
Income Cr
```

---

যদি **Loan পাও**

```
Cash Dr
Loan Cr
```

---

যদি **কম্পিউটার কিনো**

```
Computer Dr
Cash Cr
```

কারণ Computer হলো Asset।

---

# Odoo-তে Account Type দেখলেই বুঝবে

| Odoo Account Type       | DAE না LIC? |
| ----------------------- | ----------- |
| Current Assets          | ✅ DAE       |
| Fixed Assets            | ✅ DAE       |
| Bank                    | ✅ DAE       |
| Cash                    | ✅ DAE       |
| Receivable              | ✅ DAE       |
| Current Liabilities     | ❌ LIC       |
| Non-current Liabilities | ❌ LIC       |
| Payable                 | ❌ LIC       |
| Equity                  | ❌ LIC       |
| Income                  | ❌ LIC       |
| Expense                 | ✅ DAE       |

---

## জীবনে না ভোলার ট্রিক 🚀

একটা কোম্পানি কল্পনা করো।

**যা কোম্পানির কাছে আছে → DAE**

* Cash
* Bank
* Laptop
* Inventory
* Furniture

**যা কোম্পানি খরচ করেছে → DAE**

* Salary
* Rent
* Electricity
* Internet
* Marketing

**যা কোম্পানি অন্যের কাছে পাবে → DAE**

* Accounts Receivable

---

**যা কোম্পানি অন্যকে দেবে → LIC**

* Loan
* Accounts Payable
* Tax Payable
* Salary Payable

**যা কোম্পানি আয় করেছে → LIC**

* Sales
* Service Revenue
* Commission

**যা Owner-এর → LIC**

* Capital
* Retained Earnings

---

এইভাবে চিন্তা করলে আর মুখস্থ করতে হবে না। Account-এর নাম দেখেই বুঝতে পারবে সেটা **Asset, Liability, Equity, Income, নাকি Expense**, আর সেখান থেকেই **DAE না LIC** এবং **Debit না Credit** নিজে থেকেই বের হয়ে যাবে।

এরপর চাইলে আমি **Odoo 19-এর Chart of Accounts-এর ১০০+ common account** (যেমন Accounts Receivable, Accounts Payable, VAT Input, VAT Output, COGS, Inventory Valuation, Bank Suspense, Outstanding Receipts ইত্যাদি) একে একে **DAE/LIC + Debit/Credit + Real-life Example** সহ শেখাতে পারি। এতে Odoo Accounting অনেক সহজ হয়ে যাবে।

===================  Last Rules =================

এই ৪টা প্রশ্নই যথেষ্ট। এগুলোর সাথে Debit/Credit এভাবে মিলিয়ে রাখো:

| প্রশ্ন                | Account Type       | Increase হলে      |
| --------------------- | ------------------ | ----------------- |
| 🟢 **এটা কি আমার?**   | Asset              | **Debit (Dr)** ✅  |
| 🔴 **এটা কি অন্যের?** | Liability / Equity | **Credit (Cr)** ✅ |
| 🟠 **আমি খরচ করলাম?** | Expense            | **Debit (Dr)** ✅  |
| 🔵 **আমি আয় করলাম?**  | Income             | **Credit (Cr)** ✅ |

## ১০ সেকেন্ডের ম্যাজিক

```
আমার জিনিস      → Dr
অন্যের জিনিস    → Cr
খরচ             → Dr
আয়             → Cr
```

আরও ছোট করে মনে রাখো:

> **My = Dr**
> **Other = Cr**
> **Expense = Dr**
> **Income = Cr**

অর্থাৎ,

* 💰 Cash পেলাম → **Dr**
* 💻 Laptop কিনলাম → **Dr**
* 💸 Loan নিলাম → **Cr**
* 🧾 Sales করলাম → **Cr**
* 🏠 Rent দিলাম → **Dr**
* 👨‍💼 Salary দিলাম → **Dr**

এই একটাই চিন্তা Odoo Accounting-এর ৮০% Debit/Credit বুঝতে সাহায্য করবে।

