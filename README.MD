# Debugger Action Tool

## How to use by Frp Server

### Prerequisites

- A [Frp Server](https://github.com/fatedier/frp)

### Usage

1. Set up your credentials as secrets in your repository settings using `FRP_SERVER_ADDR`, `FRP_SERVER_PORT`, `FRP_TOKEN`, `SSH_PORT`

|  Secrets   | Frp Server  |
|  ----  | ----  |
| `FRP_SERVER_ADDR`  | You Server IP |
| `FRP_SERVER_PORT`  | Bind port |
| `FRP_TOKEN`        | token |

`SSH_PORT` is used to login the runner, a custom set , e.g 20090 .

2. Add the following to your workflow

```yml
- uses: halfcoke/gitactions-debugger@v1
  name: debugger
  timeout-minutes: 30
  continue-on-error: true
  with:
    frp_server_addr: ${{ secrets.FRP_SERVER_ADDR }}
    frp_server_port: ${{ secrets.FRP_SERVER_PORT }}
    frp_token: ${{ secrets.FRP_TOKEN }}
    ssh_port: ${{ secrets.SSH_PORT }}
```

3. Run your workflow and login the runner

Each runner needs a unique `ssh_port` value.

```bash
ssh runner@frp_server_addr -p ssh_port 
```

Input RootPassword: root

You have root permission by using "sudo"

4. Debugger the runner

```bash
$ ls

factory
key.pem
perflog
runners
warmup
work
```

`runners` is the working directory of workflow

### Parameters


#### `frp_server_addr`

**Required** IP address of the remote frps server.

#### `frp_server_port`

**Required** Port of the remote frps server.

#### `frp_token`

**Required** Token of the remote frps server.

#### `ssh_port`

**Required** Port to login the runner

### Thanks

[https://github.com/shaowenchen/debugger-action](https://github.com/shaowenchen/debugger-action)

### License

[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)