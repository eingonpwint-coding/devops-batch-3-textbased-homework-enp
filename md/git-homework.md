# Git_HomeWork

## Git Branching Cheat Sheet

Branch ဆိုတာ အလုပ်အသစ်တစ်ခုကို သီးခြားခွဲလုပ်ဖို့
သုံးတာပါ။


| လုပ်ချင်တာ | Command |
|---|---|
| Local branch တွေကြည့်မယ် | `git branch` |
| လက်ရှိ branch နဲ့ ဖိုင်အခြေအနေစစ်မယ် | `git status` |
| Branch အသစ်လုပ်မယ် | `git branch feature` |
| ရှိပြီးသား branch ကို ပြောင်းမယ် | `git switch feature` |
| အသစ်လုပ်ပြီး ပြောင်းမယ် | `git switch -c feature` |
| main ကို ပြန်ပြောင်းမယ် | `git switch main` |
| လက်ရှိ branch နာမည်ပြောင်းမယ် | `git branch -m login` |
| အလုပ်ပြီးတဲ့ branch ဖျက်မယ် | `git branch -d feature` |

ဖျက်မယ့် branch ပေါ်မှာ ရှိနေရင် ဖျက်လို့မရဘူး။
main branch ကို အရင်ပြောင်းရတယ်။



### Checkout နဲ့ Switch

| Switch command | Checkout command |
|---|---|
| `git switch feature` | `git checkout feature` |
| `git switch -c feature` | `git checkout -b feature` |


## 2. Different types of Merge strategies

1. Fast-forward Merge
2. Non-fast-forward Merge
3. Squash Merge

### 2.1 Fast-forward Merge

main ကနေ feature branch ခွဲပြီးနောက် feature မှာပဲ
commit အသစ်တွေ လုပ်ထားတယ်။ main မှာ commit အသစ် မရှိဘူး။

#### ဥပမာ

main မှာ A နဲ့ B commit ရှိတယ်။
B ကနေ feature ခွဲပြီး အလုပ်နှစ်ခု လုပ်ထားတယ်။

- C = Login form ထည့်တယ်။
- D = Login button ထည့်တယ်။

#### Merge မလုပ်ခင်

```mermaid
flowchart LR
    A[A] --> B["B — main"]
    B --> C["C: Login form"]
    C --> D["D: Login button — feature"]
```

- main ရဲ့ history က A → B ဖြစ်တယ်။
- feature ရဲ့ history က A → B → C → D ဖြစ်တယ်။

#### အသုံးပြုရတဲ့ Command

```bash
git switch main
git merge --ff-only feature
```

1. `git switch main` က main branch ကို ပြောင်းတယ်။
2. `git merge --ff-only feature` က main ကို
   feature ရဲ့ နောက်ဆုံး commit D ဆီ ရွှေ့ပေးတယ်။

#### Merge လုပ်ပြီး

```mermaid
flowchart LR
    A[A] --> B[B]
    B --> C[C]
    C --> D["D — main, feature"]
```

အခုဆိုရင် main နဲ့ feature နှစ်ခုလုံးက D ကို ညွှန်းနေတယ်။
main ထဲမှာ Login form နဲ့ Login button ရော ပါလာပြီ။

**Commit အသစ် မလုပ်ဘဲ main ကို B ကနေ D ဆီ
ရွှေ့ပေးတာကို Fast-forward merge လို့ ခေါ်တယ်။**

`--ff-only` က fast-forward လုပ်လို့ရမှ ပေါင်းပေးတယ်။
branch နှစ်ခုလုံးမှာ သီးခြား commit အသစ်ရှိနေရင်
merge မလုပ်ဘဲ ရပ်သွားပါမယ်။



### 2.2 Non-fast-forward Merge

main branch ကနေ feature branch ခွဲပြီးနောက် main branch
နဲ့ feature branch နှစ်ခုလုံးမှာ
သီးခြား commit အသစ်တွေ လုပ်ထားတယ်။

#### ဥပမာ

main branch မှာ A နဲ့ B commit ရှိတယ်။
B ကနေ feature branch ခွဲထားတယ်။

