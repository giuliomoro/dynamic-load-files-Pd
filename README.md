# Playing multiple samples in Pd

If you have a large number of samples, that will not all fit in arrays in memory, but still you want to be able to play them all with zero notice, then the trick is to"
- store just the beginning of the file in an array at startup (using `[soundfiler]`). This could be between 0.5 and 2 seconds, but the exact number of samples needs to be a multiple of Pd's blocksize.
- when the sample is played, start playing immediately from the array and send an `[open(` message to `[readsf~]`.
- when you finished reading the array, hopefully `[readsf~]` will have read enough data from disk into memory and will be ready to play, so send it `[1(` to start playback

This project is an implementation of the above.
