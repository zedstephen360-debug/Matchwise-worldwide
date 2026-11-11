# MatchWise — Worldwide Multi-Sport Predictor

MatchWise is a multi-sport match analysis starter app. It supports two data paths:

1. **Connected event feed:** ESPN endpoints for a limited set of supported competitions.
2. **Universal CSV import:** historical results for any sport, league, country or competition, including beach soccer and local/regional events.

## Run locally

Requires Node.js 18+.

```bash
npm install
npm start
```

Open http://localhost:3000.

## Universal match-history CSV

For any sport without a live provider connection, import a CSV with these columns:

```csv
date,team_a,team_b,score_a,score_b
2026-10-01,Coastal FC,Desert United,3,2
2026-10-08,Desert United,Coastal FC,1,1
```

Enter the two team names in the manual comparison fields and choose **Analyse imported teams**. Scores can represent goals, points, sets, runs, rounds won, or another numeric result that is comparable within that sport. For sports with non-comparable score formats (for example, motorsport positions or combat-sport decisions), a sport-specific model is required; do not treat this generic score model as validated.

## Global coverage: important distinction

The app now includes a worldwide sport directory, including football/soccer, basketball, rugby, tennis, beach soccer, futsal, volleyball, handball, field hockey, badminton, table tennis, MMA, boxing, motorsport and esports. **A sport appearing in the directory does not mean a live worldwide fixture/history feed is connected for it.**

The built-in ESPN adapter covers only selected competitions and is an unofficial endpoint. For genuine worldwide automatic event discovery and reliable historical records, configure licensed provider adapters with coverage for each sport, league, gender, age group and region. No single free feed reliably covers every sport and competition worldwide. Beach soccer in particular needs a dedicated feed or an imported historical dataset.

## Prediction model and safeguards

- Recent form and scoring margin are used in the baseline.
- Available head-to-head results are displayed where the connected feed supplies them.
- Sample size and data coverage are shown.
- Missing data is not fabricated.
- The model is not yet validated/calibrated and does not incorporate injuries, line-ups, player availability, venue-specific effects, rest, travel, weather or sport-specific tactical metrics.
- Probabilities are estimates, not guarantees or betting advice.

## Production roadmap

1. Add documented, licensed APIs per sport (fixtures, results, standings, team/player stats, injuries and line-ups).
2. Normalize all provider responses into one internal event/team/result schema.
3. Build sport-specific models: Elo/rating models for team sports, Poisson score models for soccer variants, set/game models for tennis and volleyball, and domain-specific models for combat sports and motorsport.
4. Store historical data and back-test predictions out of sample.
5. Calibrate probabilities and report Brier score/log loss by sport and competition.
6. Add provider attribution, API key management, caching, rate limits, monitoring and automated data-quality checks.

## Files

- `public/index.html`: responsive UI, competition search, universal CSV import and baseline analysis.
- `server.js`: Express proxy for supported ESPN endpoint calls.
- `package.json`: Node dependencies.


## Install on Android (PWA)

MatchWise now includes a web app manifest, app icon, and service worker. To install it on Android:

1. Deploy this app to a host that serves it over **HTTPS** (or test on `http://localhost` on the same device).
2. Open the deployed address in Chrome on Android.
3. Open Chrome's menu and tap **Install app** or **Add to Home screen**.
4. Confirm. MatchWise will appear on your home screen and open in its own app window.

The app shell can load offline after it has been visited once, but live sports data and API requests still require an internet connection. The PWA does not turn the current limited sports feed into complete worldwide live coverage.
