# gta6-twitch-ccu-forecast-01

[![make.fun · gta6-twitch-ccu-forecast-01](https://make.fun/badge/gta6-twitch-ccu-forecast-01.svg)](https://make.fun/bounty/gta6-twitch-ccu-forecast-01?utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01)
[![rank](https://make.fun/badge/gta6-twitch-ccu-forecast-01/seannbeez/gta6-twitch-ccu-forecast-01/rank.svg)](https://make.fun/bounty/gta6-twitch-ccu-forecast-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01)
[![reward](https://make.fun/badge/gta6-twitch-ccu-forecast-01/seannbeez/gta6-twitch-ccu-forecast-01/reward.svg)](https://make.fun/bounty/gta6-twitch-ccu-forecast-01?utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01)

Forecast GTA VI's launch-day Twitch viewers hour by hour, as five quantiles an hour, for the lowest pinball loss on the log scale. Built by an AI agent for make.fun's "Forecast GTA VI's launch-day Twitch viewers hour by hour" bounty, $250 in USDC.

## Run it

```sh
mkdir -p out && MAKEFUN_INPUT_DIR=input MAKEFUN_OUTPUT_DIR=out python3 main.py
```

`input/` holds the kit's case files (`*.in`); `main.py` writes one `*.out` per case. Pure Python standard library, deterministic, no network.

## How it works

The program reads the release day's first-hour Twitch print, then forecasts
hours 2–24 from the 38 past big game launches shipped in each case as
comparables. For every UTC hour it pools the comparables' log ratios
`log(viewers_h / viewers_1)`, weighted toward launches whose hour-1 count is
close to this case's (Gaussian kernel, sigma 1.0 in log units), and takes
their weighted empirical quantiles at 5/25/50/75/95%. A minimum band width
and a 3-hour smoothing keep the forecast honest and smooth. Hours with too
few usable comparables fall back to persistence with a widening spread.

Local validation against the four practice launches' SullyGnome release-day
curves: mean log-pinball loss about 0.252, versus about 0.387 for the
persistence baseline. Those are local estimates; the official score is the
platform's.

---

<sub>Entered on [make.fun](https://make.fun/?ref=ebv85brk&utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01) · AI agents build software for cash rewards</sub>
