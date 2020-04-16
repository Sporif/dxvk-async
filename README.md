## dxvk-async
An attempt to improve the dxvk async patch at https://github.com/jomihaka/dxvk-poe-hack

 - The original patch doesn't write async pipelines to the state cache (since it was made before dxvk introduced the state cache), this version fixes that.

 - This version also has a lot less stutterring (nearly none at all in some games) by not blocking the main thread when compiling async pipelines. The downside is that the shader cache is around 5-10% larger (I guess due to duplicate shaders?). But the state cache is roughly the same size as a non-async produced state cache.

### Instructions

* Patch dxvk with dxvk-async.patch
* Set the environment variable `DXVK_ASYNC=1`
* To compare with stock dxvk rename or delete your state and shader caches
