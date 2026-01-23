# Reference Design Setup

## Pre-requisites

- Python >=3.12 in local machine
- uv (Python's package manager) in local machine
- Docker Desktop installed and running in local machine

Open your working directory in terminal (e.g., Powershell, cmd, bash)

> *Note: I am using Windows' `cmd` within `D:\Others\mitre-ectf\` directory.*

## Step 1: Clone the Repository

```bash
git clone https://github.com/ectfmitre/2026-ectf-insecure-example/ && cd 2026-ectf-insecure-example
```

## Step 2: Creating a Deployment

Within the `2026-ectf-insecure-example` directory, run the following commands:

```bash
uv venv --prompt "ectf26" && uv pip install -e .\ectf26_design\
```

```bash
uv run secrets -f .\global.secrets 1 2 3 0x1111
```

## Step 3: Build the Firmware

> Note: Build Docker image if it's not already built. `docker build -t build-hsm .\firmware`

```bash
docker run --rm -v .\firmware:/hsm -v .\global.secrets:/secrets/global.secrets:ro -v .\build:/out -e HSM_PIN="abc123" -e PERMISSIONS="1234=R--:4321=RWC" build-hsm
```

## Step 4: Flash the firmware

### Hardware Update Mode / Bootloading

> *Note: On the MSPM0 LITO Boards, bootloading once is sufficient. **Hold the S2 (PB21) button and connect the device to a host machine to enter update mode.***
>
> *However, On the MSPM0 L2228 LaunchPad, follow the [Bootloader Setup](bootloader-setup.md) instructions to enter update mode.*

### Erase & Flash Firmware

```bash
uvx ectf hw COM3 erase && \
uvx ectf hw COM3 flash .\build\hsm.bin -n hsm && \
uvx ectf hw COM3 start
```

## Step 5: Test

```bash
uvx ectf tools COM3 list <HSM_PIN>
```

## Sample Usecase

### HSM A

```bash
# build the binary for HSM A
docker run --rm -v .\firmware:/hsm -v .\global.secrets:/secrets/global.secrets:ro -v .\build:/out -e HSM_PIN="abc123" -e PERMISSIONS="1111=-W-" build-hsm

uvx ectf hw COM5 erase && uvx ectf hw COM5 flash .\build\hsm.bin -n hsm && uvx ectf hw COM5 start

uvx ectf tools COM5 list abc123
```

```bash
echo Test file contents > test-file.txt
```

```bash
uvx ectf tools COM5 write 123abc 0 0x1111 .\test-file.txt && uvx ectf tools COM5 list 123abc
```

```bash
uvx ectf tools COM5 listen
```

### HSM B

```bash
# built the binary for HSM B
docker run --rm -v .\firmware:/hsm -v .\global.secrets:/secrets/global.secrets:ro -v .\build:/out -e HSM_PIN="567def" -e PERMISSIONS="1111=R-C" build-hsm

uvx ectf hw COM8 erase && uvx ectf hw COM8 flash .\build\hsm.bin -n hsm && uvx ectf hw COM8 start

uvx ectf tools COM8 list 567def
```

```bash
uvx ectf tools COM8 interrogate 567def
```
