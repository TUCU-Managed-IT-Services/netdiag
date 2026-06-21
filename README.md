# TUCU NetDiag

A signed, standard-user **Windows network diagnostic tool** — a terminal UI that
scans the LAN, monitors hosts, and runs a deductive fault localizer that tells you
*where* a network problem is (this PC, the LAN/switch, the gateway, or the ISP), not
just that one exists.

Built by [TUCU Managed IT Services](https://tucu.ca) for field technicians. Drops onto
any Windows 10/11 or Windows Server box and runs immediately — **no install, no admin,
no driver, no Npcap.**

## Download

Grab the latest signed `tucu-netdiag.exe` from the [**Releases**](../../releases) page.
A single self-contained executable (~3 MB). No installer.

## Verify the signature

The binary is Authenticode-signed by **TUCU Managed IT Services Inc** via Azure
Trusted Signing. Before running a downloaded executable, confirm the signature in
PowerShell:

```powershell
Get-AuthenticodeSignature .\tucu-netdiag.exe | Format-List Status, SignerCertificate
```

Expect `Status : Valid` and a signer of
`CN=TUCU Managed IT Services Inc, O=TUCU Managed IT Services Inc, L=Toronto, S=Ontario, C=CA`.

> **SmartScreen:** a freshly published release may show a Microsoft Defender
> SmartScreen prompt until the signing certificate accrues reputation. The valid
> signature above is the thing to verify.

## Usage

Run with no arguments for the interactive TUI:

```
tucu-netdiag.exe
```

Tabs: **Discover** (LAN scan) · **Monitor** (live host watch) · **Diagnose**
(path-to-internet + verdict) · **Speed** (throughput + bufferbloat) · **Report**.

Headless modes for RMM / background scripts — self-terminating (no Ctrl-C needed) and
the exit code reflects severity (`0` clear · `1` warning · `2` fault · `3` error):

```
tucu-netdiag.exe --headless --diagnose                       # map the path, measure, print a ticket-ready verdict
tucu-netdiag.exe --monitor 192.168.1.1 --count 20 --headless # bounded host monitor
tucu-netdiag.exe --speedtest                                 # throughput + bufferbloat grade
```

`tucu-netdiag.exe --help` lists every flag.

## Source

This repository hosts **public release binaries only.** The source is maintained
privately by TUCU.
