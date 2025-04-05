# CLI Commands

### 3.1 Anatomy of an Azure CLI Command

Every Azure CLI command follows the **same basic structure**:

```bash
bashCopyEditaz <group> <subgroup> <command> --parameters
```

| Part           | Meaning                        | Example                         |
| -------------- | ------------------------------ | ------------------------------- |
| `az`           | The Azure CLI tool itself      |                                 |
| `<group>`      | The Azure service group        | `vm`, `group`, `storage`        |
| `<subgroup>`   | Optional: further subgrouping  | `vm extension`, `network nsg`   |
| `<command>`    | The action you want to perform | `create`, `list`, `delete`      |
| `--parameters` | Additional options or settings | `--name myVM --location eastus` |

***

#### 🛠️ Example:

Create a resource group:

```bash
bashCopyEditaz group create --name myResourceGroup --location eastus
```

* `group` = working with resource groups
* `create` = action to create a new one
* `--name` and `--location` = parameters to define it

***

### 📚 3.2 Using Built-In Help

Azure CLI has **built-in help** everywhere.

If you ever forget a command or need examples:

```bash
bashCopyEditaz --help
```

Help for a specific group:

```bash
bashCopyEditaz vm --help
```

Help for a specific command:

```bash
bashCopyEditaz vm create --help
```

👉 **Tip:** Look at the **Examples** section in the help output. It saves time!

***

### 🎨 3.3 Understanding Output Formats

You can control **how** Azure CLI shows you the results with `--output` (or `-o`).

| Output Format | Usage                           | Best For                                            |
| ------------- | ------------------------------- | --------------------------------------------------- |
| JSON          | `--output json`                 | Full detail, automation scripts                     |
| Table         | `--output table`                | Human-readable summaries                            |
| YAML          | `--output yaml`                 | Structured, readable config                         |
| JSONC         | `--output jsonc` (colored JSON) | Developers, colored JSON output                     |
| None          | `--output none`                 | When you only care about the result, not the output |

***

#### 🛠️ Example:

List all resource groups as a table:

```bash
bashCopyEditaz group list --output table
```

Output:

| Name            | Location | Status    |
| --------------- | -------- | --------- |
| myResourceGroup | eastus   | Succeeded |

Much easier to read than raw JSON!

***

### 🔍 3.4 Filtering with --query (JMESPath)

Azure CLI supports **powerful filtering** using `--query`.

**JMESPath** is a query language for JSON data that lets you select specific parts of output.

***

#### 🛠️ Example:

List only the names of all resource groups:

```bash
bashCopyEditaz group list --query "[].name" --output table
```

Output:

| Name            |
| --------------- |
| myResourceGroup |
| testRG          |

***

Another Example:\
Get the ID of the first VM in the list:

```bash
bashCopyEditaz vm list --query "[0].id" --output tsv
```

(tsv = tab-separated value, just the value, no JSON)

***

**🧠 Tip:** You can combine `--query` and `--output` to make CLI results **beautiful and precise**.

***

### ⚡ 3.5 Common Parameters You’ll Always See

| Parameter                  | Purpose                    | Example                 |
| -------------------------- | -------------------------- | ----------------------- |
| `--name` or `-n`           | Name of the resource       | `--name myVM`           |
| `--resource-group` or `-g` | Name of the Resource Group | `--resource-group myRG` |
| `--location` or `-l`       | Azure Region               | `--location eastus`     |
| `--output` or `-o`         | Format the output          | `--output table`        |
| `--query`                  | Filter the output          | `--query "[].name"`     |

You’ll use these **over and over again** across all Azure CLI commands.

***

## 📝 Module 3 Summary

| Topic                 | Key Points                                             |
| --------------------- | ------------------------------------------------------ |
| CLI command structure | `az <group> <command> --parameters`                    |
| Built-in help         | `az <group> <command> --help`                          |
| Output formats        | JSON (default), Table, YAML, JSONC                     |
| Filtering output      | `--query` with JMESPath syntax                         |
| Common parameters     | `--name`, `--resource-group`, `--location`, `--output` |
