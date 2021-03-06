Diary of Rust VR
================

-------------------------
### 2016.08.21 c4augustus

__19:00: created local crates.io index to support offline programming__
  * `cd ~/v/dev/copyleft/group/c4a/repo`
  * `git clone --bare https://github.com/rust-lang/crates.io-index.git`
  * created and added to `~/v/dev/copyleft/group/.cargo/config`
    __@@@ BUT COMMENTED IT OUT BECAUSE IT REQUIRES ALL SOURCE TO BE LOCAL__
~~~
  #[registry]
  #index = "file:///Users/?????/v/dev/copyleft/group/c4a/repo/crates.io-index.git"
~~~

-------------------------
### 2016.09.03 c4augustus

__21:00: cloned gfx-rs/gfx and configured for glutin instead of glfw__
  * `cd rustvr/repo`
  * `git clone https://github.com/gfx-rs/gfx.git`

__21:30: upgraded rust from 1.9 to 1.11__

__22:30: built gfx__
  * `cd rustvr/repo/gfx`
  * `cargo clean`
  * `cargo run --example cube`
    #### @@@ FAILED:
~~~
   Compiling gfx_device_metal v0.1.0 (file:///Users/?????/v/dev/copyleft/rustvr/repo/gfx/src/backend/metal)
src/backend/metal/src/command.rs:25:5: 25:27 error: unresolved import `gfx_core::shade::Stage`. Maybe a missing `extern crate gfx_core`? [E0432]
src/backend/metal/src/command.rs:25 use gfx_core::shade::Stage;
~~~
  * `git checkout v0.12`
  * `cargo clean`
  * `cargo build`
  * `cargo run --example code`
    #### !!! SUCCESS

__24:00: started copying gfx example source: terrain__
  * copied `gfx/examples/terrain/main.rs` to `??????/src/main.rs`
  * copied `gfx/examples/terrain/data/` to `??????/src/data/`
  * copied `gfx/examples/terrain/shader/` to `??????/src/shader/`
  * edited `Cargo.toml`, extracted what's needed from `gfx/Cargo.toml`
  * `cargo clean`
  * `cargo build`
  * `cargo run`
    #### !!! SUCCESS

-------------------------
### 2016.09.12 c4augustus

__13:00: cloned Valve's OpenVR__
  * `cd rustvr/repo/_consider`
  * `git clone https://github.com/ValveSoftware/openvr.git`

__13:30: configure and built openvr-rs__
  * `cd rustvr/repo/_consider/openvr-rs`
  * `cargo build`
  * `cd example`
  * `vim build.rs`
    + changed win64 `dll` filenames to osx32 `dynlib`
  * `vim src/lib.rs`
    + changed win64 `dll` filenames to osx32 `dynlib`
  * `cargo run`
    #### @@@ FAILED BECAUSE OPENVR WON'T WORK ON MAC:
~~~
  thread 'main' panicked at 'OpenVR init: Init_PathRegistryNotFound', ../src/libcore/result.rs:788
~~~
  * `RUST_BACKTRACE=1 cargo run`

__14:00: cloned rust-openvr__
  * `cd rustvr/repo/_consider`
  * `git clone https://github.com/rust-openvr/rust-openvr.git`
  * `cd rust-openvr`
  * `cargo run --example camera`
    #### @@@ FAILED BECAUSE OPENVR WON'T WORK ON MAC:
~~~
  Failed to create IVRSystem subsystem Error { raw: EVRInitError_VRInitError_Init_PathRegistryNotFound }
~~~

__14:30: attempted to build libovr-rs__
  * `cd rustvr/repo/_consider/openvr-rs`
  * `cargo build`
    #### @@@ FAILED BECAUSE IT ONLY BUILDS ON WINDOWS
~~~
  error: main function not found
~~~

__14:30: attempted to build rovr__
  * `cd rustvr/repo/_consider/rovr`
  * `cargo build`
    #### @@@ FAILED BECAUSE ITS RUST SOURCE IS OUT OF DATE
~~~
/Users/?????/.cargo/registry/src/github.com-1ecc6299db9ec823/gl_generator-0.0.26/registry.rs:30:5: 30:40 error: module `events` is private
/Users/?????/.cargo/registry/src/github.com-1ecc6299db9ec823/gl_generator-0.0.26/registry.rs:30 use self::xml::reader::events::XmlEvent;
                                                                                                    ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
/Users/?????/.cargo/registry/src/github.com-1ecc6299db9ec823/gl_generator-0.0.26/registry.rs:322:45: 322:51 error: no method named `events` found for type `std::cell::RefMut<'_, registry::xml::EventReader<R>>` in the current scope
/Users/?????/.cargo/registry/src/github.com-1ecc6299db9ec823/gl_generator-0.0.26/registry.rs:322         for event in self.port.borrow_mut().events() {
                                                                                                                                             ^~~~~~
/Users/?????/.cargo/registry/src/github.com-1ecc6299db9ec823/gl_generator-0.0.26/registry.rs:328:17: 328:37 error: no associated item named `Error` found for type `registry::xml::reader::XmlEvent` in the current scope
/Users/?????/.cargo/registry/src/github.com-1ecc6299db9ec823/gl_generator-0.0.26/registry.rs:328                 XmlEvent::Error(err) => panic!("XML error: {:?}", err),
                                                                                                                 ^~~~~~~~~~~~~~~~~~~~
error: aborting due to 2 previous errors
Build failed, waiting for other jobs to finish...
error: Could not compile `gl_generator`.
~~~

-------------------------
### 2016.09.13 c4augustus

__11:00: setup Oculus mobile SDK on OS X__
  * downloaded Oculus mobile SDK 1.0.3 into `/u/soft/cost/oculus/`
  * copied and expanded into `??????/dist/ovr_sdk_mobile_1.0.3`

-------------------------
### 2016.09.17 c4augustus

__11:00: installed Oculus mobile SDK examples to c4a Note 5__
  * plugged c4a Note 5 via USB into MacBook Pro
  * cd `??????/dist/ovr_sdk_mobile_1.0.3`
  * `./install_to_phone.py`
~~~
Executing: adb install -r ./CinemaSDK.apk
* daemon not running. starting it now on port 5037 *
* daemon started successfully *
	pkg: /data/local/tmp/CinemaSDK.apk
Success
Executing: adb install -r ./Oculus360PhotosSDK.apk
	pkg: /data/local/tmp/Oculus360PhotosSDK.apk
Success
Executing: adb install -r ./Oculus360VideosSDK.apk
	pkg: /data/local/tmp/Oculus360VideosSDK.apk
Success
Executing: adb install -r ./VrCubeWorld_Framework.apk
	pkg: /data/local/tmp/VrCubeWorld_Framework.apk
Success
Executing: adb install -r ./VrCubeWorld_NativeActivity.apk
	pkg: /data/local/tmp/VrCubeWorld_NativeActivity.apk
Success
Executing: adb install -r ./VrCubeWorld_SurfaceView.apk
	pkg: /data/local/tmp/VrCubeWorld_SurfaceView.apk
Success
Executing: adb install -r ./VrScene.apk
	pkg: /data/local/tmp/VrScene.apk
Success
Executing: adb push sdcard_SDK /sdcard/
~~~

-------------------------
### 2016.10.04 c4augustus

__17:00: created cargo/rust project for the library rustvr-core__
  * `cd ~/v/dev/copyleft/rustvr/repo`
  * `cargo new rustvr-core`

__17:05: created cargo/rust project for the library rustvr-plug-gr-gfx__
  * `cd ~/v/dev/copyleft/rustvr/repo`
  * `cargo new rustvr-plug-gr-gfx`

__17:10: created cargo/rust project for the library rustvr-plug-hi-ovr-mobile__
  * `cd ~/v/dev/copyleft/rustvr/repo`
  * `cargo new rustvr-plug-hi-ovr-mobile`

-------------------------
### 2017.04.14 c4augustus

__22:15: created github repo rustvr-about__
  * firefox: `https://github/RustVR`
  * [New Repository]
  * Repository name: `rustvr-about`
  * Description: `About Rust VR`
  * `X` Public (default)
  * `X` Initialize this repository with a README
  * [Add a license]: [Mozilla Public License 2.0]
  * [Create repository]

__22:30: made local clone of github repo rustvr-about__
  * `cd rustvr/repo`
  * `git clone https://github.com/RustVR/rustvr-about.git`

__15:20: created github repo rustvr-core__
  * firefox: `https://github/organizations/RustVR`
  * [New Repository]
  * Repository name: `rustvr-core`
  * Description: `Rust VR core framework`
  * `X` Public (default)
  * ` ` Initialize this repository with a README

__15:30: pushed local repo rustvr-core to github__
  * `cd rustvr/repo/rustvr-core`
  * `git remote add origin https://github.com/RustVR/rustvr-core.git`
  * `git push -u origin master`

-------------------------
### 2017.04.30 c4augustus

__15:20: created github repo rustvr-gl-gfx__
  * firefox: `https://github/organizations/RustVR`
  * [New Repository]
  * Repository name: `rustvr-gl-gfx`
  * Description: `RustVR plugin for its graphics language implemented using gfx`
  * `X` Public (default)
  * ` ` Initialize this repository with a README

__15:30: pushed local repo rustvr-gl-gfx to github__
  * `cd rustvr/repo/rustvr-gl-gfx`
  * `git remote add origin https://github.com/RustVR/rustvr-gl-gfx.git`
  * `git push -u origin master`

-------------------------
### 2017.05.16 c4augustus

__15:20: created github repo rustvr-hi-ovr-mobile__
  * firefox: `https://github/organizations/RustVR`
  * [New Repository]
  * Repository name: `rustvr-hi-ovr-mobile`
  * Description: `RustVR plugin for its human interface using the Oculus Mobile SDK`
  * `X` Public (default)
  * ` ` Initialize this repository with a README

__15:30: pushed local repo rustvr-hi-ovr-mobile to github__
  * `cd rustvr/repo/rustvr-hi-ovr-mobile`
  * `git remote add origin https://github.com/rustvr/rustvr-hi-ovr-mobile.git`
  * `git push -u origin master`

-------------------------
### 2018.01.16 c4augustus

__11:38: upgraded local rust installation from 1.20.0 to 1.23.0__
  * `cd ~/u/run/rust`
  * `./curl-rustup`

-------------------------
### 2018.04.08 c4augustus

__18:00: updated gfx to v0.17__
(gfx was previously moved from xrcosa, see xrcosa-diary.md regarding its cloning)
  * `cd ~/v/dev/copyleft/rustvr/repo/gfx`
  * `git checkout master`
  * `git pull -r`
  * `git checkout v0.17`
  * `cargo update`

__21:00: created local registry for offline and reduced network retrieval__
  * `cargo install cargo-local-registry`
~~~
    Updating registry `https://github.com/rust-lang/crates.io-index`
 Downloading cargo-local-registry v0.1.5
  Installing cargo-local-registry v0.1.5
 Downloading flate2 v0.2.20
 Downloading tar v0.4.14
 Downloading cargo v0.18.0
 Downloading env_logger v0.4.3
 Downloading miniz-sys v0.1.10
 Downloading libc v0.2.40
 Downloading cc v1.0.9
 Downloading filetime v0.1.15
 Downloading cfg-if v0.1.2
 Downloading libgit2-sys v0.6.19
 Downloading url v1.7.0
 Downloading serde_derive v0.9.15
 Downloading curl v0.4.11
 Downloading num_cpus v1.8.0
 Downloading chrono v0.2.25
 Downloading serde v0.9.15
 Downloading serde_ignored v0.0.2
 Downloading crossbeam v0.2.12
 Downloading tempdir v0.3.7
 Downloading toml v0.3.2
 Downloading semver v0.6.0
 Downloading git2 v0.6.11
 Downloading serde_json v0.9.10
 Downloading git2-curl v0.7.0
 Downloading log v0.3.9
 Downloading docopt v0.7.0
 Downloading fs2 v0.4.3
 Downloading term v0.4.6
 Downloading shell-escape v0.1.4
 Downloading crates-io v0.7.0
 Downloading libz-sys v1.0.18
 Downloading libssh2-sys v0.2.6
 Downloading curl-sys v0.4.1
 Downloading cmake v0.1.30
 Downloading matches v0.1.6
 Downloading idna v0.1.4
 Downloading percent-encoding v1.0.1
 Downloading unicode-bidi v0.3.4
 Downloading unicode-normalization v0.1.5
 Downloading regex v0.2.10
 Downloading memchr v2.0.1
 Downloading thread_local v0.3.5
 Downloading aho-corasick v0.6.4
 Downloading regex-syntax v0.5.3
 Downloading unreachable v1.0.0
 Downloading lazy_static v1.0.0
 Downloading ucd-util v0.1.1
 Downloading log v0.4.1
 Downloading serde_codegen_internals v0.14.2
 Downloading socket2 v0.3.4
 Downloading num v0.1.42
 Downloading time v0.1.39
 Downloading num-traits v0.2.2
 Downloading num-integer v0.1.36
 Downloading num-iter v0.1.35
 Downloading rand v0.4.2
 Downloading remove_dir_all v0.5.0
 Downloading semver-parser v0.7.0
 Downloading bitflags v0.9.1
 Downloading dtoa v0.4.2
 Downloading itoa v0.3.4
 Downloading num-traits v0.1.43
 Downloading lazy_static v0.2.11
 Downloading strsim v0.6.0
 Downloading xattr v0.1.11
 Downloading openssl v0.9.24
 Downloading openssl-sys v0.9.28
 Downloading foreign-types v0.3.2
 Downloading foreign-types-shared v0.1.1
   Compiling rustc-serialize v0.3.24
   Compiling lazy_static v1.0.0
   Compiling dtoa v0.4.2
   Compiling matches v0.1.6
   Compiling bitflags v0.9.1
   Compiling strsim v0.6.0
   Compiling void v1.0.2
   Compiling remove_dir_all v0.5.0
   Compiling num-traits v0.2.2
   Compiling quote v0.3.15
   Compiling cfg-if v0.1.2
   Compiling glob v0.2.11
   Compiling percent-encoding v1.0.1
   Compiling unicode-normalization v0.1.5
   Compiling semver-parser v0.7.0
   Compiling itoa v0.3.4
   Compiling shell-escape v0.1.4
   Compiling crossbeam v0.2.12
   Compiling unicode-xid v0.0.4
   Compiling cc v1.0.9
   Compiling foreign-types-shared v0.1.1
   Compiling regex v0.2.10
   Compiling term v0.4.6
   Compiling pkg-config v0.3.9
   Compiling utf8-ranges v1.0.0
   Compiling openssl v0.9.24
   Compiling lazy_static v0.2.11
   Compiling libc v0.2.40
   Compiling serde v0.9.15
   Compiling ucd-util v0.1.1
   Compiling unreachable v1.0.0
   Compiling unicode-bidi v0.3.4
   Compiling log v0.4.1
   Compiling synom v0.11.3
   Compiling num-integer v0.1.36
   Compiling num-traits v0.1.43
   Compiling foreign-types v0.3.2
   Compiling semver v0.6.0
   Compiling thread_local v0.3.5
   Compiling regex-syntax v0.5.3
   Compiling fs2 v0.4.3
   Compiling rand v0.4.2
   Compiling filetime v0.1.15
   Compiling socket2 v0.3.4
   Compiling time v0.1.39
   Compiling xattr v0.1.11
   Compiling memchr v2.0.1
   Compiling num_cpus v1.8.0
   Compiling log v0.3.9
   Compiling num-iter v0.1.35
   Compiling syn v0.11.11
   Compiling idna v0.1.4
   Compiling miniz-sys v0.1.10
   Compiling libz-sys v1.0.18
   Compiling curl-sys v0.4.1
   Compiling openssl-sys v0.9.28
   Compiling cmake v0.1.30
   Compiling aho-corasick v0.6.4
   Compiling tar v0.4.14
   Compiling num v0.1.42
   Compiling tempdir v0.3.7
   Compiling url v1.7.0
   Compiling toml v0.3.2
   Compiling serde_json v0.9.10
   Compiling serde_ignored v0.0.2
   Compiling chrono v0.2.25
   Compiling libgit2-sys v0.6.19
   Compiling libssh2-sys v0.2.6
   Compiling serde_codegen_internals v0.14.2
   Compiling flate2 v0.2.20
   Compiling curl v0.4.11
   Compiling serde_derive v0.9.15
   Compiling docopt v0.7.0
   Compiling env_logger v0.4.3
   Compiling crates-io v0.7.0
   Compiling git2 v0.6.11
   Compiling git2-curl v0.7.0
   Compiling cargo v0.18.0
   Compiling cargo-local-registry v0.1.5
    Finished release [optimized] target(s) in 127.47 secs
  Installing /Users/?????/.cargo/bin/cargo-local-registry
~~~
  * `mkdir -p ~/u/run/rust/cargo/registry`
  * `cargo local-registry --sync Cargo.lock ~/u/run/rust/cargo/registry`
~~~
   Updating registry `https://github.com/rust-lang/crates.io-index`
 Downloading fuchsia-zircon v0.3.3
 Downloading redox_termios v0.1.1
 Downloading mint v0.5.0
 Downloading quick-error v1.2.1
 Downloading num-rational v0.1.42
 Downloading crossbeam-deque v0.2.0
 Downloading token_store v0.1.2
 Downloading winapi v0.3.4
 Downloading gleam v0.4.31
 Downloading core-graphics v0.13.0
 Downloading memmap v0.6.2
 Downloading approx v0.1.1
 Downloading cocoa v0.14.0
 Downloading core-foundation v0.3.0
 Downloading derivative v1.0.0
 Downloading byteorder v1.2.2
 Downloading libloading v0.5.0
 Downloading winapi-x86_64-pc-windows-gnu v0.4.0
 Downloading scoped_threadpool v0.1.9
 Downloading fuchsia-zircon-sys v0.3.3
 Downloading core-foundation-sys v0.5.1
 Downloading scopeguard v0.3.3
 Downloading glutin v0.13.1
 Downloading dlib v0.4.1
 Downloading android_glue v0.2.3
 Downloading sdl2 v0.31.0
 Downloading termion v1.5.1
 Downloading core-foundation v0.5.1
 Downloading vk v0.0.1
 Downloading core-foundation-sys v0.3.1
 Downloading proc-macro2 v0.3.6
 Downloading itertools v0.5.10
 Downloading termcolor v0.3.6
 Downloading rand v0.3.22
 Downloading draw_state v0.8.0
 Downloading crossbeam-utils v0.2.2
 Downloading deflate v0.7.18
 Downloading lalrpop-util v0.11.0
 Downloading winit v0.11.3
 Downloading unicode-xid v0.1.0
 Downloading sdl2-sys v0.31.0
 Downloading xml-rs v0.7.0
 Downloading metal-rs v0.4.3
 Downloading wayland-protocols v0.12.5
 Downloading num-complex v0.1.43
 Downloading wayland-window v0.13.3
 Downloading cgmath v0.14.1
 Downloading bitflags v1.0.1
 Downloading wayland-sys v0.12.5
 Downloading jpeg-decoder v0.1.14
 Downloading core-graphics v0.8.2
 Downloading gif v0.9.2
 Downloading tempfile v3.0.0
 Downloading serde v1.0.37
 Downloading khronos_api v2.2.0
 Downloading cgl v0.2.1
 Downloading env_logger v0.5.6
 Downloading wayland-client v0.12.5
 Downloading inflate v0.3.4
 Downloading quote v0.5.1
 Downloading nodrop v0.1.12
 Downloading serde_derive v1.0.37
 Downloading syn v0.13.1
 Downloading gcc v0.3.54
 Downloading glfw v0.20.0
 Downloading gfx_gl v0.5.0
 Downloading crossbeam-epoch v0.3.1
 Downloading x11-dl v2.17.5
 Downloading cgmath v0.16.1
 Downloading gl_generator v0.9.0
 Downloading arrayvec v0.4.7
 Downloading syn v0.10.8
 Downloading redox_syscall v0.1.37
 Downloading image v0.18.0
 Downloading either v1.5.0
 Downloading wayland-kbd v0.13.1
 Downloading num-bigint v0.1.43
 Downloading adler32 v1.0.2
 Downloading winapi-i686-pc-windows-gnu v0.4.0
 Downloading atty v0.2.8
 Downloading rayon v1.0.1
 Downloading genmesh v0.5.0
 Downloading humantime v1.1.1
 Downloading memoffset v0.2.1
 Downloading png v0.11.0
 Downloading bit-vec v0.4.4
 Downloading mint v0.2.0
 Downloading wayland-scanner v0.12.5
 Downloading shared_library v0.1.8
 Downloading serde_derive_internals v0.23.0
 Downloading cocoa v0.9.2
 Downloading wincolor v0.1.6
 Downloading rayon-core v1.4.0
 Downloading bit-set v0.4.0
 Downloading glfw-sys v3.2.2
add this to your .cargo/config somewhere:

    [source.crates-io]
    registry = 'https://github.com/rust-lang/crates.io-index'
    replace-with = 'local-registry'

    [source.local-registry]
    local-registry = '/Users/?????/u/run/rust/cargo/registry'
~~~
  * vim ~/.cargo/config
~~~
[source.crates-io]
registry = 'https://github.com/rust-lang/crates.io-index'
replace-with = 'local-registry'

[source.local-registry]
local-registry = '/Users/?????/u/run/rust/cargo/registry'
~~~
  * [https://github.com/alexcrichton/cargo-local-registry/issues/5]
  ..* NOTE that we must disable `replace-with` whenever we need to `cargo update` (https://github.com/alexcrichton/cargo-local-registry/issues/5)
  * `cargo build`
  * `cargo run --example cube`

-------------------------
### 2018.04.09 c4augustus

__15:00: updated rustvr-gl-gfx to new gfx v0.17__
  * `cd ~/v/dev/copyleft/rustvr/repo/rustvr-gl-gfx`
  * vim ~/.cargo/config
~~~
#replace-with = 'local-registry'
~~~
  * `cargo update`
  * `cargo local-registry --sync Cargo.lock ~/u/run/rust/cargo/registry`
~~~
 Downloading cocoa v0.13.0
 Downloading gfx v0.17.1
 Downloading glutin v0.12.2
 Downloading core-foundation-sys v0.4.6
 Downloading gfx_app v0.6.0
 Downloading gfx_device_dx11 v0.7.0
 Downloading core-foundation v0.4.6
 Downloading winit v0.10.0
 Downloading gfx_device_gl v0.15.2
 Downloading core-graphics v0.12.4
 Downloading gfx_core v0.8.2
 Downloading gfx_macros v0.2.1
 Downloading gfx_window_glutin v0.20.0
 Downloading gfx_window_dxgi v0.11.0
 Downloading gl_generator v0.8.0
add this to your .cargo/config somewhere:

    [source.crates-io]
    registry = 'https://github.com/rust-lang/crates.io-index'
    replace-with = 'local-registry'

    [source.local-registry]
    local-registry = '/Users/?????/u/run/rust/cargo/registry'
~~~
  * vim ~/.cargo/config
~~~
replace-with = 'local-registry'
~~~

__16:30: update origin github rustvr/gfx to upstream gfx-rs/gfx__
  * `cd ~/v/dev/copyleft/rustvr/repo/gfx`
  * `git remote set-url origin https://github.com/rustvr/gfx.git`
  * `git remote add upstream https://github.com/gfx-rs/gfx.git`
  * `git remote -v`
~~~
origin	https://github.com/rustvr/gfx.git (fetch)
origin	https://github.com/rustvr/gfx.git (push)
upstream	https://github.com/gfx-rs/gfx.git (fetch)
upstream	https://github.com/gfx-rs/gfx.git (push)
~~~
  * `git fetch`
~~~
From https://github.com/rustvr/gfx
 + 2e482755b...12de9eb1b auto       -> origin/auto  (forced update)
 + 7a3746885...3f7905173 master     -> origin/master  (forced update)
~~~
  * `git remote prune origin`
~~~
Pruning origin
URL: https://github.com/rustvr/gfx.git
 * [pruned] origin/kvark-travis
 * [pruned] origin/pre-ll
 * [pruned] origin/staging
 * [pruned] origin/trying
 * [pruned] origin/v0.16
 * [pruned] origin/v0.17
~~~
  * `git push -u origin head`
~~~
Counting objects: 1784, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (735/735), done.
Writing objects: 100% (1784/1784), 444.26 KiB | 24.68 MiB/s, done.
Total 1784 (delta 1154), reused 1636 (delta 1029)
remote: Resolving deltas: 100% (1154/1154), completed with 135 local objects.
To https://github.com/rustvr/gfx.git
 * [new branch]          head -> v0.17
Branch v0.17 set up to track remote branch v0.17 from origin.
~~~
  * `git checkout master`
~~~
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 1023 commits.
  (use "git push" to publish your local commits)
~~~
  * `git push`
~~~
Counting objects: 11434, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3614/3614), done.
Writing objects: 100% (11434/11434), 3.30 MiB | 320.00 KiB/s, done.
Total 11434 (delta 7672), reused 11214 (delta 7520)
remote: Resolving deltas: 100% (7672/7672), completed with 89 local objects.
To https://github.com/rustvr/gfx.git
   3f7905173..7a3746885  master -> master
~~~
  * `git branch --all`
~~~
* master
  v0.12
  v0.17
  remotes/origin/HEAD -> origin/master
  remotes/origin/auto
  remotes/origin/gh-pages
  remotes/origin/master
  remotes/origin/v0.10
  remotes/origin/v0.11
  remotes/origin/v0.12
  remotes/origin/v0.12-dxgi
  remotes/origin/v0.13
  remotes/origin/v0.14
  remotes/origin/v0.14-vk
  remotes/origin/v0.15
  remotes/origin/v0.17
  remotes/origin/v0.7
  remotes/origin/v0.8
  remotes/origin/v0.9
~~~
  * `git checkout v0.17`

-------------------------
### 2018.04.12 c4augustus

__15:20: created github repo rustvr-hi-macos__
  * firefox: `https://github/organizations/rustvr`
  * [New Repository]
  * Repository name: `rustvr-hi-macos`
  * Description: `Rust VR plugin for its human interface using macOS`
  * `X` Public (default)
  * ` ` Initialize this repository with a README

__15:30: pushed local repo rustvr-hi-macos to github__
  * `cd rustvr/repo/rustvr-hi-macos`
  * `git remote add origin https://github.com/rustvr/rustvr-hi-macos.git`
  * `git push -u origin master`

-------------------------
### 2018.04.13 c4augustus

__18:15: forked tomaka/android-rs-glue.git__
  * firefox: `https://github/tomaka/android-rs-glue`
  * `[fork]` `[@rustvr]`

__18:20: cloned rustvr/android-rs-glue.git__
  * `cd rustvr/repo
  * `git clone https://github.com/rustvr/android-rs-glue.git`

__19:00: installed cargo apk subcommand__
  * `cd android-rs-glue/cargo-apk
  * vim ~/.cargo/config
~~~
#replace-with = 'local-registry'
~~~
  * `cargo install`
  * `cargo local-registry --sync Cargo.lock ~/u/run/rust/cargo/registry`
~~~
replace-with = 'local-registry'
~~~

__20:00: installed cargo apk subcommand__
  * `cd android-rs-glue/cargo-apk
  * `cargo install`
~~~
  Installing cargo-apk v0.4.1 (file:///Users/admin/v/dev/copyleft/rustvr/repo/android-rs-glue/cargo-apk)
   Compiling void v1.0.2
   Compiling scoped-tls v0.1.0
   Compiling itoa v0.3.1
   Compiling num-traits v0.1.40
   Compiling gcc v0.3.45
   Compiling cfg-if v0.1.0
   Compiling openssl v0.9.11
   Compiling shell-escape v0.1.3
   Compiling crossbeam v0.2.10
   Compiling quote v0.3.15
   Compiling bitflags v0.7.0
   Compiling rustc-demangle v0.1.4
   Compiling log v0.3.7
   Compiling foreign-types v0.2.0
   Compiling term v0.4.5
   Compiling strsim v0.6.0
   Compiling matches v0.1.4
   Compiling glob v0.2.11
   Compiling rustc-serialize v0.3.24
   Compiling libc v0.2.21
   Compiling unicode-xid v0.0.4
   Compiling utf8-ranges v1.0.0
   Compiling serde v1.0.10
   Compiling semver-parser v0.7.0
   Compiling pkg-config v0.3.9
   Compiling unicode-normalization v0.1.4
   Compiling regex-syntax v0.4.1
   Compiling dtoa v0.4.1
   Compiling lazy_static v0.2.8
   Compiling bitflags v0.8.2
   Compiling unreachable v1.0.0
   Compiling unicode-bidi v0.2.5
   Compiling synom v0.11.3
   Compiling jobserver v0.1.6
   Compiling backtrace v0.3.2
   Compiling num_cpus v1.3.0
   Compiling fs2 v0.4.2
   Compiling rand v0.3.15
   Compiling memchr v1.0.1
   Compiling filetime v0.1.10
   Compiling miniz-sys v0.1.9
   Compiling cmake v0.1.22
   Compiling curl-sys v0.3.10
   Compiling libz-sys v1.0.13
   Compiling openssl-sys v0.9.11
   Compiling thread_local v0.3.4
   Compiling syn v0.11.11
   Compiling error-chain v0.10.0
   Compiling aho-corasick v0.6.3
   Compiling tar v0.4.11
   Compiling idna v0.1.1
   Compiling tempdir v0.3.5
   Compiling libgit2-sys v0.6.7
   Compiling libssh2-sys v0.2.5
   Compiling toml v0.1.30
   Compiling serde_json v1.0.2
   Compiling semver v0.7.0
   Compiling toml v0.4.2
   Compiling serde_ignored v0.0.3
   Compiling regex v0.2.2
   Compiling url v1.4.0
   Compiling serde_derive_internals v0.15.1
   Compiling flate2 v0.2.19
   Compiling curl v0.4.6
   Compiling docopt v0.7.0
   Compiling env_logger v0.4.3
   Compiling serde_derive v1.0.10
   Compiling git2 v0.6.4
   Compiling git2-curl v0.7.0
   Compiling crates-io v0.9.0
   Compiling cargo v0.20.0
   Compiling cargo-apk v0.4.1 (file:///Users/admin/v/dev/copyleft/rustvr/repo/android-rs-glue/cargo-apk)
    Finished release [optimized] target(s) in 120.40 secs
  Installing /Users/admin/.cargo/bin/cargo-apk
~~~

__18:45: install rustup__
  * `curl https://sh.rustup.rs -sSf | sh`
~~~
info: downloading installer
warning: it looks like you have an existing installation of Rust
warning: rustup cannot be installed alongside Rust. Please uninstall first
warning: run `/usr/local/lib/rustlib/uninstall.sh` as root to uninstall Rust
error: cannot install while Rust is installed
~~~
  * `sudo /usr/local/lib/rustlib/uninstall.sh`
  * `curl https://sh.rustup.rs -sSf | sh`
~~~
info: downloading installer
warning: it looks like you have existing rustup.sh metadata
warning: rustup cannot be installed while rustup.sh metadata exists
warning: delete `/Users/?????/.rustup` to remove rustup.sh
warning: or, if you already rustup installed, you can run
warning: `rustup self update` and `rustup toolchain list` to upgrade
warning: your directory structure
error: cannot install while rustup.sh is installed
~~~
  * `sudo rm -fR ~/.rustup`
  * `curl https://sh.rustup.rs -sSf | sh`
~~~
info: downloading installer

Welcome to Rust!

This will download and install the official compiler for the Rust programming
language, and its package manager, Cargo.

It will add the cargo, rustc, rustup and other commands to Cargo's bin
directory, located at:

  /Users/?????/.cargo/bin

This path will then be added to your PATH environment variable by modifying the
profile files located at:

  /Users/?????/.profile
  /Users/?????/.bash_profile

You can uninstall at any time with rustup self uninstall and these changes will
be reverted.

Current installation options:

   default host triple: x86_64-apple-darwin
     default toolchain: stable
  modify PATH variable: yes

1) Proceed with installation (default)
2) Customize installation
3) Cancel installation
~~~
  * `1`
~~~
warning: tool `rustfmt` is already installed, remove it from `/Users/?????/.cargo/bin`, then run `rustup update` to have rustup manage this tool.
warning: tool `cargo-fmt` is already installed, remove it from `/Users/?????/.cargo/bin`, then run `rustup update` to have rustup manage this tool.
info: syncing channel updates for 'stable-x86_64-apple-darwin'
info: latest update on 2018-03-29, rust version 1.25.0 (84203cac6 2018-03-25)
info: downloading component 'rustc'
 46.5 MiB /  46.5 MiB (100 %)   1.9 MiB/s ETA:   0 s
info: downloading component 'rust-std'
 38.7 MiB /  38.7 MiB (100 %)   2.5 MiB/s ETA:   0 s
info: downloading component 'cargo'
  2.7 MiB /   2.7 MiB (100 %)   1.1 MiB/s ETA:   0 s
info: downloading component 'rust-docs'
  5.7 MiB /   5.7 MiB (100 %)   2.5 MiB/s ETA:   0 s
info: installing component 'rustc'
info: installing component 'rust-std'
info: installing component 'cargo'
info: installing component 'rust-docs'
info: default toolchain set to 'stable'

  stable installed - rustc 1.25.0 (84203cac6 2018-03-25)


Rust is installed now. Great!

To get started you need Cargo's bin directory ($HOME/.cargo/bin) in your PATH
environment variable. Next time you log in this will be done automatically.

To configure your current shell run source $HOME/.cargo/env
~~~

__19:00: install rust android target__
  * `rustup target add arm-linux-androideabi`
~~~
info: downloading component 'rust-std' for 'arm-linux-androideabi'
 13.8 MiB /  13.8 MiB (100 %)   5.9 MiB/s ETA:   0 s
info: installing component 'rust-std' for 'arm-linux-androideabi'
~~~

-----------------
### (end of file)
