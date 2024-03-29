---
sidebar_position: 1
title: Popular Rust Crates
---

## CLI Tools

CLI tools (binaries) written in Rust.

| Name | Tags | Description |
|-|-|-|
| [bat](https://github.com/sharkdp/bat) | cli,shell | Rust clone of cat CLI tool |
| [bottom](https://github.com/ClementTsang/bottom) | cli,shell,system | cross-platform graphical process/system monitor |
| [broot](https://github.com/Canop/broot) | cli,shell,filesystem | new way to see and navigate directory trees |
| [difftastic](https://github.com/Wilfred/difftastic) | cli,shell,diff,code | structural diff that understands syntax |
| [dog](https://github.com/ogham/dog) | cli,shell,dns,network | command-line DNS client |
| [dust](https://github.com/bootandy/dust) | cli,disk,shell,tui | more intuitive version of du |
| [eza](https://github.com/eza-community/eza) | cli,shell | replacement for ls |
| [fd](https://github.com/sharkdp/fd) | cli,shell | simple, fast and user-friendly alternative to 'find' |
| [felix](https://github.com/kyoheiu/felix) | cli,shell,filesystem | tui file manager with vim-like key mapping |
| [ffsend](https://github.com/timvisee/ffsend) | cli,shell,sharing,files | Easily and securely share files from the command line |
| [gitui](https://github.com/extrawurst/gitui) | cli,shell,git,code | terminal-ui for git |
| [gptman](https://github.com/rust-disk-partition-management/gptman) | cli,shell,disk,partition | CLI tool for Linux that allows you to copy a partition from one disk to another and more |
| [hyperfine](https://github.com/sharkdp/hyperfine) | cli,shell,benchmark | command-line benchmarking tool |
| [monolith](https://github.com/y2z/monolith) | cli,shell,html,web | save complete web pages as a single HTML file |
| [macchina](https://github.com/Macchina-CLI/macchina) | cli,shell,system | system information frontend |
| [ouch](https://github.com/ouch-org/ouch) | cli,shell,compression,filesystem | compression and decompression for your terminal |
| [procs](https://github.com/dalance/procs) | cli,shell | modern replacement for ps |
| [ripgrep](https://github.com/BurntSushi/ripgrep) | cli,shell | recursively searches directories for a regex pattern while respecting your gitignore |
| [RustScan](https://github.com/RustScan/RustScan) | cli,shell,nmap,network | Modern Port Scanner |
| [sd](https://github.com/chmln/sd) | cli,shell | Intuitive find & replace CLI (sed alternative) |
| [tealdeer](https://github.com/dbrgn/tealdeer) | cli,shell | very fast implementation of tldr |
| [tokei](https://github.com/XAMPPRocky/tokei) | cli,shell,code | displays statistics about your code |
| [topgrade](https://github.com/topgrade-rs/topgrade) | cli,shell,system | keeps your system up-to-date |
| [zellij](https://github.com/zellij-org/zellij) | cli,shell,tmux | terminal workspace with batteries included |
| [zoxide](https://github.com/ajeetdsouza/zoxide) | cli,shell | smarter cd command |

## Graphical Rust Tools

This section lists graphical tools that are built with Rust.

| Name | Tags | Description |
|-|-|-|
| [Helix](https://github.com/helix-editor/helix) | gui,text,editor | post-modern modal text editor |

## Terminal Libraries

Crates that allow you to manipulate terminal sessions.

| Name | Tags | Description |
|-|-|-|
| [clap](https://github.com/clap-rs/clap) | cli,shell | full featured, fast Command Line Argument Parser |
| [comfy-table](https://github.com/Nukesor/comfy-table) | cli,shell,tui | Build beautiful terminal tables with automatic content wrapping |
| [console](https://github.com/console-rs/console) | cli,shell,ansi | console and terminal abstraction |
| [crossterm](https://github.com/crossterm-rs/crossterm) | terminal | Cross-platform terminal library for Rust |
| [dialoguer](https://github.com/console-rs/dialoguer) | terminal,input | utility library for nice command line prompts |
| [indicatif](https://github.com/console-rs/indicatif) | terminal | command line progress reporting library |
| [ratatui](https://github.com/ratatui-org/ratatui) | tui,terminal | Rust library that's all about cooking up terminal user interfaces |

## Async

Crates that help you write asynchronous code in Rust.

| Name | Tags | Description |
|-|-|-|
| [tokio](https://github.com/tokio-rs/tokio) | async | runtime for writing reliable asynchronous applications with Rust |
| [rayon](https://github.com/rayon-rs/rayon) | parallel,async | data parallelism library |
| [async-std](https://github.com/async-rs/async-std) | async | Async version of the Rust standard library |
| [smol](https://github.com/smol-rs/smol) | async | small and fast async runtime for Rust |

## Other

| Name | Tags | Description |
|-|-|-|

| [nom](https://github.com/rust-bakery/nom) | parser | Rust parser combinator framework |
| [regex](https://github.com/rust-lang/regex) | regex,parser | implementation of regular expressions for Rust |
| [tl](https://crates.io/crates/tl) | html,parser | fast HTML parser |
| [chromiumoxide](https://github.com/mattsse/chromiumoxide) | chrome,browser | Chrome Devtools Protocol Rust API |

## Data

Crates dealing with database platforms and data transformation.

| Name | Tags | Description |
|-|-|-|
| [fake](https://github.com/cksac/fake-rs) | data,generator | library for generating fake data |
| [mongodb](https://github.com/mongodb/mongo-rust-driver) | database,nosql | official MongoDB Rust Driver |
| [polars](https://github.com/pola-rs/polars/) | data | Fast multi-threaded, hybrid-out-of-core query engine focussing on DataFrame front-ends |
| [postgres](https://github.com/sfackler/rust-postgres) | data,database,postgres,sql | Native PostgreSQL driver for the Rust programming language |
| [quickwit](https://github.com/quickwit-oss/quickwit) | data,search | Sub-second search & analytics engine on cloud storage |
| [qdrant](https://github.com/qdrant/qdrant) | data,search,vector | vector similarity search engine and vector database |
| [serde](https://github.com/serde-rs/serde) | data,json | Serialization framework for Rust |
| [skim](https://github.com/lotabout/skim) | data,search | Fuzzy Finder in rust |
| [sqlx](https://github.com/launchbadge/sqlx) | data,sql,database | database agnostic Rust SQL Toolkit |
| [watchexec](https://github.com/watchexec/watchexec) | data,filesystem | Executes commands in response to file modifications |

## Networking

Crates dealing with exposing or consuming network services.

| Name | Tags | Description |
|-|-|-|
| [actix-web](https://github.com/actix/actix-web) | http,web | powerful, pragmatic, and extremely fast web framework for Rust |
| [curl-rust](https://github.com/alexcrichton/curl-rust) | http,web | Rust bindings to libcurl |
| [hyper](https://github.com/hyperium/hyper) | http,web | low-level HTTP library for Rust |
| [isahc](https://github.com/sagebind/isahc/) | http,web | practical HTTP client that is fun to use |
| [quiche](https://github.com/cloudflare/quiche) | http3,web | implementation of the QUIC transport protocol and HTTP/3 |
| [reqwest](https://github.com/seanmonstar/reqwest) | http,web | easy and powerful Rust HTTP Client |
| [Rocket](https://github.com/SergioBenitez/Rocket) | http,api,rest | Web framework for Rust |
| [surf](https://github.com/http-rs/surf) | http,web | Fast and friendly HTTP client framework for async Rust |
| [ureq](https://github.com/algesten/ureq) | http,web | A simple, safe HTTP client |

## User Interface

Crates dealing with building graphical user interfaces (GUI).

| Name | Tags | Description |
|-|-|-|
| [Basalt](https://github.com/AustinJ235/basalt) | gui | window/ui framework for building desktop applications |
| [Dioxus](https://github.com/DioxusLabs/dioxus/) | gui, react | Fullstack GUI library for desktop, web, mobile, and more |
| [Dominator](https://github.com/Pauan/rust-dominator) | gui, reactive | Zero-cost ultra-high-performance declarative DOM library using FRP signals for Rust |
| [egui](https://github.com/emilk/egui) | gui | easy-to-use immediate mode GUI in Rust (web + native) |
| [Xilem](https://github.com/linebender/xilem) | gui | experimental Rust native UI framework |
| [gtk3](https://github.com/gtk-rs/gtk3-rs) | gui, gtk, linux | Rust bindings for GTK 3 |
| [gtk4](https://github.com/gtk-rs/gtk4-rs) | gui, gtk, linux | Rust bindings for GTK 4 |
| [Iced](https://github.com/iced-rs/iced) | gui | cross-platform GUI library for Rust |
| [imgui](https://github.com/imgui-rs/imgui-rs) | gui, imgui | Rust bindings for Dear ImGui |
| [qmetaobject](https://github.com/woboq/qmetaobject-rs) | gui, qt | Integrate Qml and Rust |
| [relm4](https://github.com/Relm4/Relm4) | gui, gtk | Idiomatic, GTK+-based GUI library |
| [slint](https://github.com/slint-ui/slint) | gui | declarative GUI toolkit to build native user interfaces for applications |
| [tauri](https://github.com/tauri-apps/tauri) | gui | Build smaller, faster, and more secure desktop applications with a web frontend |
| [WinSafe](https://github.com/rodrigocfd/winsafe) | gui, windows | Windows API and GUI in safe, idiomatic Rust |
| [tray-item-rs](https://github.com/olback/tray-item-rs) | gui | Multi-platform system tray indicator |

## Graphics

Crates dealing with 2D raster and vector media manipulation.

| Name | Tags | Description |
|-|-|-|
| [ash](https://github.com/ash-rs/ash) | graphics, vulkan | lightweight wrapper around Vulkan |
| [glium](https://github.com/glium/glium) | graphics, opengl | Safe OpenGL wrapper for the Rust language |
| [image](https://github.com/image-rs/image) | image,file | Encoding and decoding images in Rust |
| [miniquad](https://github.com/not-fl3/miniquad) | graphics | Cross platform rendering in Rust |
| [resvg](https://github.com/RazrFalcon/resvg) | svg,image,vector | SVG rendering library |
| [vulkano](https://github.com/vulkano-rs/vulkano) | graphics | Safe and rich Rust wrapper around the Vulkan API |
| [WebRender](https://github.com/servo/webrender) | browser
| [wgpu](https://github.com/gfx-rs/wgpu) | graphics | Cross-platform, safe, pure-rust graphics api |


## Hardware

| Name | Tags | Description |
|-|-|-|
| [hidapi](https://github.com/libusb/hidapi) | usb,hid | cross-platform library for communicating with HID devices |
| [sysinfo](https://github.com/GuillaumeGomez/sysinfo) | system,hardware | Cross-platform library to fetch system information |

## Profiling

Crates that help analyze performance of Rust applications.

| Name | Tags | Description |
|-|-|-|
| [criterion](https://github.com/bheisler/criterion.rs) | benchmark,performance | Statistics-driven benchmarking library for Rust |
| [profiling](https://github.com/aclysma/profiling) | profiling,performance | thin abstraction over instrumented profiling crates like puffin, optick, tracy, and superluminal-perf |
| [inferno](https://github.com/jonhoo/inferno) | profiling,performance | Rust port of FlameGraph |