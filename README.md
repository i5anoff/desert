# Desert

Desert consists of two parts.

The main library is simply called `Desert`. It is a CUDA accelerated library
for sandpainting: http://inconvergent.net/grains-of-sand/

The second part is called `Erosion`. A Redis-based client and worker that can
accept and draw `Desert` primitives and commands encoded as JSON objects. That
means that you can use the `Erosion` worker from any platform as long as you
can construct JSON and it to a Redis queue. Eg. if you want to program in a
different language, while still having a fast drawing engine that benefits from
CUDA.


## Install

Use the install script:

    ./install.sh

This will use `setuptools` to install python libraries `desert` and `erosion`.
As well as a shell util called `erosion`. It will be available as
`~/.local/bin/erosion` if you installed with the `--user` flag.


## Examples

There are some examples in `./examples`.

To use `Desert` via Python as a local library, see:

    main.py

To see how `Erosion` works, you can run this command (from `./examples`):

    ./erosion-send.py && ~/.local/bin/erosion worker --vv

This will first send some `Desert` primitives to the `Erosion` (Redis) queue.
Then it will run the `Erosion` worker, which draws those primitives. Finally it
will save the resulting image.

To see how the `Erosion` terminal util works:

    ~/.local/bin/erosion -h


## Dependencies

The code depends on the CUDA toolkit (8.0), Redis (if you are using `Erosion`),
and a few Python (3) packages. If you install using the install script, the
python packages will be installed automatically.


## On Use and Contributions

This code is a tool that I have written for my own use. I release it publicly
in case people find it useful. It is not however intended as a
collaboration/Open Source project. As such I am unlikely to accept PRs, reply
to issues, or take requests.


## Todo

Desert:

- [x] Box
- [x] Stroke
- [x] Circle
- [ ] Spline
- [ ] Circle: varying rad
- [ ] Box: varying size
- [x] Color
- [x] Json import/export of classes
- [ ] aggregate primitives


Erosion:

- [x] Basic example using Redis
- [x] Init
- [x] Send color
- [ ] Move pfloat to erosion (from .json())


## Notes

If cuda is not working try `sudo ldconfig`. and check $LD_LIBRARY_PATH

https://documen.tician.de/pycuda/tutorial.html#executing-a-kernel

http://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#kernels

