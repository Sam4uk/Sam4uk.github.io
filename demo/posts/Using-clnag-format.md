---
title: "Форматуванняя коду ClangFormat"
date: 2020-12-07
# date: 2018-01-30T23:21:51+05:30
lastmod: 2020-12-07
publishdate: 2020-12-07
tags: ["C", "Cpp", "clang-format"]
comments: false

description: "Форматування коду C/C++ за допомогою Clang-Format"

author: "Lei Mao"
authorDesc: "Machine Learning, Artificial Intelligence, Computer Science"
authorImageUrl: https://leimao.github.io/images/author_images/Lei-Bio-Medium.jpg
# categories:
# - tutorials
# cover: "https://images.pexels.com/photos/965345/pexels-photo-965345.jpeg?cs=srgb&dl=pexels-markus-spiske-965345.jpg&fm=jpg"
draft: false
---


### Вступ

Коли над проектом працює кілька розробників слід дотримуватись правил форматування коду. Існують цілі збірники з правилами, як треба форматувати код. А якщо над кодом працює один розробник (у випадках пет проектів) код теж потрібно форматувати. Щоб якщо ви забажаєте показати своє творіння комусь код не має виглядати, як після обфускації. Процес форматування коду можна доручити якійсь утиліті, яка слідкуватиме за розміром відступу, або за довжиною рядка. А за вами лишиться чорнова робота по створенню коду та не забувати ставити розділові знаки.

