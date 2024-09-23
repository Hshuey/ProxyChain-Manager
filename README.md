
# ProxyChain Manager Script

This Python script automates the process of selecting, testing, and configuring proxies for `proxychains`. It allows you to dynamically select working proxies from a proxy list, configure the `proxychains.conf` file, and launch an application (like Firefox, Chrome, etc.) through these proxies.

## Features

- **Auto-updates from the Proxy List repository**: Pulls fresh proxy lists from the [monosans/proxy-list](https://github.com/monosans/proxy-list) GitHub repository.
- **Proxy testing**: Only working proxies are added, based on actual response time and timeout values from the proxy list.
- **Proxy configuration**:
  - **Random chain**: Proxies are used randomly from the list.
  - **Chain length**: Set to 1 to use one proxy at a time.
  - **Disable DNS proxying**: DNS queries are resolved locally instead of via the proxy.
- **Customizable proxy count**: Use the `--num-proxies` flag to specify how many proxies to use (default is 10, but can be set higher).
- **Custom application support**: Use the `--app` flag to specify the application to run through `proxychains` (default is Firefox).

## Requirements

- Python 3.x
- `proxychains` installed on your system
- `git` installed (for pulling the proxy list)
- Python packages:
  - `requests`

## Installation

1. Clone the repository:

    ```bash
    git clone https://github.com/yourusername/proxychain-manager.git
    cd proxychain-manager
    ```

2. Install required dependencies:

    ```bash
    pip install requests
    ```

3. Ensure `proxychains` is installed on your system. On most Linux distributions, you can install it with:

    ```bash
    sudo apt install proxychains
    ```

## Usage

The script provides a set of options to customize the proxy configuration and the application launched via `proxychains`.

### Basic Usage

```bash
python3 sel-prox.py
```

By default, the script will:
- Use up to 10 working proxies.
- Launch Firefox through `proxychains`.

### Customizing Proxy Count

You can specify how many proxies to use with the `--num-proxies` flag. For example, to use 15 proxies:

```bash
python3 sel-prox.py --num-proxies 15
```

### Running a Custom Application

You can also specify which application to run through `proxychains` using the `--app` flag. For example, to run Chrome:

```bash
python3 sel-prox.py --app chrome
```

### Example: Using 20 Proxies and Running Chrome

```bash
python3 sel-prox.py --num-proxies 20 --app chrome
```

## Configuration

The script automatically configures the following options in `proxychains.conf`:
- **Random chain**: Proxies are used randomly.
- **Chain length set to 1**: Only one proxy is used at a time.
- **DNS proxying disabled**: DNS queries are not proxied through the selected proxies.

It also removes the default `Tor` entry (`socks4 127.0.0.1 9050`) if present.

## Proxy Selection and Testing

The script:
- Pulls the latest proxy list from the [monosans/proxy-list](https://github.com/monosans/proxy-list) GitHub repository.
- Filters proxies by country, allowing you to choose from available locations.
- Tests proxies to ensure they are working and respond within a reasonable time (default 1 second timeout).
- If fewer than 5 working proxies are found, the script prompts you to proceed or cancel.

## Contributing

Feel free to contribute by:
- Submitting bug reports and feature requests.
- Forking the repository and creating pull requests.

## License

This project is licensed under the MIT License