- feature branch မှာ C = Login page ထပ်ထည့်
- main branch မှာ D = Contact page ထပ်ထည့်

#### Merge မလုပ်ခင်

```mermaid
flowchart TD
    A[A] --> B[B]
    B --> D["D: Contact page — main"]
    B --> C["C: Login page — feature"]
```

- main ရဲ့ history က A → B → D ဖြစ်တယ်။
- feature ရဲ့ history က A → B → C ဖြစ်တယ်။

ဒီဥပမာမှာ နှစ်ဘက်လုံးမှာ အလုပ်အသစ်ရှိလို့ main ကို C ဆီ
ရွှေ့ပေးရုံနဲ့ မရတော့ဘူး။ C နဲ့ D ရဲ့အလုပ်တွေကို
ပေါင်းဖို့ လိုတယ်။

#### အသုံးပြုမယ့် Command

```bash
git switch main
git merge feature
```

1. `git switch main` က main branch ကို ပြောင်းတယ်။
2. `git merge feature` က feature ရဲ့ Login အလုပ်နဲ့
   main ရဲ့ Contact အလုပ်ကို ပေါင်းပေးတယ်။

#### Merge လုပ်ပြီး

```mermaid
flowchart TD
    A[A] --> B[B]
    B --> D[D]
    B --> C["C — feature"]
    D --> M["M: Contact + Login — main"]
    C --> M
```

M ဆိုတဲ့ merge commit အသစ် ရလာတယ်။
M က C နဲ့ D ကို ချိတ်ထားပြီး နှစ်ဘက်လုံးရဲ့အလုပ် ပါတယ်။

- main က M ကို ညွှန်းနေတယ်။
- feature က C ကို ညွှန်းနေဆဲ။
- မူရင်း C နဲ့ D commit တွေ ဆက်ရှိနေတယ်။

**Branch နှစ်ခုရဲ့အလုပ်ကို merge commit အသစ်နဲ့
ပေါင်းချိတ်တာကို Non-fast-forward merge လို့ ခေါ်တယ်။**

#### --no-ff ဆိုတာ

Fast-forward လုပ်လို့ရတဲ့အခြေအနေမှာတောင်
merge commit သီးသန့် ထားချင်ရင် `--no-ff` သုံးတယ်။

```bash
git switch main
git merge --no-ff feature
```

### 2.3 Squash Merge

Squash merge ဆိုတာ feature branch က အပြောင်းအလဲတွေကို
main ထဲမှာ commit တစ်ခုတည်းအဖြစ် စုပြီး သိမ်းတာပါ။

#### ဥပမာ

main မှာ A နဲ့ B commit ရှိတယ်။
B ကနေ feature branch ခွဲပြီး အောက်ပါအလုပ်တွေ လုပ်ထား

| Commit | လုပ်ထားတဲ့အလုပ် |
|---|---|
| C | Login form ရေးတယ် |
| D | Login button ထည့်တယ် |
| E | Login အရောင်ပြင်တယ် |

Merge မလုပ်ခင် history က—

- main: A → B
- feature: A → B → C → D → E

#### အသုံးပြုမယ့် Command

```bash
git switch main
git merge --squash feature
git commit -m "Add complete login page"
```

1. `git switch main` က main branch ကို ပြောင်း
2. `git merge --squash feature` က feature ရဲ့ အပြောင်းအလဲတွေကို
   main ရဲ့ working files နဲ့ staging area ထဲ ထည့်ပေး
   Commit အသစ် မလုပ်ရသေး
3. `git commit` က အလုပ်အားလုံးကို S ဆိုတဲ့ commit
   တစ်ခုအဖြစ် သိမ်း

#### လုပ်ပြီးနောက်

- main: A → B → S
- feature: A → B → C → D → E

S ထဲမှာ Login form၊ Login button နဲ့ အရောင်ပြင်ထားမှု
အားလုံး ပါတယ်။ main history ထဲမှာတော့ C၊ D၊ E
တစ်ခုချင်းမပါဘဲ S တစ်ခုပဲ တိုးလာ

Feature branch မှာ မူရင်း C၊ D၊ E commit တွေ ဆက်ရှိ 