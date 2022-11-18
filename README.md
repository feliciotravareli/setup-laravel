# Setup de um Projeto Laravel

## [Criar novo projeto laravel](https://laravel.com/docs/9.x#installation-via-composer)

```bash
composer create-project laravel/laravel exemplo
```

---

## 1. [PHP CS Fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer)

[Setup](https://github.com/FriendsOfPHP/PHP-CS-Fixer/blob/master/doc/installation.rst)

```
composer require friendsofphp/php-cs-fixer --dev  
```

### Config file

`.php-cs-fixer.php`

```php
<?php

use PhpCsFixer\Config;
use PhpCsFixer\Finder;

$rules = [
    '@PSR2'                                       => true,
    'align_multiline_comment'                     => false,
    'array_indentation'                           => true,
    'array_syntax'                                => ['syntax' => 'short'],
    'binary_operator_spaces'                      => [
        'default' => 'align_single_space_minimal',
    ],
    'blank_line_after_namespace'                  => true,
    'blank_line_after_opening_tag'                => false,
    'blank_line_before_statement'                 => ['statements' => ['break', 'continue', 'declare', 'return', 'throw', 'try']],
    'braces'                                      => [
        'allow_single_line_closure'                   => false,
        'position_after_anonymous_constructs'         => 'same',
        'position_after_control_structures'           => 'same',
        'position_after_functions_and_oop_constructs' => 'next',
    ],
    'cast_spaces'                                 => ['space' => 'none'],
    // 'class_attributes_separation' => [
    //     'elements' => ['method', 'property'],
    // ],
    'no_unused_imports'                           => true,
    'combine_consecutive_issets'                  => false,
    'combine_consecutive_unsets'                  => false,
    'combine_nested_dirname'                      => false,
    'comment_to_phpdoc'                           => false,
    'compact_nullable_typehint'                   => false,
    'concat_space'                                => ['spacing' => 'one'],
    'constant_case'                               => [
        'case' => 'lower',
    ],
    'date_time_immutable'                         => false,
    'declare_equal_normalize'                     => [
        'space' => 'single',
    ],
    'declare_strict_types'                        => false,
    'dir_constant'                                => false,
    'doctrine_annotation_array_assignment'        => false,
    'doctrine_annotation_braces'                  => false,
    'doctrine_annotation_indentation'             => [
        'ignored_tags'       => [],
        'indent_mixed_lines' => true,
    ],
    'doctrine_annotation_spaces'                  => [
        'after_argument_assignments'     => false,
        'after_array_assignments_colon'  => false,
        'after_array_assignments_equals' => false,
    ],
    'elseif'                                      => false,
    'encoding'                                    => true,
    'indentation_type'                            => true,
    'no_useless_else'                             => true,
    'no_useless_return'                           => true,
    'ordered_imports'                             => true,
    'single_quote'                                => false,
    'ternary_operator_spaces'                     => true,
    'no_extra_blank_lines'                        => true,
    'no_multiline_whitespace_around_double_arrow' => true,
    'multiline_whitespace_before_semicolons'      => true,
    'no_singleline_whitespace_before_semicolons'  => true,
    'no_spaces_around_offset'                     => true,
    'ternary_to_null_coalescing'                  => true,
    'whitespace_after_comma_in_array'             => true,
    'trim_array_spaces'                           => true,
    'unary_operator_spaces'                       => true,
];

$finder = new Finder();

$finder->in([
    __DIR__ . '/app',
    __DIR__ . '/database',
]);

$config = new Config();

$config->setIndent('    ');

$config
    ->setRiskyAllowed(false)
    ->setRules($rules)
    ->setFinder($finder);

return $config;
```

### Run

`./vendor/bin/php-cs-fixer fix `

### Ref

[Workenck/Shift](https://gist.github.com/laravel-shift/cab527923ed2a109dda047b97d53c200)

---

## 2. [Code Sniffer](https://github.com/squizlabs/PHP_CodeSniffer)

```bash
composer require squizlabs/php_codesniffer --dev
```

### Config file

`phpcs.xml`

```xml
<?xml version="1.0"?>
<ruleset
    name="Laravel Standards"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:noNamespaceSchemaLocation="https://raw.githubusercontent.com/squizlabs/PHP_CodeSniffer/master/phpcs.xsd"
>
    <description>PHP Codesniffer ruleset to follow Laravel's coding style</description>
    <rule ref="Generic.Classes.DuplicateClassName">
        <exclude name="Generic.CodeAnalysis.EmptyStatement.DetectedIf"/>
    </rule>
    <rule ref="Generic.CodeAnalysis.EmptyStatement"/>
    <rule ref="Generic.CodeAnalysis.ForLoopShouldBeWhileLoop"/>
    <rule ref="Generic.CodeAnalysis.ForLoopWithTestFunctionCall"/>
    <rule ref="Generic.CodeAnalysis.JumbledIncrementer"/>
    <rule ref="Generic.CodeAnalysis.UnconditionalIfStatement"/>
    <rule ref="Generic.CodeAnalysis.UnnecessaryFinalModifier"/>
    <rule ref="Generic.CodeAnalysis.UnusedFunctionParameter">
        <exclude-pattern>/app/Http/Resources/*\.php</exclude-pattern>
        <exclude-pattern>/routes/*\.php</exclude-pattern>
    </rule>
    <rule ref="Generic.CodeAnalysis.UselessOverridingMethod"/>
    <rule ref="Generic.Commenting.DocComment">
        <exclude name="Generic.Commenting.DocComment.TagValueIndent"/>
        <exclude name="Generic.Commenting.DocComment.NonParamGroup"/>
    </rule>
    <rule ref="Generic.ControlStructures.InlineControlStructure"/>
    <rule ref="Generic.Files.ByteOrderMark"/>
    <rule ref="Generic.Files.LineEndings">
        <exclude name="Generic.Files.LineEndings.InvalidEOLChar"/>
    </rule>
    <rule ref="Generic.Formatting.DisallowMultipleStatements"/>
    <!-- <rule ref="Generic.Formatting.SpaceAfterCast"/> -->
    <rule ref="Generic.Functions.CallTimePassByReference"/>
    <rule ref="Generic.Functions.FunctionCallArgumentSpacing"/>
    <rule ref="Generic.Functions.OpeningFunctionBraceBsdAllman"/>
    <rule ref="Generic.Metrics.CyclomaticComplexity">
        <properties>
            <property name="complexity" value="20"/>
            <property name="absoluteComplexity" value="25"/>
        </properties>
    </rule>
    <rule ref="Generic.Metrics.NestingLevel">
        <properties>
            <property name="nestingLevel" value="5"/>
            <property name="absoluteNestingLevel" value="15"/>
        </properties>
    </rule>
    <rule ref="Generic.NamingConventions.ConstructorName"/>
    <rule ref="Generic.PHP.LowerCaseConstant"/>
    <rule ref="Generic.PHP.DeprecatedFunctions"/>
    <rule ref="Generic.PHP.DisallowShortOpenTag"/>
    <rule ref="Generic.PHP.ForbiddenFunctions"/>
    <rule ref="Generic.PHP.NoSilencedErrors"/>
    <rule ref="Generic.WhiteSpace.DisallowTabIndent"/>
    <rule ref="Generic.WhiteSpace.ScopeIndent">
        <properties>
            <property name="indent" value="4"/>
            <property name="tabIndent" value="true"/>
        </properties>
    </rule>
    <rule ref="MySource.PHP.EvalObjectFactory"/>
    <rule ref="PSR1.Classes.ClassDeclaration"/>
    <rule ref="PSR1.Files.SideEffects">
        <exclude-pattern>*/artisan</exclude-pattern>
    </rule>
    <rule ref="PSR1.Files.SideEffects"/>
    <rule ref="PSR2.Classes.ClassDeclaration"/>
    <rule ref="PSR2.Classes.PropertyDeclaration"/>
    <rule ref="PSR2.Classes.PropertyDeclaration.Underscore">
        <type>error</type>
    </rule>
    <rule ref="PSR2.ControlStructures.ControlStructureSpacing"/>
    <rule ref="PSR2.ControlStructures.ElseIfDeclaration"/>
    <rule ref="PSR2.ControlStructures.SwitchDeclaration"/>
    <rule ref="PSR2.Files.EndFileNewline"/>
    <rule ref="PSR2.Methods.MethodDeclaration"/>
    <rule ref="PSR2.Methods.MethodDeclaration.Underscore">
        <type>error</type>
    </rule>
    <rule ref="PSR2.Namespaces.NamespaceDeclaration"/>
    <rule ref="PSR2.Namespaces.UseDeclaration"/>
    <rule ref="PSR1">
        <exclude-pattern>*.php</exclude-pattern>
        <exclude name="PSR1.Methods.CamelCapsMethodName.NotCamelCaps"/>

        <exclude-pattern>database/*</exclude-pattern>
    </rule>
    <rule ref="PSR2">
        <exclude name="PSR2.ControlStructures.SwitchDeclaration.BodyOnNextLineCASE" />
        <properties>
            <property name="lineLimit" value="130"/>
            <property name="absoluteLineLimit" value="135"/>
        </properties>
    </rule>
    <rule ref="Squiz.Arrays.ArrayDeclaration">
        <exclude name="Squiz.Arrays.ArrayDeclaration.ValueNotAligned" />
        <exclude name="Squiz.Arrays.ArrayDeclaration.KeyNotAligned" />
        <exclude name="Squiz.Arrays.ArrayDeclaration.DoubleArrowNotAligned" />
        <exclude name="Squiz.Arrays.ArrayDeclaration.ValueNotAligned" />
        <exclude name="Squiz.Arrays.ArrayDeclaration.CloseBraceNotAligned" />
        <exclude name="Squiz.Arrays.ArrayDeclaration.ValueNoNewline" />
        <exclude name="Squiz.Arrays.ArrayDeclaration.MultiLineNotAllowed" />
        <exclude name="Squiz.Arrays.ArrayDeclaration.SingleLineNotAllowed" />
        <exclude name="Squiz.Arrays.ArrayDeclaration.IndexNoNewline" />
        <exclude name="Squiz.Arrays.ArrayDeclaration.CloseBraceNewLine" />
        <exclude name="Squiz.Functions.MultiLineFunctionDeclaration.NewlineBeforeOpenBrace" />
        <exclude name="Squiz.Arrays.ArrayDeclaration.NoKeySpecified" />
        <exclude name="Squiz.Arrays.ArrayDeclaration.KeySpecified" />
    </rule>
    <rule ref="Squiz.PHP.CommentedOutCode"/>
    <rule ref="Squiz.PHP.DisallowSizeFunctionsInLoops"/>
    <rule ref="Squiz.PHP.DiscouragedFunctions">
        <properties>
            <property name="error" value="true"/>
        </properties>
    </rule>
    <rule ref="Squiz.PHP.Eval"/>
    <rule ref="Squiz.PHP.GlobalKeyword"/>
    <rule ref="Squiz.PHP.Heredoc"/>
    <rule ref="Squiz.PHP.LowercasePHPFunctions"/>
    <rule ref="Squiz.PHP.NonExecutableCode"/>
    <rule ref="Squiz.Scope.MemberVarScope"/>
    <rule ref="Squiz.Scope.MethodScope"/>
    <rule ref="Squiz.Scope.StaticThisUsage"/>
    <rule ref="Squiz.WhiteSpace.CastSpacing"/>
    <rule ref="Squiz.WhiteSpace.ControlStructureSpacing"/>
    <rule ref="Squiz.WhiteSpace.LanguageConstructSpacing"/>
    <rule ref="Squiz.WhiteSpace.LogicalOperatorSpacing"/>
    <rule ref="Squiz.WhiteSpace.ObjectOperatorSpacing">
        <properties>
            <property name="ignoreNewlines" value="true"/>
        </properties>
    </rule>
    <rule ref="Squiz.WhiteSpace.OperatorSpacing">
        <properties>
            <property name="ignoreNewlines" value="true"/>
        </properties>
    </rule>
    <rule ref="Squiz.WhiteSpace.PropertyLabelSpacing"/>
    <rule ref="Squiz.WhiteSpace.ScopeClosingBrace"/>
    <rule ref="Squiz.WhiteSpace.ScopeKeywordSpacing"/>
    <rule ref="Squiz.WhiteSpace.SemicolonSpacing"/>
    <rule ref="Squiz.Strings.DoubleQuoteUsage.NotRequired"/>
    <rule ref="Zend.Files.ClosingTag"/>

    <file>app</file>
    <file>config</file>
    <file>public</file>
    <file>resources</file>
    <file>routes</file>
    <file>tests</file>

    <exclude-pattern>*/.phpstorm.meta.php</exclude-pattern>
    <exclude-pattern>*/_ide_helper.php</exclude-pattern>
    <exclude-pattern>*/cache/*</exclude-pattern>
    <exclude-pattern>*/config/*</exclude-pattern>
    <exclude-pattern>*/database/*</exclude-pattern>
    <exclude-pattern>*/docs/*</exclude-pattern>
    <exclude-pattern>*/migrations/*</exclude-pattern>
    <exclude-pattern>*/storage/*</exclude-pattern>
    <exclude-pattern>*/public/index.php</exclude-pattern>
    <exclude-pattern>*/resources/lang/*</exclude-pattern>
    <exclude-pattern>*/vendor/*</exclude-pattern>
    <exclude-pattern>*/*.js</exclude-pattern>
    <exclude-pattern>*/*.css</exclude-pattern>
    <exclude-pattern>*/*.xml</exclude-pattern>
    <exclude-pattern>*/*.blade.php</exclude-pattern>
    <exclude-pattern>*/autoload.php</exclude-pattern>
    <exclude-pattern>*/Console/Kernel.php</exclude-pattern>
    <exclude-pattern>*/Exceptions/Handler.php</exclude-pattern>
    <exclude-pattern>*/Http/Kernel.php</exclude-pattern>

    <arg name="colors"/>
    <arg value="spv"/>
    <ini name="memory_limit" value="128M"/>
</ruleset>
```

### Run

`./vendor/bin/cs`

### Ref

[laravel-phpcs](https://github.com/mreduar/laravel-phpcs/blob/master/phpcs.xml)

---

## 3. [LaraStan](https://github.com/nunomaduro/larastan)

```bash
composer require nunomaduro/larastan:^2.0 --dev
```

### Config file

`phpstan.neon`

```neon
includes:
    - ./vendor/nunomaduro/larastan/extension.neon

parameters:

    paths:
        - app

    # The level 9 is the highest level
    level: 5

    ignoreErrors:
        - '#PHPDoc tag @var#'

    excludePaths:
        - ./*/*/FileToBeExcluded.php

    checkMissingIterableValueType: false
```

### Run

`./vendor/bin/phpstan analyse`

### Ref

[PHPStan](https://phpstan.org/config-reference)

---

## 4. [Pest](https://pestphp.com/)

```bash
composer require pestphp/pest --dev --with-all-dependencies
composer require pestphp/pest-plugin-laravel --dev
composer require pestphp/pest-plugin-parallel --dev

php artisan pest:install
```

### Run

`./vendor/bin/pest --parallel`

---

## 5. [DebugBar](https://github.com/barryvdh/laravel-debugbar)

```bash
composer require barryvdh/laravel-debugbar --dev
```

---

## 6. [Telescope](https://laravel.com/docs/9.x/telescope#local-only-installation)

```bash
composer require laravel/telescope --dev

php artisan telescope:install

php artisan migrate
```

Add in file `App\Providers\AppServiceProvider`:

```php
public function register()
{
    if ($this->app->environment('local')) {
        $this->app->register(\Laravel\Telescope\TelescopeServiceProvider::class);
        $this->app->register(TelescopeServiceProvider::class);
    }
}
```

Adding the following to your `composer.json` file:

```json
"extra": {
    "laravel": {
        "dont-discover": [
            "laravel/telescope"
        ]
    }
},
```

_Descomentar: `Telescope::night();` no arquivo: `TelescopeServiceProvider`._

---

## Git Hooks

### Pre-Push

#### file `.git/hooks/pre-push`

```shell
#!/bin/sh


NC='\033[0m'
BBlue='\033[1;34m'
BRed='\033[1;31m'

NAME=$(git branch | grep '*' | sed 's/* //')
echo "\nRunning pre-push hook on: ${BBlue}" $NAME "${NC}\n"

# ---------------------------------------------------------------------------------------------------
# 1. Laravel Stan
echo "\n\n${BBlue}1. Larastan (PHPStan) ${NC}"
./vendor/bin/phpstan analyse

STATUS_CODE=$?

if [ $STATUS_CODE -ne 0 ]; then
    echo "${BRed}1.... larastan/phpstan: deu ruim ${NC}"
    exit 1
fi

# ---------------------------------------------------------------------------------------------------
# 2. PHP Code Sniffer
echo "\n\n${BBlue}2. PHP Code Sniffer ${NC}"
./vendor/bin/phpcs --standard=phpcs.xml

STATUS_CODE=$?

if [ $STATUS_CODE -ne 0 ]; then
    echo "${BRed}2.... php code sniffer${NC}"
    exit 1
fi

# ---------------------------------------------------------------------------------------------------
# 3. PHP Code Fixer
echo "\n\n${BBlue}3. PHP Code Fixer ${NC}"
./vendor/bin/php-cs-fixer fix --dry-run --using-cache=no --verbose --stop-on-violation

STATUS_CODE=$?

if [ $STATUS_CODE -ne 0 ]; then
    echo "${BRed}3.... php code fixer${NC}"
    exit 1
fi

# ---------------------------------------------------------------------------------------------------
# 4. PHP Tests
echo "\n\n${BBlue}4. PHP Unit Tests (Pest) ${NC}"
./vendor/bin/pest --parallel

STATUS_CODE=$?

if [ $STATUS_CODE -ne 0 ]; then
    echo "${BRed}4.... phpunit/pest${NC}"
    exit 1
fi

echo "${BBlue}pushing...${NC}\n"

```

---

### pre-rebase

#### file `.git/hooks/pre-rebase`

```shell
#!/bin/sh
# Disallow all rebasing

NC='\033[0m'
BRed='\033[1;31m'

echo -e "\n${BRed}pre-rebase: Rebase is dangerous! 👿️ Don't do it.${NC}\n"

exit 1

```

---

### commit-msg

#### file `.git/hooks/commit-msg`

```shell
#!/bin/sh

REGEX_ISSUE_ID="[a-zA-Z0-9,\.\_\-]+-[0-9]+"

NC='\033[0m'
BBlue='\033[1;34m'
BRed='\033[1;31m'

# Find current branch name
BRANCH_NAME=$(git symbolic-ref --short HEAD)

# Extract issue id from branch name
ISSUE_ID=$(echo "$BRANCH_NAME" | grep -o -E "$REGEX_ISSUE_ID")
if [-z "$ISSUE_ID"]; then
    echo -e "${BRed}Branch doesn't have Jira task code on itq....${NC}"
    echo -e "${BBlue}You can use ${BRed}git commit -m \"\" --no-verify${BBlue} to avoid this hook.${NC}"
    exit 1
fi
echo "$ISSUE_ID"': '$(cat "$1") > "$1"
```

---
