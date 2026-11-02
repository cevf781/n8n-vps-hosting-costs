# n8n vps hosting: what a self-hosted setup really costs, which plan size you actually need, and how to get it running in minutes

Most people searching for n8n VPS hosting want the same three answers: how much a server will cost per year, how much RAM n8n genuinely needs, and whether a cheap KVM VPS is good enough for production workflows. Short version: a KVM VPS with 2 GB of RAM covers the majority of self-hosted n8n setups, you can get one for roughly $22–36 per year, and deployment takes minutes either through a one-click installer or Docker.

One thing worth clearing up immediately, because it changes the whole cost picture: n8n itself doesn't charge you for self-hosting. The server is the only bill. VPS providers who market "n8n hosting" are selling you a regular VPS, sometimes with a template pre-installed. Once you understand that, you can price the decision on raw specs and renewal terms, which is exactly what this article does, using RackNerd's current published plans as the working example.

> **Quick picks**
> - Testing and light workflows: the 1 GB KVM VPS at **$21.99/year** works, though 2 GB is the safer floor for anything you plan to keep running.
> - Most people should start at the **2 GB KVM VPS, $35.99/year**. RackNerd's own FAQ says n8n is "comfortable from 2 GB," and this plan renews at the same price for as long as you keep it.
> - Queue mode, large payloads, or heavy concurrent executions: 4 GB ($59.99/year) and up.
> - 👉 [Check RackNerd's current VPS specials and prices](https://bit.ly/RacKnerd)

## Why n8n needs a VPS in the first place

If your workflows are triggered by external services (GitHub, forms, CRMs, anything sending a webhook), n8n has to be reachable from the public internet. That's the official n8n documentation's own framing, and it's the reason running n8n on your laptop hits a wall fast.

n8n does ship a tunnel feature based on cloudflared that exposes a local instance to the web, but the docs are explicit that it's for local development and testing, and "it isn't safe to use it in production." The tunnel's implementation can also change between n8n versions, which is not what you want underneath business-critical automations.

A VPS solves this the boring, reliable way: a static IPv4, a 1Gbps port, and a machine that stays on. Every RackNerd KVM plan includes one IPv4 address and the 1Gbps port as standard, so there's no separate "webhook add-on" to worry about.

## RackNerd's plans for running n8n

RackNerd currently lists two families of KVM VPS plans, and the difference matters for an n8n budget. The specials page is annual-only and priced aggressively; the standard Los Angeles KVM page bills monthly and costs several times more for similar specs.

### Annual specials (the ones built for self-hosting)

All five are KVM virtualization with full root access, 1Gbps port, one IPv4, and instant deployment. Per the official FAQ, these are "lifetime recurring": you renew at the same rate for as long as you keep the service.

| Plan | CPU / RAM / SSD | Monthly traffic | Price (annual) | Order |
| --- | --- | --- | --- | --- |
| 1 GB KVM VPS (most popular) | 1 vCPU / 1 GB / 20 GB | 3 TB | $21.99/yr | [Order the 1 GB plan](https://my.racknerd.com/cart.php?a=add&pid=952&aff=11397) |
| 2 GB KVM VPS | 2 vCPU / 2 GB / 35 GB | 5 TB | $35.99/yr | [Order the 2 GB plan](https://my.racknerd.com/cart.php?a=add&pid=953&aff=11397) |
| 4 GB KVM VPS | 3 vCPU / 4 GB / 60 GB | 7 TB | $59.99/yr | [Order the 4 GB plan](https://my.racknerd.com/cart.php?a=add&pid=954&aff=11397) |
| 6 GB KVM VPS | 6 vCPU / 6 GB / 100 GB | 12 TB | $89.99/yr | [Order the 6 GB plan](https://my.racknerd.com/cart.php?a=add&pid=955&aff=11397) |
| 8 GB KVM VPS | 7 vCPU / 8 GB / 150 GB | 20 TB | $119.99/yr | [Order the 8 GB plan](https://my.racknerd.com/cart.php?a=add&pid=956&aff=11397) |

### Standard Los Angeles KVM plans (monthly billing)

The LA page is billed monthly and runs on Intel Xeon hardware with RAID-10 SSD and a network optimized by Noction IRP. It's the right pick only if you genuinely need month-to-month flexibility.

| Plan | CPU / RAM / SSD | Monthly traffic | Price | Order |
| --- | --- | --- | --- | --- |
| 512 MB | 1 vCore / 512 MB / 30 GB | 500 GB | $26.99/yr | [Order the 512 MB plan](https://my.racknerd.com/cart.php?a=add&pid=1&aff=11397) |
| 1 GB | 2 vCore / 1 GB / 50 GB | 1 TB | $17.99/mo | [Order the 1 GB monthly plan](https://my.racknerd.com/cart.php?a=add&pid=20&aff=11397) |
| 2 GB | 3 vCore / 2 GB / 75 GB | 2 TB | $20.59/mo | [Order the 2 GB monthly plan](https://my.racknerd.com/cart.php?a=add&pid=21&aff=11397) |
| 4 GB | 4 vCore / 4 GB / 130 GB | 3 TB | $24.59/mo | [Order the 4 GB monthly plan](https://my.racknerd.com/cart.php?a=add&pid=22&aff=11397) |
| 6 GB | 5 vCore / 6 GB / 170 GB | 4 TB | $27.59/mo | [Order the 6 GB monthly plan](https://my.racknerd.com/cart.php?a=add&pid=23&aff=11397) |
| 8 GB | 6 vCore / 8 GB / 220 GB | 5 TB | $36.59/mo | [Order the 8 GB monthly plan](https://my.racknerd.com/cart.php?a=add&pid=24&aff=11397) |
| 12 GB | 7 vCore / 12 GB / 300 GB | 6 TB | $55.99/mo | [Order the 12 GB monthly plan](https://my.racknerd.com/cart.php?a=add&pid=25&aff=11397) |

For an n8n box, the annual specials win almost every time. The 2 GB special costs $35.99 per year; the 2 GB monthly plan on the standard page costs $20.59 *per month*, which is $247.08 over the same year. Same RAM, same brand, roughly 7x the price. Monthly billing only makes sense if you're spinning something up for a short-lived project and want the freedom to cancel.

## How much server does n8n actually need?

Less than most "n8n VPS" marketing pages imply. n8n's official prerequisites put memory in the 320 MB to 2 GB range and note that the software "isn't CPU intensive," so even small cloud instances are generally enough. The database (SQLite by default, PostgreSQL if you configure it) needs 512 MB to 4 GB of SSD.

RackNerd's own FAQ lines up with this. Their one-click app guidance ranks the apps by RAM appetite: OpenClaw wants at least 8 GB, tools like AnythingLLM, Ollama, and LibreChat want 4 GB, and then this: "n8n or Coolify are comfortable from 2 GB."

Putting the sources together gives a practical sizing ladder:

- **1 GB (special, $21.99/yr)**: fine for testing, learning Docker, and workflows that run a few times a day. n8n's supported memory floor technically reaches down here. Expect tightness if you stack PostgreSQL on the same box or process large payloads.
- **2 GB (special, $35.99/yr)**: the recommended starting point. Comfortable for n8n plus SQLite, or n8n plus a small PostgreSQL container, with headroom for OS overhead.
- **4 GB ($59.99/yr)**: the sensible choice when you add PostgreSQL, run multiple Docker services alongside n8n, or handle bigger payloads. The jump from the 2 GB plan is $24 a year; if you already know PostgreSQL is going on the same box, that $24 buys real headroom instead of an upgrade chore later.
- **6–8 GB ($89.99–$119.99/yr)**: this is queue-mode territory, where n8n runs with separate workers plus Redis and PostgreSQL. A European host's n8n sizing guide maps exactly this stack to its 4 GB-plus tiers, so if your automations involve heavy concurrency, plan for 4 GB minimum and don't be shy about 6–8 GB.

Worth knowing: on the standard KVM plans you can upgrade to the next tier later, and RackNerd says the transition only requires about a minute of downtime for a reboot. So starting small on a special and stepping up if you outgrow it is a legitimate strategy.

## The real cost over two or three years

This is where cheap-VPS pricing either holds up or falls apart, so it's worth doing the math with published numbers.

The renewal question is the big one, because plenty of budget hosts hook you with a first-year teaser and then reset to a higher rate. RackNerd's specials FAQ states directly that these plans are "lifetime recurring" and renew at the same rate. That claim also circulates among users: one widely shared renewal-pricing writeup documents an $11.29/year plan renewing at exactly the same price three years in, with other users reporting the same pattern into year four.

So for the recommended 2 GB special at $35.99/year:

- Year 1: $35.99
- Three years: $107.97
- Five years: $179.95

Compare that to n8n Cloud or any per-execution billing model, or to a monthly-billed VPS, and the gap gets wide fast. A monthly 2 GB plan at $20.59 (standard LA page) costs $247.08 in year one alone.

One trap to avoid: the specials are annual-only. If you order one, you're committing for a year. That's the trade you make for the locked-in price. If you can't stomach a 12-month commitment, the standard monthly plans exist for exactly that reason, and you pay for the flexibility.

## Getting n8n running: one click or Docker

There are two realistic paths, and both work on any of the plans above.

**Path 1: the one-click installer.** Every RackNerd special includes the ctrl control panel, which handles reboot, OS reinstall, an HTML5 VNC console, root password resets, and a network firewall. Among its one-click apps sits n8n itself. The flow is: deploy the VPS, open One-Click Apps in ctrl, select n8n, and credentials show up in-panel once it's ready. You can also install Docker with Portainer the same way if you'd rather manage containers yourself. If you've never administered a server, this is the shortest route from payment to a working n8n login page.

**Path 2: Docker, the official way.** n8n's documentation recommends Docker for most self-hosting, since it sidesteps OS compatibility issues and keeps database management contained. The essentials from the official install guide:

1. Install Docker Engine and Docker Compose (RackNerd offers Ubuntu, Debian, Rocky Linux, AlmaLinux, CentOS, and Fedora images; custom ISOs are available via a support ticket).
2. Run the official n8n image with port 5678 exposed on the host.
3. Mount a data volume at `/home/node/.n8n` so your credentials, execution history, and workflows survive container restarts. This step is not optional in any practical sense; skipping it means rebuilding everything after every update.
4. For anything beyond experimentation, switch from the default SQLite to PostgreSQL using environment variables. A complete docker-compose file for that setup is published in n8n's official hosting repository.
5. Updating means pulling the latest image and restarting the container. Budget ten minutes per update.

Either way, remember the firewall angle: your n8n instance needs port 5678 (or whatever you map) reachable from the web for webhooks to land. RackNerd's ctrl Network Firewall filters inbound traffic in front of the VPS, so open the port there as well as in your OS firewall, or you'll spend an afternoon debugging why GitHub's webhook pings vanish.

## What a budget VPS doesn't give you

Honesty time, because this affects expectations.

RackNerd's KVM VPS is unmanaged. You get full root access and 24/7 support for infrastructure problems, but n8n itself, Docker, updates, and security hardening are on you. The one-click installer lowers the entry barrier a lot, yet you're still the sysadmin.

Resource isolation has practical limits too. Third-party plan writeups of RackNerd's lineup point out that KVM allocations sit on shared physical hardware, so entry-level plans can occasionally feel noisy-neighbor effects, described as uncommon but possible. For most n8n workloads, which idle most of the day, this rarely matters. If your automations are latency-sensitive around the clock, it's a fair reason to look at bigger plans or a different host tier.

And the flip side of the one-click app is worth stating: installing n8n is easy; operating it (backups, updates, monitoring) is still your job. RackNerd sells optional backup add-ons at checkout if you want the server side covered.

## How this compares with n8n-focused VPS providers

Several hosts market n8n hosting specifically, and they're legitimate options with different trade-offs. Hostinger sells n8n VPS templates and, in its own sizing guidance, suggests 8+ vCPU cores and 16+ GB RAM (its KVM 8 tier) for high-load webhook and AI workloads, which is a much pricier spec than most setups need. Cloudzy advertises n8n VPS plans from around $2.48/month, which lands in a similar price band to RackNerd's specials. Contabo publishes a detailed Docker self-hosting guide for n8n on its VPS line. Some smaller EU-focused hosts publish n8n-specific sizing tables starting around €4/month for a 2 GB machine.

None of these do anything your own VPS with Docker can't do. The template-and-managed-experience layer is what you're paying extra for, where it exists. If you're comfortable with the five-step Docker setup above, buying raw KVM capacity and locking in a multi-year renewal price is the cheaper route.

## FAQ

**Can the $21.99/year 1 GB plan actually run n8n?**
Yes, for light use. n8n's official docs list memory requirements as low as a few hundred MB, and a 1 GB box handles test workflows and low-frequency executions. For a production instance you'll keep, start at 2 GB, which both RackNerd's FAQ and general community sizing treat as the comfortable floor.

**Do I pay n8n anything for self-hosting?**
No. The self-hosted Community Edition is free to install, and your VPS bill is the whole cost. Providers advertising n8n hosting without per-task billing are describing this exact arrangement.

**Which datacenter location should I pick?**
RackNerd operates 20 locations across North America, Europe, and Asia, including Los Angeles, New York, Amsterdam, London, and Strasbourg. Pick whichever is closest to where your workflows' traffic originates. The LA location runs an Asia-optimized network, and LA and France can also provision up to 100 free IPv6 addresses on request via a support ticket, useful if any of your integrations are IPv6-only.

**Can I upgrade later if my workflows grow?**
On the standard KVM plans, yes, and the official FAQ says the upgrade only needs about a minute of reboot downtime. Plan sizing is therefore less scary than it looks: start at 2 GB, move up when queue mode or PostgreSQL demands it.

**Monthly or annual?**
Annual specials if you're keeping the server, without much hesitation. The 2 GB special is $35.99/year versus $247.08 for twelve months of the comparable standard plan, and the special renews at the same price. Monthly only earns its premium when you don't know if you'll still need the server next month.

## The bottom line before you order

Match the plan to what you'll actually run: experimenting and low-frequency workflows, the 1 GB special at $21.99/year is enough. A personal or small-business automation stack, the 2 GB special at $35.99/year is the pick, and its renewal price is locked for as long as you keep it. Queue mode with Redis and PostgreSQL, or large payloads and concurrent executions, go 4 GB or 6 GB.

Two things to check before checking out: confirm you're fine with an annual commitment (specials don't do monthly), and remember the box arrives unmanaged, so the one-click n8n install in ctrl is your friend if server administration is new to you. When you've settled on a size, 👉 [the 2 GB KVM VPS order page](https://my.racknerd.com/cart.php?a=add&pid=953&aff=11397) is the one most n8n self-hosters should land on, and if you're still comparing, 👉 [browse RackNerd's full current specials list](https://bit.ly/RacKnerd) to check the latest prices and datacenter options before you commit.
