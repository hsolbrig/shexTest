# shexTest

## Directories:
### `schemas`

* Test schemas in ShExC (`.shex`), ShExJ (`.json`) and sometimes SHACL (`.shacl`).

The ShExC and ShExJ files with the same stem name are equivalent.
A ShExC syntax test consists of these steps:

* parse the ShExC version of the document with some base URI.
* parse the ShExJ, as JSON; evaluate the values of the following as relative IRIs:
  * values of the `start`, `inclusion`, `predicate`, and `datatype` properties.
  * shape names (keys in the `shapes` object).
  * terms in `values` properties.
* ensure that no `ValueAnd` or `ValueOr` expression contains `ValueAnd` or `ValueOr` expressions in the list of `valueExprs`.
* the two parsed products should be equivalent, with blank node substitution.


## `negativeSyntax`
These tests should raise errors when parsed, noting the rule about nested `ValueAnd` and `ValueOr` expressions.

### `validation`

* Validation tests in a manifest (Turtle - `manifest.ttl`, [ShExJ][http://shex.io/primer/ShExJ) - `manifest.json`).
* Input data in Turtle (`.ttl`).
* [ShEx Results format](http://shex.io/primer/ShExJ) (`.val`).

A ShEx validator is `logic-conformant` when it returns success for the tests of type `ValidationTest` and failure for the tests of type `ValidationFailure`.
A ShEx validator is `result-conformant` (experimental) when it executes as `ValidationTest` and produces the same result structure as produced by this procedure:
* parse the result file as JSON.
* parse the ShExJ, as JSON; evaluate the values of the following as relative IRIs:
  * values of the `node`, `shape`, `subject`, `predicate`, and `object` properties.
* the two parsed products should be equivalent, with blank node substitution.
A ShEx validator is `error-conformant` (even more experimental) when it executes a `ValidationFailure` and produces the same result structure as produced by the procedure above.
