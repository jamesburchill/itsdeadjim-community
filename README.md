# 🧠 Dead Jim Community Repo

> “It's Dead, Jim!”
> — Every engineer’s least favourite moment

**Dead Jim** watches your devices, servers, and systems for signs of life — and calls time of death when they stop talking.

This repo hosts **open-source agents** for various platforms. Each one’s tiny, easy to deploy, and designed to “ping” the Dead Jim server when it boots or at set intervals. When the pings stop… well, you get the idea.

---

## 🚀 Quick Start

1. **Pick your platform** from the [agents](https://github.com/jamesburchill/itsdeadjim-community/blob/main/agents) folder:

   * Raspberry Pi Pico W
   * Linux (Bash or Python)
   * Windows (PowerShell)
   * ESP32 / ESP8266
   * Docker container

2. **Edit the config** (Wi-Fi, server URL, and API token).

3. **Deploy** — flash, copy, or build depending on the agent.

4. **Watch Dead Jim record the heartbeat**.

5. When power or connectivity drops, Dead Jim will raise an alert once your timeout threshold expires.

Example ping payload:

```json
{
  "device_id": "aabbccddeeff",
  "status": "boot",
  "timestamp": 1738727396
}
```

---

## 🧩 Agents

| Platform                               | Language    | Description                              |
| -------------------------------------- | ----------- | ---------------------------------------- |
| [Pico W](./agents/pico-w)              | MicroPython | Boots, connects Wi-Fi, posts “I’m alive” |
| [Linux (Bash)](./agents/linux-bash)    | Bash + curl | Runs via cron or systemd timer           |
| [Windows](./agents/windows-powershell) | PowerShell  | Lightweight heartbeat script             |
| [ESP32](./agents/esp32)                | MicroPython | Low-power deep-sleep option              |
| [Docker](./agents/docker)              | Shell       | Container-based monitor                  |
| [Python Generic](./agents/python)      | Python 3    | Works anywhere with `requests`           |

---

## 🛠️ Server-Side Overview

Each agent talks to the **Dead Jim Core** server.
It listens on a simple REST endpoint (default: `api.itsdeadjim.com/v1/heartbeat`).

_For convenience you can also use this endpoint too: `api.itsdeadjim.com/ping` (it does the same thing and routes to the heartbeat end point.)_

When the server hasn’t heard from a device for a configured period, it logs a **down event** and, depending on your setup, emails, texts, or posts alerts.

![architecture diagram placeholder](docs/diagram-deadjim-arch.png)

---

## 🔐 Authentication

Agents authenticate with a short-lived bearer token:

```bash
Authorization: Bearer <your-token-here>
```

Keep tokens private; they identify your devices. Rotate them periodically if you distribute public builds.

---

## 🧰 Examples & Extras

You’ll find real-world setups in [`examples/`](./examples):

* Linux cron job (`@reboot`)
* systemd timer unit
* Docker Compose snippet
* Pico W autostart script

---

## 💬 Docs & FAQ

* [Quickstart](./docs/quickstart.md)
* [FAQ](./docs/faq.md)
* [Architecture](./docs/architecture.md)
* [Contributing](./docs/contributing.md)

---

## 🤝 Contributing

Pull requests welcome!
If you’ve got an idea for a new agent, open a PR that includes:

1. Working code in its own subfolder
2. A short `README.md` explaining setup
3. A test payload example

Please don’t include secrets or tokens in your examples.

---

## 🪦 License

All Dead Jim Agents are released under the **MIT License**.
Do whatever you like — just don’t blame us if your system actually dies.

---

## 🧭 Links

* [Official Dead Jim Site](https://itsdeadjim.com)
* [API Docs Portal](https://api.itsdeadjim.com/docs)
* [Community Discussions](https://github.com/jamesburchill/itsdeadjim-community/discussions)

---
