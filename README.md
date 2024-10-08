# Curlio - A cURL Implementation in Rust

`curlio` is a command-line tool built in `Rust` that mimics the functionality of `cURL`. It allows you to send HTTP requests to `URLs` with support for various HTTP methods, custom headers, request body data (including JSON and multipart form data with file uploads), and more. The tool also includes options for verbosity, silence, response storage, Download file, zip, images, videos and retry mechanisms.

## Features

- Supports common HTTP methods like `GET`, `POST`, `PUT`, and `DELETE`.
- Allows custom headers to be passed in JSON format.
- Sends request body data in various formats.
- Supports multipart form data including file uploading.
- Optional verbose mode to show detailed request and response information.
- Silent mode to suppress output.
- Option to store response data to a file.
- Timeout configuration.
- Retry mechanism for handling failed requests.
- Basic and Bearer authentication support.
- Download file, zip, images and videos using `curlio` with nice informatics loading indicator.

## Installation

This CLI is published with `Cargo`. You can easily download and update with `cargo install curlio` command and accept the binary from everywhere.

```bash
cargo install curlio
```

## Local setup

To use `curlio`, you need to have Rust installed on your system. You can install Rust from [here](https://www.rust-lang.org/tools/install).

Once Rust is installed, clone the repository and build the project:

```bash
git clone https://github.com/Kei-K23/curlio.git
cd curlio
cargo build --release
```

## Usage

Run the executable with the necessary arguments to send HTTP requests. Below are the available options:

```bash
curlio 0.4.3
Kei-K23
curlio is a cURL implementation in Rust

USAGE:
    curlio [OPTIONS] <url>

ARGS:
    <url>    The URL to send the request to

Options:
  -X, --request <method>         HTTP method (GET, POST, etc.) [default: GET]
  -d, --data <data>              Sends the specified data in a POST request
  -F, --form <form>              Sends multiple form data using JSON structured format (use file path for file uploading)
  -H, --header <header>          Add headers to the request
  -v, --verbose <verbose>        Show detail information about request and response <f for False/ t for True> [default: f]
  -s, --silent <silent>          Suppress all output <f for False/ t for True> [default: f]
  -t, --timeout <timeout>        Set a timeout for the request (in seconds)
  -r, --retry <retry>            Number of retry attempts in case of failure
  -S, --store <store>            Store the response data to file
  -A, --user-agent <user_agent>  Specify custom User-Agent
  -u, --user <basic_auth>        Provide basic authentication in the format `username:password`
  -L, --location <follow>        Follow HTTP redirects <f for False/ t for True> [default: f]
      --proxy <proxy>            Use HTTP/HTTPS proxy
  -D, --download <download>      Download file and save them in your file system
      --cookies <cookies>        Attach cookies to the request
  -h, --help                     Print help
  -V, --version                  Print version
```

## Examples

### Main Options

1. Simple GET request:

```bash
curlio http://example.com
```

2. POST request with data:

```bash
curlio -X POST -d '{"key":"value"}' http://example.com
```

3. GET request with custom headers:

```bash
curlio -H '{"Content-Type": "application/json"}' http://example.com
```

4. GET request with a timeout:

```bash
curlio -t 5 http://example.com
```

5. Verbose mode:

```bash
curlio -v t http://example.com
```

6. Retry on failure:

```bash
curlio -r 3 http://example.com
```

7. Store the response data to file:

```bash
curlio "https://fakestoreapi.com/products" -X GET -H '{"Accept": "application/json"}' -S "products.json"
```

8. Basic Authentication:

```bash
curlio -u "username:password" http://example.com
```

9. Bearer Token Authentication:

```bash
curlio -H '{"Authorization": "Bearer your_token_here"}' http://example.com
```

10. Cookies file support. Add cookies values to request header:

```bash

# Example cookies json file (name what ever you want just to be sure to be .json file)
# [
#     {
#         "name": "session-id",
#         "value": "235-3769708-3150250"
#     },
#     {
#         "name": "ubid-main",
#         "value": "134-3687901-5787569"
#     },
#     {
#         "name": "session-token",
#         "value": "\"JKASDIUivnisduhfisd213biHUKLFbnoisd2344325\""
#     }
# ]

curlio 'https://fakestoreapi.com/products' -X GET -H '{"Accept": "application/json"}' --cookies cookies.json
```

11. Download files, zips, images, videos as you wish

```bash
curlio "https://file-examples.net/wp-content/uploads/2024/02/SampleTextFile_1MB.txt" -D test.txt

# Example Output
Starting download of 1023385 bytes...
Progress: [#############################                     ] 58.20% (595608/1023385)
```

### Error Handling

If the request fails and no retries are specified, an error message will be displayed in the terminal:

```bash
Request failed: <Error message>
```

If retries are enabled, it will retry the request up to the specified count, and you will see output like:

```bash
Attempt 1 failed, retrying... (<Error message>)
```

## Todo

- [ ] Make binary for other installer methods.
- [ ] Add test cases to cover all use cases.
- [ ] Additional features and improvements.

## License 

This project is licensed under the MIT License - see the [LICENSE](/LICENSE) file for details.

## Contribution

All contributions are welcome. Please open issues or make PR for error, bug, and adding new features.
