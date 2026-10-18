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