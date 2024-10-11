---
title: eslintrc.js文件配置相关说明
abbrlink: 10b7b260
---
```
module.exports = {
	root: true,
	// 此项是用来告诉eslint找当前配置文件不能往父级查找
	parserOptions: {
		// 此项是用来指定javaScript语言类型和风格，sourceType用来指定js导入的方式，默认是script，此处设置为module，指某块导入方式
		parser: "@babel/eslint-parser",
		// 设置 script(默认) 或 module，如果代码是在ECMASCRIPT中的模块
		sourceType: "module"
	},
	// 此项指定环境的全局变量，下面的配置指定为浏览器环境
	env: {
		browser: true,
		node: true,
		es6: true
	},
	// 此项是用来配置标准的js风格，就是说写代码的时候要规范的写，如果你使用vs-code我觉得应该可以避免出错
	extends: ["plugin:vue/recommended", "eslint:recommended"],
	rules: {
		"vue/max-attributes-per-line": ["error", { // 每个属性独占一行
			"singleline": { // 单行属性
				"max": 1 // 单行属性最大数量
			},
			"multiline": { // 多行属性
				"max": 1	// 多行属性最大数量
			}
		}],
		"vue/singleline-html-element-content-newline": "off", // 在单行元素的内容前后要求换行
		"vue/multiline-html-element-content-newline": "off", // 在多行元素的内容前后要求换行
		// 'vue/name-property-casing': ['error', 'PascalCase'], // 组件名使用PascalCase命名
		// 'vue/no-v-html': 'off', // 禁止使用v-html指令
		"vue/html-self-closing": [ // 标签自动闭合
			"error",
			{
				html: {
					void: "always", // void元素（如：img、br必须闭合）
					normal: "always", // 普通元素（如：div比如闭合）
					component: "always" // 组件元素(如：my-component必须闭合)
				},
				svg: "always", // svg元素必须闭合
				math: "always" // math元素必须闭合
			}
		],
		"accessor-pairs": 2, // 强制geeter和seeter成对出现
		"arrow-spacing": [ // 箭头函数前后空格
			2, // 错误级别
			{
				before: true, // 前面是否需要空格
				after: true // 后面是否需要空格
			}
		],
		"block-spacing": [2, "always"], // 大括号前后空格
		"brace-style": [
			2,
			"1tbs", // 大括号风格
			{
				allowSingleLine: true // 允许块语句和单行语句写在同一行
			}
		],
		camelcase: [ // 强制使用驼峰命名
			0,
			{
				properties: "always"
			}
		],
		"comma-dangle": [2, "never"], // 对象字面量项尾不能有逗号
		"comma-spacing": [ // 逗号前后的空格
			2,
			{
				before: false, // 逗号前是否需要空格
				after: true // 逗号后是否需要空格
			}
		],
		"comma-style": [2, "last"], // 逗号风格，换行时在行尾
		"constructor-super": 2, // super()必须在构造函数中调用
		curly: [2, "multi-line"], // 	大括号风格
		"dot-location": [2, "property"], // 点号操作符使用风格
		"eol-last": 2, // 文件末尾强制换行
		eqeqeq: ["error", "always", { null: "ignore" }], // 强制使用全等
		"generator-star-spacing": [ // 强制 generator 函数中 * 号前后空格
			2, // 错误级别
			{
				before: true, // * 号前是否需要空格
				after: true // * 号后是否需要空格
			}
		],
		"handle-callback-err": [2, "^(err|error)$"], // 处理错误
		indent: ["error", "tab", { SwitchCase: 1 }], // 缩进风格
		"padded-blocks": [2, "never"], // 块语句内部前后空行
		"vue/html-indent": [ // vue文件缩进风格
			"error",	// 错误级别
			"tab",	// 缩进风格
			{
				attribute: 1, // 属性缩进
				baseIndent: 1, // 基础缩进
				closeBracket: 0, // 闭合标签缩进
				alignAttributesVertically: true, // 属性垂直对齐
				ignores: [] // 忽略缩进
			}
		],
		"jsx-quotes": [2, "prefer-single"], // 强制在JSX属性中一致地使用单引号或双引号
		"key-spacing": [ // 对象字面量中冒号后的空格
			2,
			{
				beforeColon: false, // 冒号前是否需要空格
				afterColon: true // 冒号后是否需要空格
			}
		],
		"keyword-spacing": [ // 关键字前后空格
			2,
			{
				before: true, // 关键字前是否需要空格
				after: true // 关键字后是否需要空格
			}
		],
		"new-cap": [ // 构造函数首字母大写
			2,
			{
				newIsCap: true, // 构造函数首字母大写
				capIsNew: false // new 关键字首字母大写
			}
		],
		"new-parens": 2, // new时必须加括号
		"no-array-constructor": 2, // 禁止使用数组构造器
		"no-caller": 0, // callee// arguments.caller 和 arguments.callee 被移除，可使用命名函数表达式代替
		// 'no-console': 'off', // 禁止使用console
		"no-class-assign": 2, // 禁止修改类声明
		"no-cond-assign": 2, // 禁止条件表达式中出现赋值操作符
		"no-const-assign": 2, // 禁止修改const声明的变量
		"no-control-regex": 0, // 禁止正则表达式字面量中出现控制字符
		"no-delete-var": 2, // 不能删除变量
		"no-dupe-args": 2, // 函数参数不能重复
		"no-dupe-class-members": 2,	// 类成员不能重复
		"no-dupe-keys": 2, // 对象字面量中禁止出现重复key
		"no-duplicate-case": 2, // switch中的case标签不能重复
		"no-empty-character-class": 2, // 禁止在正则表达式中使用空字符集
		"no-empty-pattern": 2, // 禁止使用空解构模式
		"no-eval": 0, // eval() // eval() 会被移除
		"no-ex-assign": 2, // 禁止对catch语句的参数重新赋值
		"no-extend-native": 2, // 禁止扩展原生类型
		"no-extra-bind": 2, // 禁止不必要的函数绑定
		"no-extra-boolean-cast": 2, //	禁止不必要的bool转换
		"no-extra-parens": [2, "functions"], //	禁止不必要的括号
		"no-fallthrough": 2, // 禁止 case 语句落空
		"no-floating-decimal": 2, // 禁止省略浮点数中的0 .5 3.
		"no-func-assign": 2, // 禁止重复的函数声明
		"no-implied-eval": 2, // 禁止使用隐式eval
		"no-inner-declarations": [2, "functions"], // 禁止在if while for语句中使用声明语句
		"no-invalid-regexp": 2, // 禁止无效的正则表达式
		"no-irregular-whitespace": 2, // 禁止不规则的空白
		"no-iterator": 2, // 禁止使用__iterator__属性
		"no-label-var": 2, // 禁止标签与变量同名
		"no-labels": [ // 禁止标签定义在case之后
			2,
			{
				allowLoop: false, // allowLoop, allowSwitch // 允许在循环内使用label
				allowSwitch: false // 禁止标签定义在case之后
			}
		],
		"no-lone-blocks": 2, // 禁止不必要的嵌套块
		"no-mixed-spaces-and-tabs": 2, // 禁止混用tab和空格
		"no-multi-spaces": 2, // 禁止多余的空格
		"no-multi-str": 2, // 禁止多行字符
		"no-multiple-empty-lines": [ // 禁止出现多行空行
			2,
			{
				max: 1 // 最大连续空行数
			}
		],
		"html-closing-bracket-newline": [2, { multiline: false }], // html标签结束标签换行 // 禁止出现多行空行
		"vue/html-closing-bracket-newline": [2, { multiline: false }], // html标签结束标签换行 // 禁止出现多行空行
		"array-bracket-newline": "off", // 数组括号内的空格使用风格 <a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel" target="_blank"> 多个属性换行时，结尾的标签跟随最后一个属性，可以不换行
		"no-native-reassign": 2, // 禁止修改原生对象
		"no-negated-in-lhs": 2, // 禁止在in条件语句左侧使用否定操作符
		"no-new-object": 2, // 禁止使用new Object()
		"no-new-require": 2, // 禁止使用new require
		"no-new-symbol": 2, // 禁止 Symbol new 操作符
		"no-new-wrappers": 2, // 禁止使用new创建包装实例
		"no-obj-calls": 2, // 禁止把全局对象作为函数调用
		"no-octal": 2, // 禁止使用八进制
		"no-octal-escape": 2, // 禁止使用八进制转义序列
		"no-path-concat": 2, // node // __dirname, __filename // 禁止对__dirname, __filename使用字符串连接
		"no-proto": 2, // 禁止使用__proto__属性
		"no-redeclare": 2, // 禁止重复声明变量
		"no-regex-spaces": 2, // 禁止正则表达式字面量中出现多个空格
		"no-return-assign": [0, "except-parens"], // 禁止在return语句中使用赋值语句
		"no-self-assign": 2, // 禁止自己给自己赋值
		"no-self-compare": 2, // 禁止自身比较
		"no-sequences": 0, // md5 error // 禁止逗号操作符
		"no-shadow-restricted-names": 2, // 禁止使用保留字作为变量名
		"no-spaced-func": 2, // 禁止函数名和括号之间有空格
		"no-sparse-arrays": 2, // 禁止稀疏数组
		"no-this-before-super": 2, // 在调用super()之前不能使用this或super
		"no-throw-literal": 2, // throw 必须是 Error 对象
		"no-trailing-spaces": 2, // 行尾禁止有空格
		"no-undef": 2, // 未定义变量
		"no-undef-init": 2, // 禁止将undefined作为变量初始化
		"no-unexpected-multiline": 2, // md5 error //禁止行内空格和tab混用
		"no-unmodified-loop-condition": 0, // while(x) // x未修改
		"no-unneeded-ternary": [// 	禁止不必要的嵌套 var isYes = true ? true : false; // 错误写法
			2,
			{
				defaultAssignment: false // 默认赋值
			}
		],
		"no-unreachable": 2, // 不能有无法执行的代码
		"no-unsafe-finally": 2, // md5 error // finally块中不能有控制流语句
		"no-unused-vars": [ // 禁止出现未使用的变量
			2,
			{
				vars: "all", // 所有变量
				args: "none" // 函数参数不使用
			}
		],
		"no-useless-call": 2, // 禁止不必要的call和apply
		"no-useless-computed-key": 2, // 禁止在对象字面量中使用不必要的计算属性
		"no-useless-constructor": 2, //	禁止不必要的构造函数
		"no-useless-escape": 0, // md5 error // 禁止不必要的转义字符
		"no-whitespace-before-property": 2, // 对象字面量中冒号的前后空格
		"no-with": 2, // with error // 禁止使用with
		"one-var": [ // 声明多个变量时，必须使用一个var
			2,
			{
				initialized: "never" // 声明多个变量时，必须使用一个var
			}
		],
		"operator-linebreak": [ // 换行符的位置
			2,
			"after",
			{
				overrides: { // 换行符的位置
					"?": "before", // 三元运算符
					":": "before" // if语句
				}
			}
		],

		// 'quotes':'off',
		quotes: [	// 引号类型 `` "" ''
			1,
			// 'single', // 建议使用单引号
			"double", // 建议使用双引号
			{
				avoidEscape: true, // 避免转义
				allowTemplateLiterals: true // 允许使用模板字符串
			}
		],
		// 'semi': 'off',
		// 'comma-dangle':'off',
		semi: [2, "never"],	// 语句末尾是否需要分号
		"semi-spacing": [ // 分号前后空格
			2,
			{
				before: false,	// 分号前是否需要空格
				after: true // 分号后是否需要空格
			}
		],
		"space-before-blocks": [2, "always"], // '{'前是否需要空格
		"space-before-function-paren": [ // 函数定义时括号前面要不要有空格
			"error",
			{
				anonymous: "always", // 	匿名函数
				named: "never", // 命名函数
				asyncArrow: "always" // 异步函数
			}
		],
		"space-in-parens": [2, "never"], // ()内是否需要空格
		"space-infix-ops": 2, // 中缀操作符周围要不要有空格
		"space-unary-ops": [ //	一元操作符前后要不要加空格
			2,
			{
				words: true, // 一元运算符前后是否加空格
				nonwords: false
			}
		],
		"spaced-comment": [ // 注释风格要不要有空格什么的
			2,
			"always", // always:在行首出现，且后面至少有一个空格，在行尾出现没有空格
			{
				markers: ["global", "globals", "eslint", "eslint-disable", "*package", "!", ","] // 标记不需要空格的注释
			}
		],
		"template-curly-spacing": [2, "never"], // 大括号内是否允许空格
		"use-isnan": 2, // 用isNaN()检查NaN
		"valid-typeof": 2, // 必须使用合法的typeof的值
		"wrap-iife": [2, "any"], // 立即执行函数表达式的小括号风格问题，参数是否允许省略
		"yield-star-spacing": [2, "both"], // 	yield*表达式中的*号前后是否有空格
		yoda: [2, "never"], // 	禁止尤达条件
		"prefer-const": 2, //	首选const
		"no-debugger": process.env.NODE_ENV === "production" ? 2 : 0, // 生产环境禁止使用debugger
		"object-curly-spacing": [ // 大括号内是否允许空格
			2,
			"always", // always:在行首出现，且后面至少有一个空格，在行尾出现没有空格
			{
				objectsInObjects: true // 对象的属性值允许有空格
			}
		],
		"array-bracket-spacing": [2, "never"] // 数组前后是否加空格
	}
}
```
