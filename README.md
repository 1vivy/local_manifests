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
| `local_manifests/1vivy-feature-gaps.xml` | Overlays the device trees onto `staging/feature-gaps/*` topic branches. Apply ON TOP of the base file to build a tree with the in-flight feature-gap work. |

`1vivy-infiniti-base.xml` pins the profile targets at their `series.json` `base_sha`, so
applying the `patches` profile is MANDATORY with it. Do not combine it with
`infiniti-camera-port/local_manifest`, which pins the same repos at promoted heads — that
would double-apply.

The feature-gap overlay is topic branches under active development; expect it to move.
