# ClockCmd Plugin Wiki

------

## 🎯 Introduction

**ClockCmd** is a powerful Minecraft Bukkit/Spigot plugin that allows server administrators to set delayed command execution and daily scheduled commands. It supports both Chinese and English interfaces, providing flexible task management features.

------

## ⭐ Features

### 🔧 Core Features

- **Delayed Commands**: Set commands to execute after a specified number of seconds
- **Daily Scheduling**: Set commands to execute at a fixed time every day
- **Task Management**: Add, delete, and view task details
- **Batch Operations**: Clear all tasks (admin function)

### 🌍 Multilingual Support

- Full support for Chinese and English
- Configurable language settings
- Localized error messages and help information

### 🛡️ Permission Control

- Fine-grained permission management
- Separate user and admin permissions
- Flexible access control

### 📊 Advanced Features

- Automatic configuration saving
- Task status monitoring
- Debug mode support
- Thread-safe design

------

## 🚀 Installation and Setup

### Installation Steps

1. Download the Plugin
   - Place the ClockCmd.jar file into the server's plugins folder
2. Restart the Server
   - Restart the server to generate the configuration files
3. Configure the Plugin
   - Edit plugins/ClockCmd/config.yml for personalized settings

### File Structure

text

```
plugins/ClockCmd/
├── config.yml           # Main configuration file
├── messages_zh.yml      # Chinese language pack
├── messages_en.yml      # English language pack
└── plugin.yml          # Plugin information file
```

------

## 💬 Command Usage

### Main Command Format

text

```
/clockcmd <subcommand> [arguments...]
/clock <subcommand> [arguments...]     # Chinese alias
```

### Subcommand List

| Command    | Description       | Usage                                 | Permission      |
| ---------- | ----------------- | ------------------------------------- | --------------- |
| **add**    | Add a new task    | /clockcmd add <type> <time> <command> | clockcmd.use    |
| **remove** | Remove a task     | /clockcmd remove <ID>                 | clockcmd.use    |
| **list**   | List all tasks    | /clockcmd list                        | clockcmd.use    |
| **info**   | View task details | /clockcmd info <ID>                   | clockcmd.use    |
| **clear**  | Clear all tasks   | /clockcmd clear                       | clockcmd.admin  |
| **reload** | Reload config     | /clockcmd reload                      | clockcmd.reload |

### Task Types

#### Delayed Task (delay)

Execute a command once after a specified number of seconds

text

```
/clockcmd add delay <seconds> <command>
```

**Example**:

text

```
/clockcmd add delay 300 say 5 minutes are up!
/clockcmd add delay 3600 restart  # Restart the server after 1 hour
```

#### Daily Scheduled Task (daily)

Execute a command at a fixed time every day

text

```
/clockcmd add daily <HH:mm> <command>
```

**Example**:

text

```
/clockcmd add daily 14:30 broadcast Daily maintenance time
/clockcmd add daily 00:00 save-all    # Save the world every midnight
```

------

## 🔐 Permission System

### Permission Nodes

| Permission      | Description          | Default |
| --------------- | -------------------- | ------- |
| clockcmd.use    | Use basic commands   | true    |
| clockcmd.reload | Reload plugin config | op      |
| clockcmd.admin  | Admin commands       | op      |
| clockcmd.*      | All permissions      | op      |

### Permission Configuration Example

**Using LuckPerms**:

text

```
# Grant basic usage permission to a player
/lp user <player> permission set clockcmd.use true

# Grant full permissions to an admin
/lp user <admin> permission set clockcmd.* true
```

**Using PermissionsEx**:

yaml

```
groups:
  default:
    permissions:
    - clockcmd.use
  admin:
    permissions:
    - clockcmd.*
```

------

## ⚙️ Configuration Files

### config.yml

yaml

```
# Language setting: en (English) or zh (Chinese)
language: zh

# Auto-save configuration interval (minutes)
auto-save: 5

# Plugin settings
settings:
  # Show task count on startup
  show-task-count-on-startup: true
  
  # Maximum delay time (seconds, default 7 days)
  max-delay-seconds: 604800
  
  # Log command execution
  log-command-execution: true
  
  # Allow players to use commands
  allow-player-commands: true
  
  # Daily task check interval (minutes)
  daily-check-interval: 60

# Debug settings
debug:
  enabled: false
  verbose-scheduling: false
```

### Configuration Options

