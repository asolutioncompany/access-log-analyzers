# access-log-analyzers

Bash shell scripts to analyze WordPress access logs for bot detection.

Run both scripts from the directory that contains your access logs (e.g. `access.log`).

---

## access-top

Shows the top N remote hosts by request count from the access log, with reverse DNS hostname. Only the number of unique IPs actually present (up to N) are processed.

### Usage

```text
./access-top [--all] [-n N | --top N] [filter_string]
```

### Options

| Option | Description |
|--------|-------------|
| `--all` | Include all rotated logs matching `./access.log*` (including `.gz`). Default is only `./access.log`. |
| `-n N` / `--top N` | Show at most N top remote hosts (default: 100). |
| `filter_string` | Optional. Only count log lines that contain this string. |

### Examples

```bash
./access-top
./access-top -n 50
./access-top --all
./access-top "bot"
./access-top --all -n 200 "/wp-login.php"
```

---

## access-details

Shows up to N of the most recent log entries that match a string. Output includes date/time, status, remote IP, hostname, URL, and user agent. Only the actual number of matching entries (up to N) are processed.

### Usage

```text
./access-details [--all] [-n N] <match_string>
```

### Options

| Option | Description |
|--------|-------------|
| `--all` | Search all rotated logs matching `./access.log*` (including `.gz`). Default is only `./access.log`. |
| `-n N` | Show at most N matching entries (default: 100). |
| `match_string` | Required. Only lines containing this string (e.g. an IP or path) are shown. |

### Examples

```bash
./access-details 192.168.0.1
./access-details -n 50 crawler
./access-details --all crawler
./access-details --all -n 200 "/wp-admin"
```
