---
name: ask-tty
description: 需要 stdin 輸入時（sudo、ssh、y/N 確認等），透過 ask-tty 向使用者要求輸入。永遠生效。
alwaysApply: true
---

# ask-tty — stdin proxy

Bash tool 不支援互動式 stdin。當指令需要使用者輸入（密碼、確認、passphrase 等），使用 `ask-tty` 取得。

## 位置偵測

```bash
# 依序嘗試：PATH > ~/bin > 專案 scripts/
command -v ask-tty || test -x ~/bin/ask-tty || echo "ask-tty not found"
```

如果找不到就告知使用者 ask-tty 未安裝。

## 用法

### sudo

```bash
echo $(ask-tty "sudo password" --sensitive) | sudo -S <command>
```

### ssh 密碼

```bash
sshpass -p "$(ask-tty "SSH password for user@host" --sensitive)" ssh user@host <command>
```

### y/N 確認

```bash
ANSWER=$(ask-tty "Proceed with apt upgrade? (y/N)")
echo "$ANSWER" | sudo apt upgrade
```

### 一般輸入

```bash
VALUE=$(ask-tty "Enter the new hostname")
```

## Flags

- `--sensitive` / `-s`: 輸入內容自動從聊天記錄中刪除（用於密碼類）
- `--timeout N` / `-t N`: 超時秒數（預設 120 秒）

## 規則

1. 密碼類**一定**加 `--sensitive`
2. 不要把 ask-tty 的輸出存到檔案或 log
3. 不要在 prompt 中洩漏現有密碼
4. ask-tty 回傳的值透過 stdout 取得，不帶換行
5. 如果 ask-tty 失敗（timeout、config 缺失），告知使用者原因，不要重試
