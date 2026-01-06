## .cursor目录，是cursor的专用优化目录。
将该目录放到uni-app x项目下，在cursor中就可以自动应用规则。
目前包括2部分内容：
1. 一批mdc文件，描述了uni-app x的规则，帮助ai生成更准确的uni-app x代码。
2. mcp服务，告诉ai当前项目下有哪些可用的easycom组件，生成代码时可以使用这些组件。


## .github目录和.vscode，是vscode的专用优化目录
1. .github目录是存放规则文件
2. .vscode目是存放调用mcp的配置文件


## .trae目录是trae的专用优化目录
1. 与.cursor配置相同，
2. 不过目前trae官方并没有支持在.trae目录中配置mcp.json，官方提供了手动配置方式，是配置在全局的，
但mcp.json的内容是一样的，可以直接使用

## .agent目录是Google Antigravity的专用优化目录
1. 与.trae配置相同

## .claude目录是Claude Code的专用优化目录
1. CLAUDE.md是默认提示词
2. mcp服务，告诉ai当前项目下有哪些可用的easycom组件，生成代码时可以使用这些组件。