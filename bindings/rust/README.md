# tree-sitter-cairo

This crate provides a Cairo grammar for the [tree-sitter][] parsing library. To
use this crate, add it to the `[dependencies]` section of your `Cargo.toml`
file. (Note that you will probably also need to depend on the
[`tree-sitter`][tree-sitter crate] crate to use the parsed result in any useful
way.)

```toml
[dependencies]
tree-sitter = "~0.20.9"
tree-sitter-cairo = "1.0.0"
```

Typically, you will use the [language][language func] function to add this
grammar to a tree-sitter [Parser][], and then use the parser to parse some code:

```rust
let cairo_0_code = r#"
func uint256_signed_lt{range_check_ptr}(a: Uint256, b: Uint256) -> (res: felt) {
    let (a, _) = uint256_add(a, cast((low=0, high=2 ** 127), Uint256));
}
"#;
let mut parser = Parser::new();
parser.set_language(tree_sitter_cairo::language()).expect("Error loading Cairo grammar");
let cairo_0_parsed = parser.parse(code, None);

let cairo_1_code = r#"
impl ArrayIndex<T> of IndexView<Array<T>, usize, @T> {
    fn index(self: @Array<T>, index: usize) -> @T {
        array_at(self, index).unbox()
    }
}
"#;
let cairo_1_parsed = parser.parse(code, None);
```

If you have any questions, please reach out to us in the [tree-sitter
discussions] page.

[language func]: https://docs.rs/tree-sitter-cairo/*/tree_sitter_cairo/fn.language.html
[parser]: https://docs.rs/tree-sitter/*/tree_sitter/struct.Parser.html
[tree-sitter]: https://tree-sitter.github.io/
[tree-sitter crate]: https://crates.io/crates/tree-sitter
[tree-sitter discussions]: https://github.com/tree-sitter/tree-sitter/discussions
