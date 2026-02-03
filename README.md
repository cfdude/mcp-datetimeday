# mcp-datetimeday

A lightweight MCP server for date, time, and day of week.

## Installation

```bash
pip install mcp-datetimeday
```

Or with uv:
```bash
uv pip install mcp-datetimeday
```

## Usage

### Claude Code

```bash
claude mcp add --scope user mcp-datetimeday -- uvx mcp-datetimeday
```

### Claude Desktop

Add to your config (`~/Library/Application Support/Claude/claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "datetimeday": {
      "command": "uvx",
      "args": ["mcp-datetimeday"]
    }
  }
}
```

## Available Tools

| Tool | Description |
|------|-------------|
| `get_datetime` | Get current date/time with **day of week** first. Supports `tz` arg for timezone, `format` arg: `iso8601`, `unix`, `human`, or full (default). |
| `relative_time` | Get relative time between dates (e.g., "3 days ago", "in 2 weeks") |
| `days_in_month` | Get number of days in a month with first/last day info |
| `convert_time` | Convert time between timezones |
| `get_week_year` | Get week number, ISO week, day of year, quarter |

## Example Output

### `get_datetime()`
```json
{
  "day_of_week": "Monday",
  "date": "2026-02-02",
  "time": "16:55:22",
  "timezone": "PST",
  "utc_offset": "-0800",
  "iso8601": "2026-02-02T16:55:22-08:00",
  "unix_timestamp": 1770080122,
  "human_readable": "Monday, February 02, 2026 at 04:55 PM"
}
```

### `get_datetime(format="iso8601")`
```json
{
  "day_of_week": "Monday",
  "iso8601": "2026-02-02T16:55:22-08:00"
}
```

### `get_datetime(tz="UTC")`
```json
{
  "day_of_week": "Tuesday",
  "date": "2026-02-03",
  "time": "00:55:22",
  "timezone": "UTC",
  "utc_offset": "+0000",
  "iso8601": "2026-02-03T00:55:22+00:00",
  "unix_timestamp": 1738544122,
  "human_readable": "Tuesday, February 03, 2026 at 12:55 AM"
}
```

### `relative_time("2026-02-10")`
```json
{
  "target": "2026-02-10",
  "target_day_of_week": "Tuesday",
  "reference": "now",
  "relative": "in 1 week",
  "days_difference": 7,
  "total_seconds": 604800
}
```

### `get_week_year()`
```json
{
  "date": "2026-02-02",
  "day_of_week": "Monday",
  "day_of_week_number": 1,
  "week_number": 5,
  "iso_week": 6,
  "iso_year": 2026,
  "day_of_year": 33,
  "days_remaining_in_year": 332,
  "is_weekend": false,
  "quarter": 1
}
```

## Development

```bash
git clone https://github.com/cfdude/mcp-datetimeday.git
cd mcp-datetimeday
uv sync
uv run mcp-datetimeday
```
