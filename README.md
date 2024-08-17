# Wyoming dependancies for ARMv6 (Raspberry Pi 0)


### Build:
#### OnnxRuntime (Wyoming Satellite
* Use a docker container for the target system so you can build natively
	* docker build --platform linux/arm/v6 -t onnxbuild -f Dockerfile .
	* docker run --platform linux/arm/v6 --rm -v /home/james/docker/ccache:/ccache -v /home/james/docker/runtime:/runtime -it onnxbuild bash
		* CCache is critical for your own sanity
	* Build CMake from source (3.30.2 used), as the generally available ones aren't working with onnx at the time of writing
	* Install numpy (< version 2.0 for the sepcified onnx version)
	* ./build.sh ${BUILDARGS} --update --build --build_shared_lib --enable_pybind --build_wheel --parallel --compile_no_warning_as_error
		* Note, after v1.16.3, onnx runetime wasn't building for the archtecture.

#### TF Lite (Wyoming OpenWakeWord)
* Use a docker container for the target system (same way as before)
	* ./tensorflow/lite/tools/pip_package/build_pip_package_with_cmake.sh native
	* You'll need to pre-load libatomic on execution (or you can statically link in the build system)
	

#### I'm sure I'm missing some small things, such as needing to grab/copy some files, but they'll be few.  
#### Wyoming OpenWakeWord is "working" for me, but the performance is making it completely unusable.  See my [open issue](https://github.com/rhasspy/wyoming-openwakeword/issues/30)