Однією з таких утиліт є [clang-format](https://clang.llvm.org/docs/ClangFormat.html). Мені ця утиліта дуже сподобалась з першого погляду.

### Встановлення

```zsh
sudo apt-get install clang-format
```

### Конфігурація форматувальника

Для форматування коду нам потрібен файл конфігурації `.clang-format` в якому прописані правила за яким відбуватиметься форматування коду. Цей файл можу бути створений з кількох попередньо налаштваних стилів.

Щоб згенерувати `.clang-format` файл потрібно в терміналі виконати наступну команду:

```zsh
clang-format -style=google -dump-config > .clang-format
```

Ця утиліта за замовчуванням має передвстановлені стилі `google`, `chromium`, `mozilla`, `webkit`, `microsoft`.

Файл `.clang-format` можна модифікувати у будь-якому текстовому редакторі - всі налаштування конфігурації зберігаються у форматі `yaml` https://clang.llvm.org/docs/ClangFormatStyleOptions.html#

```yaml
---
Language:        Cpp
# BasedOnStyle:  Google
AccessModifierOffset: -1
AlignAfterOpenBracket: Align
AlignConsecutiveMacros: false
AlignConsecutiveAssignments: false
AlignConsecutiveDeclarations: false
AlignEscapedNewlines: Left
AlignOperands:   true
AlignTrailingComments: true
AllowAllArgumentsOnNextLine: true
AllowAllConstructorInitializersOnNextLine: true
AllowAllParametersOfDeclarationOnNextLine: true
AllowShortBlocksOnASingleLine: Never
AllowShortCaseLabelsOnASingleLine: false
AllowShortFunctionsOnASingleLine: All
AllowShortLambdasOnASingleLine: All
AllowShortIfStatementsOnASingleLine: WithoutElse
AllowShortLoopsOnASingleLine: true
AlwaysBreakAfterDefinitionReturnType: None
AlwaysBreakAfterReturnType: None
AlwaysBreakBeforeMultilineStrings: true
AlwaysBreakTemplateDeclarations: Yes
BinPackArguments: true
BinPackParameters: true
BraceWrapping:
  AfterCaseLabel:  false
  AfterClass:      false
  AfterControlStatement: false
  AfterEnum:       false
  AfterFunction:   false
  AfterNamespace:  false
  AfterObjCDeclaration: false
  AfterStruct:     false
  AfterUnion:      false
  AfterExternBlock: false
  BeforeCatch:     false
  BeforeElse:      false
  IndentBraces:    false
  SplitEmptyFunction: true
  SplitEmptyRecord: true
  SplitEmptyNamespace: true
BreakBeforeBinaryOperators: None
BreakBeforeBraces: Attach
BreakBeforeInheritanceComma: false
BreakInheritanceList: BeforeColon
BreakBeforeTernaryOperators: true
BreakConstructorInitializersBeforeComma: false
BreakConstructorInitializers: BeforeColon
BreakAfterJavaFieldAnnotations: false
BreakStringLiterals: true
ColumnLimit:     80
CommentPragmas:  '^ IWYU pragma:'
CompactNamespaces: false
ConstructorInitializerAllOnOneLineOrOnePerLine: true
ConstructorInitializerIndentWidth: 4
ContinuationIndentWidth: 4
Cpp11BracedListStyle: true
DeriveLineEnding: true
DerivePointerAlignment: true
DisableFormat:   false
ExperimentalAutoDetectBinPacking: false
FixNamespaceComments: true
ForEachMacros:
  - foreach
  - Q_FOREACH
  - BOOST_FOREACH
IncludeBlocks:   Regroup
IncludeCategories:
  - Regex:           '^<ext/.*\.h>'
    Priority:        2
    SortPriority:    0
  - Regex:           '^<.*\.h>'
    Priority:        1
    SortPriority:    0
  - Regex:           '^<.*'
    Priority:        2
    SortPriority:    0
  - Regex:           '.*'
    Priority:        3
    SortPriority:    0
IncludeIsMainRegex: '([-_](test|unittest))?$'
IncludeIsMainSourceRegex: ''
IndentCaseLabels: true
IndentGotoLabels: true
IndentPPDirectives: None
IndentWidth:     2
IndentWrappedFunctionNames: false
JavaScriptQuotes: Leave
JavaScriptWrapImports: true
KeepEmptyLinesAtTheStartOfBlocks: false
MacroBlockBegin: ''
MacroBlockEnd:   ''
MaxEmptyLinesToKeep: 1
NamespaceIndentation: None
ObjCBinPackProtocolList: Never
ObjCBlockIndentWidth: 2
ObjCSpaceAfterProperty: false
ObjCSpaceBeforeProtocolList: true
PenaltyBreakAssignment: 2
PenaltyBreakBeforeFirstCallParameter: 1
PenaltyBreakComment: 300
PenaltyBreakFirstLessLess: 120
PenaltyBreakString: 1000
PenaltyBreakTemplateDeclaration: 10
PenaltyExcessCharacter: 1000000
PenaltyReturnTypeOnItsOwnLine: 200
PointerAlignment: Left
RawStringFormats:
  - Language:        Cpp
    Delimiters:
      - cc
      - CC
      - cpp
      - Cpp
      - CPP
      - 'c++'
      - 'C++'
    CanonicalDelimiter: ''
    BasedOnStyle:    google
  - Language:        TextProto
    Delimiters:
      - pb
      - PB
      - proto
      - PROTO
    EnclosingFunctions:
      - EqualsProto
      - EquivToProto
      - PARSE_PARTIAL_TEXT_PROTO
      - PARSE_TEST_PROTO
      - PARSE_TEXT_PROTO
      - ParseTextOrDie
      - ParseTextProtoOrDie
    CanonicalDelimiter: ''
    BasedOnStyle:    google
ReflowComments:  true
SortIncludes:    true
SortUsingDeclarations: true
SpaceAfterCStyleCast: false
SpaceAfterLogicalNot: false
SpaceAfterTemplateKeyword: true
SpaceBeforeAssignmentOperators: true
SpaceBeforeCpp11BracedList: false
SpaceBeforeCtorInitializerColon: true
SpaceBeforeInheritanceColon: true
SpaceBeforeParens: ControlStatements
SpaceBeforeRangeBasedForLoopColon: true
SpaceInEmptyBlock: false
SpaceInEmptyParentheses: false
SpacesBeforeTrailingComments: 2
SpacesInAngles:  false
SpacesInConditionalStatement: false
SpacesInContainerLiterals: true
SpacesInCStyleCastParentheses: false
SpacesInParentheses: false
SpacesInSquareBrackets: false
SpaceBeforeSquareBrackets: false
Standard:        Auto
StatementMacros:
  - Q_UNUSED
  - QT_REQUIRE_VERSION
TabWidth:        8
UseCRLF:         false
UseTab:          Never
...

```

### Форматування коду

`Clang-Format` може відформатувати один файл або всі файли з однаковим розширенням. Наприклад, щоб відформатувати розширення .cpp, запустіть у терміналі таку команду.

```zsh
clang-format -i *.cpp
```

Щоб відформатувати всі файли .h, .c, .hpp, .cpp, .cu разом, виконайте наступну команду в терміналі.

```zsh
$ find . -regex '.*\.\(cpp\|hpp\|cu\|c\|h\)' -exec clang-format -style=file -i {} \;
```

[оригінал статті](https://leimao.github.io/blog/Clang-Format-Quick-Tutorial/)