---
title: cron
author: pzc
date: 2024-09-20
cover: /assets/images/jpg/30.jpg
categories: [other]
tags: [linux,mac]
---
Cron 是一种在 Unix、Linux 和 macOS 等操作系统上用于调度任务的工具。它允许用户设定定时执行的任务，比如定期备份数据库、清理临时文件、发送邮件提醒等。Cron 任务通常被称为 "cron jobs"。

### Cron 表达式

Cron 任务的时间安排是通过 cron 表达式来定义的。一个 cron 表达式由六个或七个字段组成，每个字段代表一个时间单位。基本格式如下：

```
* * * * * [command]
- - - - - -
| | | | | |
| | | | | +--- 星期几 (0 - 7) (0 或 7 代表星期天)
| | | | +----- 月份 (1 - 12)
| | | +------- 日期 (1 - 31)
| | +--------- 小时 (0 - 23)
| +----------- 分钟 (0 - 59)
+------------- 秒 (0 - 59, 可选)
```

每个字段可以包含以下类型的值：

- `*`：表示任何可能的值。
- `,`：用来列出多个可能的值，例如 `1,3,5` 表示第1、第3和第5个。
- `-`：用来定义一个范围，例如 `1-5` 表示从1到5。
- `/`：用来定义步长，例如 `*/15` 表示每隔15个单位。

### 示例

- `* * * * *`：每分钟执行一次。
- `0 0 * * *`：每天午夜执行一次。
- `0 0 * * 0`：每周日午夜执行一次。
- `0 0 1 * *`：每月的第一天午夜执行一次。
- `0 0 1 1 *`：每年的1月1日午夜执行一次。

### 如何创建 Cron 任务

1. **编辑 crontab 文件**：
   打开终端，输入 `crontab -e` 命令来编辑当前用户的 crontab 文件。如果你第一次使用这个命令，系统可能会要求你选择一个文本编辑器。

2. **添加任务**：
   在打开的文件中，按照上述格式添加一行新的 cron 表达式，后面跟着要执行的命令或脚本路径。例如：
   ```
   0 0 * * * /usr/bin/backup_script.sh
   ```

3. **保存并退出**：
   根据你使用的编辑器，保存文件并退出。对于 vi/vim 编辑器，可以按 `Esc` 键，然后输入 `:wq` 保存并退出。

4. **查看任务列表**：
   输入 `crontab -l` 查看当前用户的所有 cron 任务。

### 注意事项

- **环境变量**：cron 任务在执行时，其环境变量与用户登录时的环境变量可能不同。因此，最好在脚本中显式指定所有必要的环境变量。
- **输出重定向**：默认情况下，cron 任务的输出会通过邮件发送给用户。如果不需要邮件通知，可以将输出重定向到文件或丢弃：
  ```sh
  0 0 * * * /usr/bin/backup_script.sh > /dev/null 2>&1
  ```
- **测试**：新创建的 cron 任务可能不会立即生效，系统可能需要几分钟来更新任务列表。为了确保任务按预期工作，建议先设置一个测试任务，观察其行为。

Cron 是一个强大且灵活的工具，适合于各种自动化任务的需求。