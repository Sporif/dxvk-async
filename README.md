## dxvk-async
An attempt to improve the dxvk async patch at https://github.com/jomihaka/dxvk-poe-hack

### Improvements

 - Write async pipelines to the state cache (the original patch didn't since it was made before dxvk introduced the state cache).

 - A lot less stutterring (nearly none at all in some games) by not blocking the main thread when compiling async pipelines. The downside is that the shader cache is around 5-10% larger (I guess due to duplicate shaders?). But the state cache is roughly the same size as a non-async produced state cache.

 - You can now use dxvk.numCompilerThreads to also specify the number of async pipeline compiler threads (previously half the cpu thread count was used, now it's the same logic as the state cache). You may want to try a low nummber to lower cpu usage when recompiling from a state cache after the shader cache is invalidated (due to a driver update for example).

### Instructions

* Patch dxvk with dxvk-async.patch
* Set the environment variable `DXVK_ASYNC=1`
* To compare with stock dxvk, rename or delete your state and shader caches
* You can use `DXVK_HUD=pipelines` to see pipelines being compiled without stutter
