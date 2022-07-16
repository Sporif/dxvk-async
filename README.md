## dxvk-async
An attempt to improve the dxvk async patch at https://github.com/jomihaka/dxvk-poe-hack

### Improvements

 - Compatible with dxvk v1.4.3 - v1.10.2

 - Async pipelines are written to the state cache. The original patch doesn't since it was made before dxvk introduced the state cache. Previously you would end up with near empty state caches when using dxvk-async, now you can have the best of both worlds.

 - A lot less stutterring (nearly none at all in some games) by not blocking the main thread when compiling async pipelines. The downside is that the shader cache is around 5-10% larger (I guess due to duplicate shaders?). But the state cache is roughly the same size as a non-async produced state cache.

 - A new option `dxvk.numAsyncThreads` to specify the number of async pipeline compiler threads. Previously half the cpu thread count was used by default, now it's the same logic as the state cache.

### Instructions

* Patch dxvk with dxvk-async.patch
* Set the environment variable `DXVK_ASYNC=1` or use `dxvk.enableAsync = true` in dxvk.conf
* To compare with stock dxvk, rename or delete your state and shader caches
* Use `DXVK_HUD=pipelines` to see the pipeline count go up (hopefully) without stutter

### Compatibility Matrix

| Async Patch  | DXVK Version |
|--------------|--------------|
| [dxvk-async-af418dc.patch](https://github.com/Sporif/dxvk-async/blob/master/dxvk-async-af418dc.patch) | 1.10.2 | 
| [dxvk-async-80e125a.patch](https://github.com/Sporif/dxvk-async/blob/master/dxvk-async-80e125a.patch) | 1.10  - 1.10.1 | 
| [dxvk-async-67e2ee1.patch](https://github.com/Sporif/dxvk-async/blob/master/dxvk-async-67e2ee1.patch) | 1.9.3 - 1.9.4  | 
| [dxvk-async-f1aad6c.patch](https://github.com/Sporif/dxvk-async/blob/master/dxvk-async-f1aad6c.patch) | 1.4.3 - 1.9.1  | 

## Warnings

dxvk-async could theoretically trigger client-side anti cheats, and as such, may be risky to use inside of multiplayer games.
If you have been banned because of dxvk-async, please report about it at [this issue here](https://github.com/Sporif/dxvk-async/issues/42) with information about your system (like a neofetch), distribution/OS (BSD, GNU/Linux, etc.), how long it took the ban to take effect, and whether or not you were able to get unbanned. 

As of 2022-07-16 we are not aware of any bans that happened due to dxvk_async.
