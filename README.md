# egui-video, a video playing library for [`egui`](https://github.com/emilk/egui)

[![crates.io](https://img.shields.io/crates/v/egui-video)](https://crates.io/crates/egui-video/0.5.2)
[![docs](https://docs.rs/egui-video/badge.svg)](https://docs.rs/egui-video/0.5.2/egui_video/)
[![license](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/n00kii/egui-video/blob/main/README.md)

![Demo](https://github.com/n00kii/egui-video/assets/57325298/c618ff0a-9ad2-4cf0-b14a-dda65dc54b23)

Plays videos in egui from file path or from bytes.

## Dependencies

- Requires ffmpeg 6. Follow the build instructions [here](https://github.com/zmwangx/rust-ffmpeg/wiki/Notes-on-building)
- Requires sdl2. By default, a feature is enabled to automatically compile it for you, but you are free to disable it and follow [these instructions](https://github.com/Rust-SDL2/rust-sdl2#requirements)

## Usage

```rust
/* called once (top level initialization) */

{ // if using audio...
    let audio_device = egui_video::init_audio_device_default()?;
    
    // don't let audio_device drop out of memory! (or else you lose audio)

    add_audio_device_to_state_somewhere(audio_device);
}
```

```rust
/* called once (creating a player) */

let mut player = Player::new(ctx, my_media_path)?;

{ // if using audio...
    player = player.with_audio(&mut my_state.audio_device)
}
```

```rust
/* called every frame (showing the player) */
player.ui(ui, [player.width as f32, player.height as f32]);
```

## Contributions

are welcome :)

### Current caveats

- Need to compile in `release` or `opt-level=3` otherwise limited playback performance
