# local_manifests

Personal ROM development for the OnePlus 15 (`infiniti`, SM8850) on crDroid 16.0.

Drop the files you want into `.repo/local_manifests/` after:

```
repo init -u https://github.com/crdroidandroid/android.git -b 16.0
repo sync
```

| File | Purpose |
|---|---|
| `local_manifests/1vivy-infiniti-base.xml` | The working base composition: device trees from the `1vivy` forks, camera-port vendor/proprietary lanes, and the crDroid upstream pins. |
| `local_manifests/1vivy-feature-gaps.xml` | Self-contained composition that pins the five projects carrying feature-gap work at `staging/feature-gaps/all`. Use it INSTEAD OF the base file, not alongside it. |

`1vivy-infiniti-base.xml` pins the profile targets at their `series.json` `base_sha`, so
applying the `patches` profile is MANDATORY with it. Do not combine it with
`infiniti-camera-port/local_manifest`, which pins the same repos at promoted heads — that
would double-apply.

`1vivy-feature-gaps.xml` is self-contained on purpose. repo loads
`.repo/local_manifests/*.xml` in sorted filename order, so `1vivy-feature-gaps.xml` is
parsed BEFORE `1vivy-infiniti-base.xml` and could not have overridden it as an overlay;
dropping both also declares `device/oneplus/infiniti` twice, which repo rejects as a
duplicate path. Drop exactly one of the two.

`vendor/oneplus/infiniti` is served from `infiniti-camera-port` rather than `1vivy`:
publishing that branch to `1vivy` requires 189 Git LFS objects (1.84 GiB at HEAD plus
history) against GitHub's 1 GiB free per-account quota, while `infiniti-camera-port`
already holds every one of them.

The feature-gap branches are under active development; expect them to move.
