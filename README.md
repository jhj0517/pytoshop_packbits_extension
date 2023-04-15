# pytoshop_packbits_extension
This repository is meant to resolve the [stable-diffusion-webui-Layer-Divider #5](https://github.com/jhj0517/stable-diffusion-webui-Layer-Divider/issues/5). 

When pytoshop is installed with cython, the .so and .pyd files are not properly generated, causing issues.
- related issue
  - [pytoshop #9](https://github.com/mdboom/pytoshop/issues/9)

After investigating the issue, it appears that there are some bugs with installing extensions with `cython` using `setuptools`.
- related issue
  - [setuptools #3891](https://github.com/pypa/setuptools/issues/3891)
  - [setuptools #3786](https://github.com/pypa/setuptools/issues/3786)

To solve this issue, I decided to directly download the `so` file.

I used Github's Actions to download `so` file. 

In the `.github\workflows\main.yaml`, there's an example of how pytoshop is installed on macOS to generate the so file using Github's Action.

For some reason, the so file is not generated just by running `pip install pytoshop`

However, if you first run `pip install cython` and then `pip install pytoshop`, it generates the so file.

it means that `pytoshop`'s `setuptools` is not working properly since `cython` is in the requirements of `pytoshop`'s setuptools.
