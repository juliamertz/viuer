# viuer
Display images in the terminal with ease.

![ci](https://github.com/atanunq/viuer/workflows/ci/badge.svg)

`viuer` is a Rust library that makes it easy to show images in the terminal. It has a straightforward
interface and is configured through a single struct. The default printing method is through
lower half blocks (▄ or \u2585). However, [Kitty graphics protocol](https://sw.kovidgoyal.net/kitty/graphics-protocol.html)
is used if support for it is detected, resulting in full resolution images in the terminal.


For a demo of the library's usage and example screenshots, see [`viu`](https://github.com/atanunq/viu).

## Examples

```toml
# in Cargo.toml, under [dependencies]
viuer = "0.1"
```
```rust
// in src/main.rs
use viuer::{print_from_file, Config};

fn main() {
    let conf = Config {
        // set offset
        x: 20,
        y: 4,
        // set dimensions
        width: Some(80),
        height: Some(25),
        ..Default::default()
    };

    // starting from row 4 and column 20,
    // display `img.jpg` with dimensions 80x25 (in terminal cells)
    // note that the actual resolution in the terminal will be 80x50
    print_from_file("img.jpg", &conf).expect("Image printing failed.");
}
```

Or if you have a [DynamicImage](https://docs.rs/image/*/image/enum.DynamicImage.html), you can use it directly:
```rust
// ..Config setup

let img = image::DynamicImage::ImageRgba8(image::RgbaImage::new(20, 10));
viuer::print(&img, &conf).expect("Image printing failed.");
```

## Docs
Check the [full documentation](https://docs.rs/crate/viuer) for examples and all the configuration options.