| Option                     | Type    | Default | Description                         |
| -------------------------- | ------- | ------- | ----------------------------------- |
| language                   | String  | zh      | Interface language (en/zh)          |
| auto-save                  | Integer | 5       | Auto-save interval (minutes)        |
| show-task-count-on-startup | Boolean | true    | Show task statistics on startup     |
| max-delay-seconds          | Integer | 604800  | Maximum delay time (seconds)        |
| log-command-execution      | Boolean | true    | Log command executions              |
| allow-player-commands      | Boolean | true    | Allow players to use commands       |
| daily-check-interval       | Integer | 60      | Daily task check interval (minutes) |

------

## 📚 Usage Examples

### Basic Usage

**1. Create a reminder in 5 minutes**

text

```
/clockcmd add delay 300 say The server will restart in 5 minutes, please prepare!
```

**2. Set a daily maintenance reminder**

text

```
/clockcmd add daily 02:00 broadcast §c[Maintenance] The server will undergo maintenance in 2 minutes
/clockcmd add daily 02:02 restart
```

**3. View all tasks**

text

```
/clockcmd list
```

### Advanced Applications

**Scheduled World Backups**

text

```
/clockcmd add daily 03:00 save-all
/clockcmd add daily 03:01 say World data has been saved
```

**Server Restart Sequence**

text

```
/clockcmd add delay 600 say §e[System] The server will restart in 10 minutes
/clockcmd add delay 900 say §6[System] The server will restart in 5 minutes  
/clockcmd add delay 1140 say §c[System] The server will restart in 1 minute
/clockcmd add delay 1200 restart
```

**Event Management**

text

```
/clockcmd add daily 20:00 broadcast §a[Event] Daily sign-in starts now! Type /signin to sign in
/clockcmd add daily 19:00 broadcast §b[Weekend Event] Building contest starts now!
```

### Task Management

**View Task Details**

text

```
/clockcmd info a1b2c3d4-e5f6-7890-abcd-ef1234567890
```

**Remove a Specific Task**

text

```
/clockcmd remove a1b2c3d4-e5f6-7890-abcd-ef1234567890
```

**Clear All Tasks** (Admin)

text

```
/clockcmd clear
```

------

## ❓ Frequently Asked Questions

### Q: How to switch languages?

**A**: Edit the language setting in config.yml:

- language: en - English interface
- language: zh - Chinese interface

### Q: What if a task doesn't execute?

**A**: Check the following:

1. Ensure the server time is correct
2. Verify the command syntax
3. Look for error messages in the console
4. Check the task status: /clockcmd info <ID>

### Q: Can I execute commands from other plugins?

**A**: Yes! ClockCmd supports executing any console command, including:

- Native Minecraft commands
- Commands from other plugins
- Custom script commands

### Q: Is there a limit to the number of tasks?

**A**: There is no hard limit, but it's recommended to set a reasonable number based on server performance. Too many tasks may affect server performance.

### Q: Will tasks disappear after a server restart?

**A**: No. All tasks are saved in the configuration file and will be automatically reloaded after a server restart.

### Q: What are the requirements for the time format?

**A**: Daily tasks use the 24-hour format:

- Correct: 14:30, 09:00, 23:59
- Incorrect: 2:30pm, 9:00, 25:00

### Q: How to set permissions?

**A**: Use a permission management plugin (such as LuckPerms) to set the corresponding permission nodes. Refer to the Permission System section.

------

## 🔧 Troubleshooting

### Common Errors and Solutions

**1. Plugin fails to load**

- Check Java version compatibility
- Confirm Bukkit/Spigot version support
- Check the console for error messages

**2. Command execution fails**

text

```
Error: Invalid time format!
Solution: Check the time format, use HH:mm format (e.g., 14:30)
```

**3. Permission issues**

text

```
Error: You don't have permission to do that!
Solution: Check user permissions, ensure they have the `clockcmd.use` permission
```

**4. Task not executing**

- Check the server system time
- Confirm the task status (/clockcmd info <ID>)
- Review the console logs

### Debug Mode

Enable debug mode for detailed information:

yaml

```
debug:
  enabled: true
  verbose-scheduling: true
```

------

## 📞 Support and Feedback

### Getting Help

- **In-game Help**: /clockcmd (displays usage instructions)
- **Configuration Help**: Refer to this Wiki document
- **Error Reporting**: Check the server console logs
