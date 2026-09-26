# 这Readme是豆包写的。

# 🦐 ShrimpVM

**A UGC framework for Godot 4.6 — players build game behavior with visual blocks, right inside the game.**

> ShrimpVM gives your players a block-based scripting virtual machine, a matching text DSL, and a complete editing toolchain, so "player-made mods" become a first-class feature of your game instead of an afterthought.

---

## What is this?

ShrimpVM is a **User-Generated Content (UGC) framework** for the Godot 4.6 engine. It lets players write and run game behavior scripts by **dragging and dropping block nodes** in an in-game editor — no external tools, no compilation step, no programming background required.

Under the hood, every block is a `ShrimpIR` resource with a self-declared schema. The same script can be authored in two interchangeable ways:

- 🧱 **Visual blocks** — drag, drop, and wire nodes on a canvas inside the game.
- ⌨️ **Garlic DSL** — a text language (`.srk`) for advanced users who prefer typing code.

Both compile into **the same IR tree**, so the two editing styles are fully interoperable.

---

## Project Map

| Repository | Role | What it does |
|---|---|---|
| [**shrimp-vm**](https://github.com/Shrimp-VM/shrimp-vm) | Core framework | Visual block editor + virtual machine + IR compiler for Godot 4.6 |
| [**garlic-language**](https://github.com/Shrimp-VM/garlic-language) | Text DSL | Lexer & parser for the Garlic text language (`.srk`) |
| [**garlic-lsp**](https://github.com/Shrimp-VM/garlic-lsp) | Language server | LSP server for Garlic — completion, hover, real-time diagnostics |
| [**garlic-vscode**](https://github.com/Shrimp-VM/garlic-vscode) | IDE extension | VSCode extension for `.srk`, wired to garlic-lsp over TCP |
| [**coong-fu**](https://github.com/Shrimp-VM/coong-fu) | Example game | A 2D roguelike shooter proving the framework in a real game |
| [**.github**](https://github.com/Shrimp-VM/.github) | Organization profile | This page and org-wide metadata |

---

## Architecture

```
        Authoring                        Core                      Runtime
┌──────────────────────┐        ┌────────────────────┐     ┌─────────────────┐
│ 🧱 Visual blocks     │        │                    │     │                 │
│    (.sst)            │──┐     │   ShrimpIR tree    │     │   ShrimpVM      │
├──────────────────────┤  └───▶ │  (resource, schema)│────▶│   executor      │
│ ⌨️ Garlic DSL (.srk) │──┘     │  compiler/optimizer│     │  (await, async) │
└──────────────────────┘        └────────────────────┘     └─────────────────┘
```

- **Blocks as code** — every block is a `ShrimpIR` resource; its schema is consumed by the visual editor, the importer, and the LSP alike.
- **Async all the way** — the whole execution pipeline is `await`-based, natively supporting suspension, timing, waiting for input, and generators.
- **Full language facilities** — functions, `if`/`while`/`for`/`repeat`, OOP (classes, instances, member access, `this`), and a symbol scope chain.
- **Dual script formats** — visual (`.sst`) and text (`.srk`) compile into the same IR tree, keeping both editing styles interoperable.
- **In-game editor** — a block canvas embeddable in any game: drag & drop, wiring, box selection, and schema-driven parameter editors.
- **Language server** — the Garlic LSP runs inside the editor process alongside the plugin, giving completion / hover / live diagnostics for `.srk` over TCP.

---

## Get Started

Want to use ShrimpVM in your own game?

1. Place the plugin in `addons/shrimpvm` and enable it in project settings.
2. Add a `ShrimpVM` node to your scene and assign a `ShrimpIR` resource to `autoRun`.
3. Or run it manually in code:

```gdscript
var result = await vm.execute(some_ir, ExecutionContext.new())
```

> Want to see it in action? Open the **coong-fu** example game and press `Tab` to open the block editor, then customize your bullets on the fly.

---

## Contributing

We're at an early stage and welcome ideas, bug reports, and pull requests.

- Check the **issues** tab of the relevant repository first.
- For framework work, start with `shrimp-vm`; for the language, `garlic-language`.
- Keep PRs focused and document your custom block nodes following the `ShrimpIR` interface (`execute` / `decompile` / `create_from` / `get_wrapper_schema`).

---

## License

Each repository carries its own license. See the individual repositories for details.

---

<p align="center"><sub>Built on Godot 4.6 · Made for player-driven gameplay</sub></p>

---

---

# 🦐 ShrimpVM（中文版）

**一个基于 Godot 4.6 的 UGC 框架 —— 玩家可以在游戏内用可视化积木搭建游戏行为。**

> ShrimpVM 为你的玩家提供一套积木式脚本虚拟机、配套的文本 DSL 以及完整的编辑工具链，让"玩家自制 Mod"成为游戏的一等公民，而不是事后补丁。

---

## 这是什么？

ShrimpVM 是为 Godot 4.6 引擎打造的**用户生成内容（UGC）框架**。玩家可以在游戏内的编辑器中**通过拖拽积木节点**来编写并运行游戏行为脚本——无需外部工具、无需编译步骤、无需编程基础。

在底层，每个积木都是一个自带声明式 schema 的 `ShrimpIR` 资源。同一份脚本可以用两种可互相替换的方式编写：

- 🧱 **可视化积木** —— 在游戏内的画布上拖拽、连线积木节点。
- ⌨️ **Garlic DSL** —— 面向偏好手写代码的高级用户的文本语言（`.srk`）。

两种方式会编译进**同一棵 IR 树**，因此两种编辑风格完全互通。

---

## 项目地图

| 仓库 | 角色 | 说明 |
|---|---|---|
| [**shrimp-vm**](https://github.com/Shrimp-VM/shrimp-vm) | 核心框架 | Godot 4.6 的可视化积木编辑器 + 虚拟机 + IR 编译器 |
| [**garlic-language**](https://github.com/Shrimp-VM/garlic-language) | 文本 DSL | Garlic 文本语言（`.srk`）的词法分析与语法分析器 |
| [**garlic-lsp**](https://github.com/Shrimp-VM/garlic-lsp) | 语言服务器 | Garlic 的 LSP 服务器 —— 补全、hover、实时诊断 |
| [**garlic-vscode**](https://github.com/Shrimp-VM/garlic-vscode) | IDE 扩展 | 面向 `.srk` 的 VSCode 扩展，通过 TCP 接入 garlic-lsp |
| [**coong-fu**](https://github.com/Shrimp-VM/coong-fu) | 示例游戏 | 一个 2D 俯视角 Rogue-like 射击游戏，验证框架在真实游戏中的可用性 |
| [**.github**](https://github.com/Shrimp-VM/.github) | 组织主页 | 本页面及组织级元数据 |

---

## 架构

```
       编写方式                         核心                       运行期
┌──────────────────────┐        ┌────────────────────┐     ┌─────────────────┐
│ 🧱 可视化积木        │        │                    │     │                 │
│    (.sst)            │──┐     │   ShrimpIR 树      │     │   ShrimpVM      │
├──────────────────────┤  └───▶ │  (resource, schema)│────▶│   执行器         │
│ ⌨️ Garlic DSL (.srk) │──┘     │  编译器/优化器     │     │  (await, async) │
└──────────────────────┘        └────────────────────┘     └─────────────────┘
```

- **积木即代码** —— 每个积木都是一个 `ShrimpIR` 资源，其 schema 同时被可视化编辑器、导入器和 LSP 消费。
- **全程异步** —— 整个执行管线基于 `await`，天然支持挂起、计时、等待输入以及生成器。
- **完整的语言设施** —— 函数、`if`/`while`/`for`/`repeat` 控制流、OOP（类、实例、成员访问、`this`）以及符号作用域链。
- **双格式脚本** —— 可视化（`.sst`）与文本（`.srk`）编译进同一棵 IR 树，两种编辑风格互通。
- **游戏内编辑器** —— 可嵌入任意游戏的积木画布：拖拽、连线、框选，以及由 schema 动态生成的参数编辑器。
- **语言服务器** —— Garlic LSP 随插件常驻编辑器进程，通过 TCP 为 `.srk` 提供补全、hover 与实时诊断。

---

## 快速上手

想把 ShrimpVM 用到自己的游戏里？

1. 将插件放入 `addons/shrimpvm`，并在项目设置中启用。
2. 在场景中添加一个 `ShrimpVM` 节点，把 `ShrimpIR` 资源赋给 `autoRun` 以自动执行。
3. 或在代码中手动执行：

```gdscript
var result = await vm.execute(some_ir, ExecutionContext.new())
```

> 想立刻看到效果？打开 **coong-fu** 示例游戏，按 `Tab` 打开积木编辑器，即可现场自定义你的子弹行为。

---

## 参与贡献

我们处于早期阶段，欢迎各种想法、Bug 反馈和 Pull Request。

- 先查看对应仓库的 **issues** 标签。
- 框架相关工作从 `shrimp-vm` 开始；语言相关从 `garlic-language` 开始。
- 保持 PR 聚焦，并按照 `ShrimpIR` 接口（`execute` / `decompile` / `create_from` / `get_wrapper_schema`）为你的自定义积木节点编写文档。

---

## 许可证

每个仓库各自带有自己的许可证。详见各仓库。

---

<p align="center"><sub>基于 Godot 4.6 构建 · 为玩家驱动式玩法而生</sub></p>
