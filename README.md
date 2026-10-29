# java-learning

软件技术 → Java 后端 的学习仓库。
路线文档：`../零基础到Java开发_专升本学习路线.md`

---

## ✅ JDK 已装好（2026-10-29）

| 项目 | 值 |
|---|---|
| 版本 | **OpenJDK 21.0.2 LTS** |
| 安装位置 | `G:\Java\jdk-21` |
| JAVA_HOME | 已写入用户环境变量 |
| PATH | 已追加 `G:\Java\jdk-21\bin` |
| 安装包备份 | `../tools/jdk21.zip`（192MB，确认无误后可删） |

> 用的是免安装版（解压即用），没有写注册表、没有装服务，**想卸载直接删掉 `G:\Java` 文件夹即可**。

### 验证（开一个**全新的**终端窗口）

```powershell
java -version
javac -version
```

应该输出：

```
openjdk version "21.0.2" 2024-01-16
OpenJDK Runtime Environment (build 21.0.2+13-58)
javac 21.0.2
```

> **老窗口不会自动生效**，环境变量只对新开的进程生效。

---

## 跑第一个程序

```powershell
cd java-learning\day01
java HelloWorld.java
```

输出：

```
Hello, 世界!
我的第一行 Java 代码跑起来了。
Java 版本: 21.0.2
运行平台: Windows 11
```

也可以走「先编译再运行」，理解 Java 的两步机制：

```powershell
javac HelloWorld.java     # 生成 HelloWorld.class（字节码，给 JVM 看）
java HelloWorld           # 运行，注意不带 .class
```

---

## 环境出问题时（G 盘盘符变了 / 换电脑）

在仓库根目录执行（如果提示 `禁止运行脚本`，先跑一次
`Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned`）：

```powershell
. .\java-env.ps1
```

脚本会自动在 `G:\Java`、`C:\Program Files\Microsoft`、`C:\Program Files\Java`、
`%USERPROFILE%\.jdks` 等位置找 JDK 并配好当前窗口的 PATH。

手工等价写法：

```powershell
$env:JAVA_HOME="G:\Java\jdk-21"
$env:PATH="$env:JAVA_HOME\bin;$env:PATH"
```

---

## 下一步：装 IDEA（可选，第 2–3 天再做）

- Community 版免费：**<https://www.jetbrains.com/idea/download/>**
- 第一次启动选主题、装插件全部跳过
- `File → Open` 选 `java-learning` 文件夹
- 右键 `HelloWorld.java` → `Run 'HelloWorld.main()'`
- IDEA 会自动读到已配好的 `JAVA_HOME`

---

## 常见报错对照

| 报错 | 原因 | 解决 |
|---|---|---|
| `无法将"java"项识别为 cmdlet` | 用的是老窗口 / PATH 没生效 | **新开窗口**；仍不行跑 `. .\java-env.ps1` |
| `类 HelloWorld 是公共的, 应在名为 HelloWorld.java 的文件中声明` | 文件名与类名不一致（大小写也算） | 改成完全一致 |
| `找不到符号` / `需要';'` | 拼写错、缺分号、括号不配对 | **只修第一条错误**，后面的多半是连带的 |
| `找不到或无法加载主类` | `java` 后面多写了 `.class` | `java HelloWorld` |
| 中文乱码 | 控制台编码不是 UTF-8 | `chcp 65001` 后再运行 |
| `Could not find or load main class` 且路径带空格 | 命令行参数被拆开 | 给参数加引号 |

---

## 编码习惯（第一天就养成）

1. **文件名 = 类名**，首字母大写
2. 每条语句结尾 `;`；`main` 签名一个字符都不能改
3. 缩进 **4 个空格**，不要 Tab 与空格混用
4. **不要复制粘贴来"跑通"**——手敲一遍，肌肉记忆是唯一不骗人的东西
5. 每完成一个练习就 `git commit`（Day 2 教 Git）
