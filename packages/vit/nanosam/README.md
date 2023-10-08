# nanosam

> [`CONTAINERS`](#user-content-containers) [`IMAGES`](#user-content-images) [`RUN`](#user-content-run) [`BUILD`](#user-content-build)


* NanoSAM from https://github.com/NVIDIA-AI-IOT/nanosam/

### Run the basic usage example and copy the result to host

```
./run.sh $(./autotag nanosam) /bin/bash -c " \
  cd /opt/nanosam && \
  python3 examples/basic_usage.py \  
    --image_encoder=data/resnet18_image_encoder.engine \
    --mask_decoder=data/mobile_sam_mask_decoder.engine && \
  mv data/basic_usage_out.jpg /data/ \
  "
```

### Benchmark

```
 ./run.sh $(./autotag nanosam) /bin/bash -c " \
   cd /opt/nanosam && \
   python3 benchmark.py --run 3 -s /data/nanosam.csv && \
   mv data/benchmark_last_image.jpg /data/ \
   "
 ```
<details open>
<summary><b><a id="containers">CONTAINERS</a></b></summary>
<br>

| **`nanosam`** | |
| :-- | :-- |
| &nbsp;&nbsp;&nbsp;Builds | [![`nanosam_jp51`](https://img.shields.io/github/actions/workflow/status/dusty-nv/jetson-containers/nanosam_jp51.yml?label=nanosam:jp51)](https://github.com/dusty-nv/jetson-containers/actions/workflows/nanosam_jp51.yml) |
| &nbsp;&nbsp;&nbsp;Requires | `L4T >=34.1.0` |
| &nbsp;&nbsp;&nbsp;Dependencies | [`build-essential`](/packages/build-essential) [`python`](/packages/python) [`numpy`](/packages/numpy) [`cmake`](/packages/cmake/cmake_pip) [`onnx`](/packages/onnx) [`pytorch`](/packages/pytorch) [`torchvision`](/packages/pytorch/torchvision) [`torch2trt`](/packages/pytorch/torch2trt) [`huggingface_hub`](/packages/llm/huggingface_hub) [`rust`](/packages/rust) [`bitsandbytes`](/packages/llm/bitsandbytes) [`auto_gptq`](/packages/llm/auto_gptq) [`transformers`](/packages/llm/transformers) |
| &nbsp;&nbsp;&nbsp;Dockerfile | [`Dockerfile`](Dockerfile) |
| &nbsp;&nbsp;&nbsp;Images | [`dustynv/nanosam:r35.2.1`](https://hub.docker.com/r/dustynv/nanosam/tags) `(2023-10-01, 6.3GB)` |

</details>

<details open>
<summary><b><a id="images">CONTAINER IMAGES</a></b></summary>
<br>

| Repository/Tag | Date | Arch | Size |
| :-- | :--: | :--: | :--: |
| &nbsp;&nbsp;[`dustynv/nanosam:r35.2.1`](https://hub.docker.com/r/dustynv/nanosam/tags) | `2023-10-01` | `arm64` | `6.3GB` |

> <sub>Container images are compatible with other minor versions of JetPack/L4T:</sub><br>
> <sub>&nbsp;&nbsp;&nbsp;&nbsp;• L4T R32.7 containers can run on other versions of L4T R32.7 (JetPack 4.6+)</sub><br>
> <sub>&nbsp;&nbsp;&nbsp;&nbsp;• L4T R35.x containers can run on other versions of L4T R35.x (JetPack 5.1+)</sub><br>
</details>

<details open>
<summary><b><a id="run">RUN CONTAINER</a></b></summary>
<br>

To start the container, you can use the [`run.sh`](/docs/run.md)/[`autotag`](/docs/run.md#autotag) helpers or manually put together a [`docker run`](https://docs.docker.com/engine/reference/commandline/run/) command:
```bash
# automatically pull or build a compatible container image
./run.sh $(./autotag nanosam)

# or explicitly specify one of the container images above
./run.sh dustynv/nanosam:r35.2.1

# or if using 'docker run' (specify image and mounts/ect)
sudo docker run --runtime nvidia -it --rm --network=host dustynv/nanosam:r35.2.1
```
> <sup>[`run.sh`](/docs/run.md) forwards arguments to [`docker run`](https://docs.docker.com/engine/reference/commandline/run/) with some defaults added (like `--runtime nvidia`, mounts a `/data` cache, and detects devices)</sup><br>
> <sup>[`autotag`](/docs/run.md#autotag) finds a container image that's compatible with your version of JetPack/L4T - either locally, pulled from a registry, or by building it.</sup>

To mount your own directories into the container, use the [`-v`](https://docs.docker.com/engine/reference/commandline/run/#volume) or [`--volume`](https://docs.docker.com/engine/reference/commandline/run/#volume) flags:
```bash
./run.sh -v /path/on/host:/path/in/container $(./autotag nanosam)
```
To launch the container running a command, as opposed to an interactive shell:
```bash
./run.sh $(./autotag nanosam) my_app --abc xyz
```
You can pass any options to [`run.sh`](/docs/run.md) that you would to [`docker run`](https://docs.docker.com/engine/reference/commandline/run/), and it'll print out the full command that it constructs before executing it.
</details>
<details open>
<summary><b><a id="build">BUILD CONTAINER</b></summary>
<br>

If you use [`autotag`](/docs/run.md#autotag) as shown above, it'll ask to build the container for you if needed.  To manually build it, first do the [system setup](/docs/setup.md), then run:
```bash
./build.sh nanosam
```
The dependencies from above will be built into the container, and it'll be tested during.  See [`./build.sh --help`](/jetson_containers/build.py) for build options.
</details>