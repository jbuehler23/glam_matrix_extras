# bevy-main

This branch follows Bevy's git `main` branch for the Jackdaw editor, which
builds on Bevy main. It is upstream `main` with the Bevy crates (and the
avian dependency forks) taken from git instead of crates.io, plus the fixes
needed to compile against Bevy main.

Bevy comes from `{ git = "https://github.com/bevyengine/bevy", branch = "main" }`,
spelled the same way Jackdaw spells it, so both resolve to one copy of Bevy.
The commit is chosen by the consumer's `Cargo.lock`, not here.

## Moving to a newer Bevy commit

1. Rebase this branch on upstream `main`.
2. In Jackdaw, update its Bevy commit (`cargo update -p bevy`), then copy its
   `Cargo.lock` here and run `cargo check --all-features` (or the crate's
   usual feature set) to find what broke.
3. Fix the compile errors, commit, and push `bevy-main`.
4. In Jackdaw's `integrations/physics`, run `cargo update -p avian3d -p avian2d`
   so its lockfile picks up the new commit.

The dependency forks (`bevy_heavy`, `bevy_transform_interpolation`,
`glam_matrix_extras`) carry the same branch and are moved first, in that
order: `glam_matrix_extras`, then `bevy_heavy` and
`bevy_transform_interpolation`, then `avian`.
