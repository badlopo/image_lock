# BadLock

一种文件加解密方法, 支持多密码 (`<=16`)

## 项目结构

- `core.rs`: 实现 `AES-256-CBC` 加解密

## 文件格式

```text
BadLock\0****\n\[ORIGINAL_FILENAME]n[ENCRYPTED_PASSWORD1_LEN]\n[ENCRYPTED_PASSWORD2_LEN]\n...\n[ENCRYPTED_PASSWORD_BYTES]\n[DATA]
```

- 第1行: `BadLock\0[****]`, 固定12字节, 其中 `****` 为`密码数量-1`的二进制表示 (即最大支持16个密码)
- 第2行: `[ORIGINAL_FILENAME]`, 原始文件名
- 后续若干行: `[ENCRYPTED_PASSWORD_LEN]\n`, 每一行包含一个密文的长度
- 后续1行: `[ENCRYPTED_PASSWORD_BYTES]`, 所有密文的拼接
- 最后一行: `[DATA]`, 加密后的数据

## wasm build

> https://rustwasm.github.io/docs/wasm-pack/commands/build.html

`wasm-pack build --release --target web --out-dir ./wasm --out-name badlock`
