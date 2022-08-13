## dxvk-async
An attempt to improve the dxvk-async patch at https://github.com/jomihaka/dxvk-poe-hack

### Improvements

 - Compatible with dxvk v1.4.3 - v1.10.3

 - A lot less stuttering (nearly none at all in some games) by not blocking the main thread when compiling async pipelines.

 - [dxvk-async-e3a63d4.patch] and earlier: Async pipelines are written to the state cache. The original patch doesn't since it was made before dxvk introduced the state cache. Previously you would end up with near empty state caches when using dxvk-async, now you can have the best of both worlds.

 - [dxvk-async.patch] uses the existing worker thread system (controlled by `dxvk.numCompilerThreads`) to compile async pipelines.

 - [dxvk-async-ab1d629.patch] and earlier: A new option `dxvk.numAsyncThreads` to specify the number of async pipeline compiler threads. Previously half the cpu thread count was used by default, now it's the same logic as the state cache.

### Caveats

 - [dxvk-async-ab1d629.patch] and newer: Enabling dxvk-async will force disable the new dxvk option: `dxvk.enableGraphicsPipelineLibrary`. This is currently necessary for dxvk-async to work.

 - [dxvk-async-af418dc.patch] and earlier: The shader cache can be around 5-10% larger.

### Instructions

* Patch dxvk with dxvk-async.patch
* Set the environment variable `DXVK_ASYNC=1` or use `dxvk.enableAsync = true` in dxvk.conf
* To compare with stock dxvk, rename or delete your state and shader caches
* Use `DXVK_HUD=pipelines` to see the pipeline count go up (hopefully) without stutter

### Compatibility Matrix

| Async Patch | DXVK Versions | DXVK Commits |
|-|-|-|
| [dxvk-async.patch]         |                 | r4705.ab1d629 -               |
| [dxvk-async-ab1d629.patch] |                 | r4388.52038b2 - r4704.764de6f |
| N/A                        |                 | r4321.e3a63d4 - r4387.ca52c5a |
| [dxvk-async-e3a63d4.patch] |                 | r4275.af418dc - r4320.39a2b1c |
| [dxvk-async-af418dc.patch] | 1.10.2 - 1.10.3 | r4217.80e125a - r4274.a27448b |
| [dxvk-async-80e125a.patch] | 1.10   - 1.10.1 | r4072.67e2ee1 - r4216.4ff7687 |
| [dxvk-async-67e2ee1.patch] | 1.9.3  - 1.9.4  | r3942.f1aad6c - r4071.a4fe434 |
| [dxvk-async-f1aad6c.patch] | 1.4.3  - 1.9.2  | r2644.2c974cb - r3941.5b72520 |

[dxvk-async.patch]: https://github.com/Sporif/dxvk-async/blob/master/dxvk-async.patch
[dxvk-async-ab1d629.patch]: https://github.com/Sporif/dxvk-async/blob/master/dxvk-async-ab1d629.patch
[dxvk-async-e3a63d4.patch]: https://github.com/Sporif/dxvk-async/blob/master/dxvk-async-e3a63d4.patch
[dxvk-async-af418dc.patch]: https://github.com/Sporif/dxvk-async/blob/master/dxvk-async-af418dc.patch
[dxvk-async-80e125a.patch]: https://github.com/Sporif/dxvk-async/blob/master/dxvk-async-80e125a.patch
[dxvk-async-67e2ee1.patch]: https://github.com/Sporif/dxvk-async/blob/master/dxvk-async-67e2ee1.patch
[dxvk-async-f1aad6c.patch]: https://github.com/Sporif/dxvk-async/blob/master/dxvk-async-f1aad6c.patch

## Warnings

dxvk-async could theoretically trigger client-side anti cheats, and as such, may be risky to use inside of multiplayer games.
If you have been banned because of dxvk-async, please report about it at [this issue here](https://github.com/Sporif/dxvk-async/issues/42) with information about your system (like a neofetch), distribution/OS (BSD, GNU/Linux, etc.), how long it took the ban to take effect, and whether or not you were able to get unbanned. 

As of 2022-07-16 we are not aware of any bans that happened due to dxvk-async.
