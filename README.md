## dxvk-async
An attempt to improve the dxvk async patch at https://github.com/jomihaka/dxvk-poe-hack

### Improvements

 - Compatible with dxvk v1.4.5 - v1.7.1

 - Async pipelines are written to the state cache. The original patch doesn't since it was made before dxvk introduced the state cache. Previously you would end up with near empty state caches when using dxvk-async, now you can have the best of both worlds.

 - A lot less stutterring (nearly none at all in some games) by not blocking the main thread when compiling async pipelines. The downside is that the shader cache is around 5-10% larger (I guess due to duplicate shaders?). But the state cache is roughly the same size as a non-async produced state cache.

 - A new option `dxvk.numAsyncThreads` to specify the number of async pipeline compiler threads. Previously half the cpu thread count was used by default, now it's the same logic as the state cache.

### Instructions

* Patch dxvk with dxvk-async.patch
* Set the environment variable `DXVK_ASYNC=1` or use `dxvk.enableAsync = true` in dxvk.conf
* To compare with stock dxvk, rename or delete your state and shader caches
* Use `DXVK_HUD=pipelines` to see the pipeline count go up (hopefully) without stutter
