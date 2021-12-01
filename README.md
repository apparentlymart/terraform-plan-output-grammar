# TextMate-style Grammar for Terraform Plan Diff Output

This repository contains a TextMate-style language grammar for tokenizing the
human-oriented output from the `terraform show PLANFILE` command in
HashiCorp Terraform.

This is not a typical programming language but instead more of a domain-specific
diff representation intended for human consumption. The goal here is therefore
just to help call out some interesting tokens that might be interesting to
highlight when including a Terraform plan diff in a place which uses inferred
highlighting information, such as Markdown literal blocks in systems which use
TextMate-style grammars to format their contents.

The goal is to provide at least enough tokens to roughly recreate the
formatting Terraform would typically produce itself in a virtual terminal using
escape sequences, though it also includes some additional detail in case it's
useful to achieve a more detailed highlighting result than Terraform would
typically be able to achieve within the constraints of a terminal.

Because this is not a typical use-case for TextMate-style grammars, the scopes
selected are rather idiosyncratic and intended to stand a reasonable chance of
matching rules in existing themes designed for more "normal" languages, because
it's unlikely that most rendering environments would have rules specifically
for this very-specialized grammar.

## Testing

This grammar has test cases under the `tests` directory which are intended for
use with
[`vscode-tmgrammar-test`](https://github.com/PanAeon/vscode-tmgrammar-test).

To run those tests, install that tool and then run a command like the
following:

```shell
vscode-tmgrammar-test -s 'text.tfplandiff' -g 'terraformPlanDiff.tmLanguage.json' -t './tests/*'
```

The test only catches incorrect and missing tokens, and will not catch _new_
tokens that were not previously mentioned in the test. When adding new
tokens to the grammar it's important to visit the existing test cases and
introduce new assertions for locations where those new tokens ought to apply.