# Pkl Systemd

Pkl templates for configuring [Systemd](https://systemd.io/).

## Usage

Create `hello.pkl`:

```pkl
amends "package://pkl.declix.org/pkl-systemd@0.0.6#/Service.pkl"

service = new {
    execStart = "bash -c 'echo hello'"
}

unit = new {
    description = "hello service"
    wants = "network-online.target"
    after = "network-online.target"
}

install = new { 
    wantedBy = "default.target" 
}
```

```text
$ pkl eval hello.pkl
[Unit]
After=network-online.target
Description=hello service
Wants=network-online.target

[Install]
WantedBy=default.target

[Service]
ExecStart=bash -c 'echo hello'
```
