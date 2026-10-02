# CFB Fundamental Handicapping Playbook

**Markets covered:** full-game total, team total, first-half spread.
**Scope:** research angles, how to weigh them, what to ignore, and a repeatable weekly process. This is deliberately *not* an exact-score model. The goal is to build a defensible directional view (over/under, favorite/dog in the first half) with a confidence grade, then let the market tell you whether your view is priced.

---

## Table of contents

1. [Operating principles](#1-operating-principles)
2. [What each market actually prices](#2-what-each-market-actually-prices)
3. [Data sources](#3-data-sources)
4. [The angle library](#4-the-angle-library)
   - 4.1 Pace, tempo, possessions
   - 4.2 Efficiency
   - 4.3 Explosiveness and variance
   - 4.4 Trenches
   - 4.5 Finishing drives
   - 4.6 Field position, turnovers, hidden yards
   - 4.7 Special teams and kicking
   - 4.8 Matchups and scheme fits
   - 4.9 Personnel and availability
   - 4.10 Coaching
   - 4.11 Game script
   - 4.12 Situational and scheduling
   - 4.13 Weather and environment
   - 4.14 Rules, clock, and officiating
   - 4.15 Market structure and derivative pricing
   - 4.16 Regression, sample size, and priors
   - 4.17 Season-phase angles (Weeks 0–3, conference play, November, CCG/bowls/CFP)
   - 4.18 Angles people miss
5. [Market-specific checklists](#5-market-specific-checklists)
   - 5.1 Full-game total
   - 5.2 Team total
   - 5.3 First-half spread
6. [What not to lean on](#6-what-not-to-lean-on)
7. [The repeatable weekly process](#7-the-repeatable-weekly-process)
8. [Per-game research template](#8-per-game-research-template)
9. [Turning research into a lean without a score model](#9-turning-research-into-a-lean-without-a-score-model)
10. [Logging, review, and angle validation](#10-logging-review-and-angle-validation)
11. [Reference: thresholds, definitions, stabilization](#11-reference-thresholds-definitions-stabilization)

---

## 1. Operating principles

1. **Points = possessions × points per possession.** Every total angle is ultimately a claim about one of those two terms (or about variance around them). Force yourself to say which one an angle moves.
2. **Opponent-adjust and garbage-time-filter everything.** Raw CFB stats are polluted by FCS games, 50-point blowouts, and schedule gaps between G5 and P4. If a number isn't adjusted, treat it as a hint, not evidence.
3. **The market already knows the obvious.** Tempo brands ("Air Raid = over"), name-brand defenses, and last week's box score are priced by Sunday night. Your edge comes from (a) things that are hard to quantify (scheme fit, OL continuity, backup QB quality, coach tendencies), (b) information timing (weather, availability, targeting carryovers), and (c) derivative markets that lag the main line.
4. **Range thinking, not point estimates.** You are producing bands ("this game lives 52–60") and asking whether the posted number sits outside the band. A number inside your band is a pass, regardless of how good the story is.
5. **Separate "what I know" from "what I believe."** Each game sheet should tag every input as *fact* (confirmed availability, forecast), *measured* (adjusted efficiency), or *judgment* (scheme fit, motivation). Judgment inputs cap your confidence grade.
6. **Kill criteria before thesis.** Write down what would make you drop the play *before* you fall in love with it (e.g., "if the wind forecast drops below 12 mph, no play").
7. **Grade the process by closing line value (CLV) and by angle, not by win/loss over a weekend.** Variance in CFB totals is enormous; a season of results tells you little without CLV.

---

## 2. What each market actually prices

### Full-game total
- The sum of both teams' points **including overtime**.
- Driven by: combined possessions, both offenses' efficiency vs. the opposing defense, explosiveness, finishing, turnovers (roughly neutral in expectation but variance-increasing), weather, and late-game script (hurry-up vs. kneel-downs).
- Variance is highest of the three markets. Extreme explosiveness on either side widens the distribution even when the mean is unchanged, which matters when the posted number sits near a scoring cluster.

### Team total
- One team's points, **including overtime**.
- Isolates *one offense vs. one defense* plus that team's share of possessions. The opponent's pace still matters: a slow opponent caps your team's possessions even if your team plays fast.
- Heavily game-script dependent: big favorites pull starters and run clock; underdogs pile up garbage-time points against soft coverage only if they can throw.
- Priced off the main spread and total (see 4.15), posted later, with lower limits. That lag is the primary source of edge.

### First-half spread
- Margin at halftime. **No overtime, no second-half garbage time, no bench emptying.**
- A purer test of starting-lineup quality than the full-game spread. That's why 1H spreads for big favorites run above half the full number (see 4.15).
- Driven by: scripted opening drives, starting QB and OL quality, fresh-defense efficiency, early-game turnover variance, end-of-half management, first-half-only suspensions (targeting carryover), and weather that changes during the game.
- Halftime adjustments, depth, and conditioning matter far less here than in the second half; conversely, early-game execution and preparation matter more.

---

## 3. Data sources

Verify pricing and availability each season; these move.

| Need | Sources |
|---|---|
| Play-by-play, drives, advanced box scores, betting lines, weather fields | collegefootballdata.com (CFBD API; free tier), cfbfastR (R), Game on Paper |
| Opponent-adjusted ratings | Bill Connelly's SP+ (ESPN+), FEI (Brian Fremeau), Massey composite (masseyratings.com) for a consensus of ~100 systems |
| Line/trench/havoc/finishing stats | Connelly's weekly advanced stats, CFBD advanced metrics, Game on Paper |
| Grades, pressure rate, pass-block/run-block win rates, missed tackles, drops, coverage grades | PFF (paid) |
| Returning production, recruiting/talent composite, depth charts, transfer tracking | 247Sports, On3, Connelly's returning-production tables |
| Tempo and pace splits | CFBD (seconds per play by game state), TeamRankings (plays per game), your own PBP pull |
| Availability | Conference availability reports (Big Ten, SEC, ACC, Big 12 all now publish; cadence differs), team-released depth charts, beat writers, coach pressers |
| Suspensions / targeting carryover | Box scores (targeting in 2nd half = sits next 1H), beat writers, conference announcements |
| Weather | NWS point forecast for stadium coordinates, Windy/Open-Meteo for hourly wind and gusts, stadium orientation via satellite view |
| Market | Circa, Pinnacle, Bookmaker for openers and sharp numbers; DraftKings/FanDuel/ESPN Bet for derivatives; an odds screen (Unabated, OddsJam, Action, DonBest) for line history |
| Officiating crews | Compile your own from CFBD penalty data by game and crew assignments where published |

Build your own tables rather than trusting a single site's "advanced stats" page. You need to control garbage-time filtering, FCS exclusion, and the explosive-play definition.

---

## 4. The angle library

Each angle lists: what to measure, why it moves the number, which markets it affects most, and traps.

### 4.1 Pace, tempo, possessions

**Why first:** possessions are the single largest lever on totals and the one most often mispriced in non-marquee games.

**Measure:**
- **Seconds per play** (offense), split by game state: leading by 8+, within 8, trailing by 8+. Many "fast" teams are only fast when trailing.
- **Plays per game**, offense and defense, opponent-adjusted (your plays are partly a function of how fast the other team gives the ball back).
- **Possessions per game** (exclude end-of-half kneel drives). FBS averages have run roughly 11–13 per team; recompute the current-season baseline every year because clock rules changed (see 4.14).
- **Plays per possession** and **time per possession** — a methodical team can be "slow" with few possessions but many plays.
- **Three-and-out rate** (both sides). High 3-and-out rates increase possessions and shorten time of each one.
- **Run/pass rate by down and game state.** Incompletions stop the clock; heavy pass offenses generate more plays per minute even at the same huddle tempo.
- **Huddle vs. no-huddle percentage**, and whether tempo is used as a weapon (snap within 15 seconds) or just a pace of play.
- **Sack and penalty rates** — both extend drive time and reduce plays per minute.
- **Opponent's defensive substitution/tempo interaction:** some defenses deliberately slow the game (late subs, injuries, calls for review).

**Combining two teams:** Possessions are almost equal for both sides, so project one number for the game. Average both teams' adjusted possessions per game, then adjust toward the slower team if it's the favorite (it will control the clock when ahead) and toward the faster team if it's the favorite and known to keep the pedal down. Then overlay expected competitiveness: close games produce more late hurry-up and clock stoppages; lopsided games produce clock-killing from one side and sometimes hurry-up from the other.

**Markets:** Full total (dominant). Team total (your team's possessions depend on *both* tempos). 1H spread (fewer possessions = fewer chances for the better team to separate; tempo teams build leads early while defenses are fresh, but also expose themselves to short-field variance).

**Traps:**
- Time of possession is a tempo artifact, not a quality signal.
- "Plays per game" for a team that played two FCS/weak opponents early is inflated by scoring fast and getting the ball back.
- Tempo often changes with QB injury (backup = more huddle, more runs) or with a new OC midseason.

### 4.2 Efficiency

**Measure (all opponent-adjusted, garbage time removed):**
- **Success rate** (down-and-distance adjusted) for offense and defense, split rush/pass and standard downs/passing downs.
- **EPA per play**, split rush/pass, early downs vs. third down.
- **Yards per play** as a sanity check only; it blends efficiency and explosiveness.
- **Early-down success** drives third-down distance. Teams with high early-down success face short third downs and sustain drives; this is the real skill behind third-down conversion rate.
- **Passing-downs success** (2nd-and-8+, 3rd/4th-and-5+): defenses that excel here get off the field; offenses that excel here have a QB and protection that can rescue drives.
- **Rushing efficiency vs. light boxes / heavy boxes** where available (PFF). Teams that only run well against light boxes get shut down by committed run defenses.
- **QB-specific efficiency**: completion % over expected, EPA under pressure vs. clean pocket, sack rate (QB-driven as much as OL-driven), scramble rate and yards.

**Matchup grid:** Build a 2×2 — Team A pass O vs Team B pass D; Team A rush O vs Team B rush D; and the reverse. Rank each quadrant as strong edge / even / weak. Totals leans need multiple quadrants pointing the same direction; team-total leans need the two quadrants on that side.

**Markets:** All three. For 1H spread, weight starting-lineup efficiency more heavily and discount depth-driven second-half stats.

**Traps:** Raw points per game and total yards. Third-down % and red-zone % without the early-down context. Any stat that includes FCS games or garbage time.

### 4.3 Explosiveness and variance

**Measure:**
- **Explosive play rate** (pick one definition — 10+ rush / 20+ pass, or 15+/20+ — and use it consistently) for offense and allowed by defense.
- **Yards per successful play / IsoPPP** — how big are the successful plays?
- **Explosive-play dependency:** share of points scored on drives containing an explosive play. High dependency = boom/bust offense.
- **Defensive structure:** two-high-safety-heavy defenses allow efficiency but suppress explosives; single-high/pressure-heavy defenses do the reverse.
- **Missed tackle rate** (PFF) and YAC allowed — the leading indicator of explosive passes allowed.
- **Secondary injuries and depth:** a CB2 or safety injury is the most reliable path to a spike in explosives allowed.
- **QB arm talent and deep-ball rate** vs. opponent's deep-ball coverage; WR separation and contested-catch profile.

**Why it matters beyond the mean:** Explosiveness increases the *variance* of outcomes. For a total, a wider distribution shifts probability mass away from the center. If the market number sits at a dense scoring cluster, variance favors the side with more room; if your mean estimate is close to the number, high variance alone is not a reason to play. For 1H spreads, explosive underdogs are live for early leads; explosive favorites separate before halftime.

**Markets:** Full total (mean and variance), team total (an explosive offense is less dependent on possessions), 1H spread (early-game variance).

**Traps:** Explosive rates stabilize slowly; a few 70-yard plays swing the season figure. Blend with prior-season and talent priors longer than you do for success rate.

### 4.4 Trenches

**Measure:**
- **Line yards** (OL credit for rushing), **stuff rate** (runs stopped at/behind line), **opportunity rate** (% of carries reaching 4+ yards), **power success** (3rd/4th-and-≤2 conversions by run).
- **Havoc rate** (TFL + pass breakups + forced fumbles per play), split DL / LB / DB.
- **Pressure rate and sack rate**, allowed and generated, adjusted for QB time to throw (a quick-game offense neutralizes a great pass rush; a long-developing offense exposes a mediocre OL).
- **Pass-block / run-block / pass-rush win rates** (PFF).
- **OL continuity:** career starts, consecutive games with the same five, position shuffles after injuries. A single interior OL loss often matters more than a RB1 loss.
- **DL rotation depth:** snap share of the top 4 DL. Thin DL rotations fade in heat and against tempo — a second-half effect, so it matters more for the full game than for 1H.
- **Size/weight mismatches** in G5-vs-P4 and FCS-vs-FBS games; talent composite by unit.
- **Returning starters on OL** (early season) — one of the stronger preseason predictors of offensive stability.

**Why:** Trench control determines whether an offense can run on standard downs (sustaining drives, bleeding clock → fewer possessions but higher points per possession) and whether a QB has time to produce explosives.

**Markets:** Team total (offense's floor), 1H spread (OL continuity shows up immediately in scripted drives; pass-rush mismatches produce early turnovers), full total (dominant run game lowers possessions; dominant pass rush lowers points per possession).

**Traps:** Sack totals as a pass-rush measure (QB-dependent). Rushing yards per game (tempo and game-script dependent).

### 4.5 Finishing drives

**Measure:**
- **Points per scoring opportunity** (drives reaching the opponent's 40) for offense and allowed by defense. This is the cleanest finishing metric; red-zone % is a noisier subset.
- **Red-zone TD rate** vs. FG rate, and **goal-to-go efficiency**; red-zone rushing success, jumbo/TE usage, QB run threat near the goal line (designed QB runs add a blocker and matter most in compressed fields).
- **Kicker quality and range** (see 4.7); a bad kicker turns scoring opportunities into zeros.
- **Fourth-down aggressiveness by coach** in opponent territory: aggressive coaches convert FG opportunities into TD attempts (and occasionally zeros), raising both mean and variance of points per opportunity.
- **Turnover rate inside the 40** (fumble-prone RBs, interception-prone QBs in tight windows).

**Markets:** Team total (this is where one team's drives become 3s vs. 7s vs. 0s), full total, 1H spread (early red-zone failures are how favorites fail to cover halves).

**Traps:** Red-zone % over small samples. Treat finishing as moderately persistent (skill in QB/OL/scheme) but regress hard early in the season.

### 4.6 Field position, turnovers, hidden yards

**Measure:**
- **Average starting field position** (offense and defense), and the drivers: net punting, kick return/coverage, touchback rate, turnovers, penalties on kicks.
- **Turnover luck:** compare actual turnover margin to expected (fumble recoveries regress to ~50%; interceptions regress toward a share of pass breakups). Teams with a large positive gap are due to give points back; large negative gaps are due to get them back.
- **Pressure-driven turnovers** are more repeatable than fumble recoveries; a high-pressure defense facing an interception-prone QB is a legitimate turnover angle. Everything else is noise.
- **Penalty rate** (offense pre-snap, defensive PI/holding that extends drives), with a road/noise split.
- **Defensive and special-teams touchdowns:** unpredictable, but high-havoc defenses facing turnover-prone offenses have a real (small) edge in non-offensive scoring, which pushes totals and 1H margins.

**Effect on totals:** Turnovers are roughly neutral for the *mean* total (they end one drive but give the other side a short field) but increase variance. They are strongly directional for team totals and 1H spreads.

**Markets:** 1H spread (field position compounds quickly in a 30-minute window), team total, full total (variance).

### 4.7 Special teams and kicking

- **Field goal range and accuracy** from 40+ and 50+. A kicker with a 45-yard limit changes the coach's 4th-down map and shrinks the scoring zone; the market rarely prices this in non-marquee games.
- **Extra point reliability** (yes, it matters in G5).
- **Punter net average and pin-deep rate** → opponent starting field position.
- **Kickoff touchbacks vs. returns**; coverage unit quality; return specialists capable of a house call.
- **Blocked-kick rates** (both ways) as a proxy for special-teams coaching.
- **Onside/fake tendencies** of the coach (variance, late-game script).

**Markets:** Team total and 1H spread most directly.

### 4.8 Matchups and scheme fits

These are the hardest for the market to price and where film and beat-writer knowledge pay off.

- **Pass offense vs. coverage type:** man-heavy defenses vs. receivers who win on separation; zone-heavy defenses vs. QBs who struggle reading post-snap rotation; Cover-2/quarters vs. teams that live on seams and posts.
- **Pressure packages vs. protection:** blitz-heavy defenses vs. offenses with poor hot-route answers and immobile QBs; conversely, blitz-heavy defenses vs. RPO/quick-game teams get burned.
- **RPO / zone-read / QB run vs. edge discipline:** defenses with undisciplined edges and poor option responsibilities leak explosives; disciplined, two-gapping fronts suffocate them.
- **Power/gap run game vs. light boxes** (and vs. 3-3-5 / 4-2-5 structures that prioritize space over size).
- **Tempo vs. depth:** fast offenses against thin DL rotations and defenses that substitute heavily; this is a second-half effect (full total, not 1H).
- **Option/triple option (service academies and a few others):** possessions collapse (often 8–9 per team), the opponent's prep week matters, cut-blocking and assignment discipline dominate, and the opponent's offense gets fewer chances. Totals are structurally lower; the market knows, so look for cases where the *opponent* can still score explosively on few possessions, or where the academy's defense is overmatched.
- **Mobile QB vs. defenses with poor rush-lane discipline** (scramble yards are a hidden efficiency source on passing downs).
- **Tight end usage vs. linebackers in coverage;** slot receivers vs. nickel quality.
- **Coordinator familiarity:** a coordinator facing his former team or former scheme (knows calls, tendencies, personnel); former assistants on the other staff.
- **Experience vs. inexperience at QB** against disguised-coverage defenses: young QBs vs. heavy disguise/sim pressure is a repeatable negative.
- **Crowd noise vs. communication-dependent offenses:** road teams with pre-snap-heavy, check-at-the-line offenses in loud night environments see more procedure penalties and slower tempo. Helmet communication (allowed in FBS since 2024) reduces but does not eliminate this.

**Markets:** All three. For team totals, this is the core of the work.

### 4.9 Personnel and availability

- **Starting QB status** is the single most important fact in CFB handicapping. Drop-offs to backups are much larger than in the NFL, affect tempo and scheme, and are often confirmed late.
- **Backup QB evaluation:** recruiting profile, prior snaps and efficiency, mobility, spring/fall camp reports, whether the offense simplifies (fewer plays per minute, more runs, lower explosiveness). A dual-threat backup in an RPO offense may preserve more than a pocket passer would.
- **Non-QB injuries ranked by impact:** interior OL and LT; CB1/CB2 and safeties (explosives allowed); edge rusher; WR1 (target concentration matters: offenses with one dominant target suffer more); RB1 (usually lowest impact unless the offense is RB-centric or depth is poor).
- **Cumulative attrition:** count starters missing per unit; depth charts with three or more new starters in the secondary or OL are a flag.
- **Suspensions and targeting carryover:** a player ejected for targeting in the second half of the previous game sits the **first half** of the next game. This is a direct 1H-spread angle that is routinely underpriced because it's buried in box scores and does not appear in many injury feeds.
- **Availability reports:** power conferences publish them; learn each conference's cadence (some midweek plus pregame, some only pregame). Non-conference games across conferences may have asymmetrical disclosure.
- **Transfer portal / opt-outs:** bowl season (NFL opt-outs, portal departures) and the spring/summer portal (roster cohesion early in the season). Portal-built rosters often take several games to gel on OL and in the secondary.
- **Position changes and emergency starters** flagged in depth charts (e.g., a walk-on OL starting).
- **Illness/weather-related travel issues** reported by beat writers the day before.

**Markets:** All three. Timing matters most for team totals and 1H spreads where the derivative markets are slower to react.

### 4.10 Coaching

- **Offensive identity and play-calling:** pass rate over expected (PROE) by game state, early-down pass rate, tempo philosophy, screen/RPO rate, deep-shot rate.
- **Fourth-down aggressiveness** (go rate in 4th-and-short by field zone), and whether it changes with a lead.
- **Lead management:** who sits on leads (run-heavy, bleed clock, pull starters early) vs. who keeps scoring. This is a *team total* and *full total* angle for big favorites and shows up in second-half splits — look at behavior, not just points.
- **End-of-half behavior:** does the coach attack with 1:30 and two timeouts, or kneel? Does he use the "double dip" (score before half, receive to open the 2nd half)? Directly a 1H-spread angle.
- **Timeout and clock management competence** (late-half sequences, 2-minute offense quality).
- **Scripted openers:** some staffs script the first 10–15 plays and consistently start fast; others are notorious slow starters. Measure first-quarter EPA and first-drive success rate, but treat with caution (noisy); use it as a tiebreaker, not a thesis.
- **Halftime adjustment reputation:** largely narrative; where it's real it shows as sustained second-half efficiency improvements across seasons. Irrelevant to 1H spreads by definition.
- **New coordinators / new systems:** early-season efficiency often lags installed talent; tempo may be slower than last year's brand. Research the coordinator's history at previous stops rather than the team's last-year numbers.
- **Interim coaches:** the "interim bounce" is noisy; the relevant change is often a new play-caller and a tempo or scheme shift.
- **Hot-seat and lame-duck dynamics** (late-season effort, roster disengagement) — real but hard to measure; use beat reporting.
- **Coach's bye-week track record and prep-heavy games** (option opponents, rivalry) — minor.
- **Discipline:** penalty rate under a given staff is fairly persistent.

**Markets:** Team total (lead management, aggressiveness), 1H spread (openers, end-of-half management), full total (tempo philosophy, 4th-down approach).

### 4.11 Game script

Game script is the bridge between the spread and the total; you cannot handicap a team total or a 1H spread without a view of how the game unfolds.

- **Expected margin band** from the market spread. Large favorites: more second-half clock-killing, more backups, possibly more garbage-time points for the dog. Close games: more plays, more late hurry-up, more field goal attempts, more variance from end-of-game possessions.
- **Trailing team's passing ability:** garbage-time points require a functional passing game against soft coverage. A run-first underdog that falls behind usually does *not* back-door a team total.
- **Favorite's bench behavior:** who empties the bench at +28 in the 3rd quarter vs. +35 with 5:00 left? Build a list by coach.
- **Trailing team's tempo when behind:** some teams go no-huddle and generate plays; others stay methodical and the game dies.
- **Expected lead change frequency:** games projected close produce more "answer" drives and more aggressive play-calling.
- **Possession parity:** in blowouts, the favorite's long drives + the dog's three-and-outs concentrate possessions and reduce the total; in shootouts, quick scores from both sides inflate possessions.
- **Late-game dynamics:** kneel-downs, prevent defense, end-of-game FGs, two-point conversions (standard from 2nd OT, mandatory alternating 2-pt tries from 3rd OT) — small but real for numbers near the margin.
- **1H script specifically:** who receives (most teams defer; the team receiving the opening kickoff may get one extra 1H possession), scripted opener quality, how the half ends (two-minute drill competence, conservatism with the ball at midfield).

### 4.12 Situational and scheduling

Use as modifiers, never as a primary thesis.

- **Rest:** bye week (extra prep is most valuable before option teams and unusual schemes; extra rest helps thin rosters), short weeks (Tuesday–Friday games after a Saturday), consecutive road games.
- **Travel:** cross-country and multi-time-zone trips (realignment has expanded these for Big Ten and ACC schools), early-kickoff body-clock effects for West Coast teams playing noon ET (evidence is mixed; small modifier), the Hawaii trip and the game *after* it.
- **Altitude:** Air Force, Wyoming, Colorado State, Colorado, New Mexico, Utah, BYU. Longer kicks, thinner visitor rotations late — second-half effect (full total), negligible for 1H.
- **Heat and humidity:** September in the South and Texas; afternoon kickoffs; depth and rotation matter more in the second half. Fresh-defense first halves can be *more* efficient than the full-game numbers suggest.
- **Lookahead / letdown / sandwich spots:** real but small; the market prices the famous ones. Only use where there's a concrete mechanism (e.g., short week after an emotional night game and a road trip).
- **Rivalry games:** familiarity, intensity, and often conservative play-calling. Don't treat "rivalry = under" as a rule; check how the specific staffs have called these games.
- **Conference championship games, CFP first round (on-campus, December weather in the north), neutral-site bowls:** see 4.17.
- **Midweek MACtion and G5 weeknight games:** smaller crowds, odd prep weeks, thinner markets, lower limits — more inefficiency but also more roster chaos.
- **Homecoming / senior day / coach milestones:** no measurable effect; ignore.
- **Kickoff time and crowd:** night games at elite venues produce more procedure penalties and communication issues for road offenses.

### 4.13 Weather and environment

- **Wind is the only weather variable that reliably moves totals.** Sustained 12–15 mph starts to matter; 20+ mph is significant; gusts matter as much as sustained speed; direction relative to field orientation matters (crosswind vs. end-to-end). It depresses deep passing, FG range, punting, and kickoff touchbacks (which increases returns and variance in field position). It also pushes play-calling toward the run, which lowers plays per minute — a double hit on the total.
- **Rain:** overrated by the public for passing volume; matters for footing (more explosives from slips on both sides), ball security, and kicking. Heavy, sustained rain with wind is the combination that matters.
- **Cold:** minor on its own above ~25°F; matters for kicking and ball handling at extremes; often bundled with wind in November.
- **Snow:** rare; footing and visibility; cornerbacks slip more than receivers; FG range shrinks.
- **Heat/humidity:** second-half fatigue, cramping, rotation depth; see 4.12.
- **Lightning delays:** stop rhythm and extend the game clock but not possessions; relevant for live situations, not pregame.
- **Domes and retractable roofs:** check roof status for the game; neutral-site bowl stadiums vary.
- **Field surface:** turf vs. grass is a minor pace/footing input; wet grass is the condition that matters.
- **Stadium orientation and enclosure:** open-ended stadiums at coastal or plains sites channel wind; closed bowls dampen it. Learn the problem venues in advance.
- **Forecast timing:** wind forecasts are usable inside ~48–72 hours and reliable inside ~24; the market typically prices wind by Friday night. Your edge is acting on a high-confidence forecast *before* the market (Thursday for weekend games, or on the open for midweek games) and avoiding overpriced "weather unders" on Saturday morning when the move is already in.

**Markets:** Full total (dominant), team total (an air-dependent offense in wind), 1H spread (if conditions change during the game — e.g., front arriving at halftime — the first half plays under different weather than the full game).

### 4.14 Rules, clock, and officiating

Rules change often; re-verify each August. Recent changes that matter for pace and scoring:

- **2023 clock rule:** the clock no longer stops on first downs outside the final two minutes of each half; no untimed downs after defensive penalties at the end of the 1st and 3rd quarters; consecutive timeouts restricted. Net effect was a meaningful reduction in plays per game. Any historical baseline that includes pre-2023 seasons overstates plays and possessions.
- **2024:** two-minute timeout at the end of each half (stops the clock at 2:00), coach-to-player helmet communication, sideline tablets. Minor pace effects; the two-minute stoppage adds a small end-of-half scoring opportunity.
- **2025:** injury-timeout handling in the final two minutes (teams charged a timeout for certain injury stoppages after the ball is spotted) to reduce faked injuries; overtime timeout limitations. Minor.
- **Overtime (since 2021):** two-point conversions required from the 2nd OT; alternating two-point tries from the 3rd OT. OT **counts for full-game totals, spreads, and team totals, not for 1H markets.** Expected OT points are capped lower than they used to be.
- **Kickoffs:** touchbacks and fair catches inside the 25 come out to the 25; coverage/return quality matters less than it did.
- **Targeting:** ejection; second-half ejections carry a first-half suspension into the next game.
- **Officiating crews:** penalty rates and pace vary by crew and conference; defensive holding/PI frequency extends drives; frequent reviews slow the game. Build a crew table if you can get assignments; treat as a Tier-3 modifier.

### 4.15 Market structure and derivative pricing

- **Opening sequence:** look-ahead lines and early openers appear Sunday at a few books; derivative markets (team totals, 1H, quarters) often post midweek and are generated from the main spread and total with house adjustments. Derivatives lag main-market moves, have lower limits, and are where fundamental edges most often survive.
- **Team total derivation:** with total *T* and favorite spread *S* (positive number of points), the implied favorite team total ≈ (T + S)/2 and the dog's ≈ (T − S)/2, before juice shading. Compare the posted team totals to this; deviations tell you how the book views the distribution of points between teams (e.g., shading the dog's total up because it expects garbage-time scoring).
- **First-half spread pricing:** 1H spreads typically run **above** half of the full-game spread — commonly ~55–60% of the full number, rising with the size of the spread — because favorites accumulate margin disproportionately in the first half and give it back to backups and clock-killing later. Measure the ratio at your books and track games where your fundamentals say the favorite's margin is *more* or *less* front-loaded than the standard ratio. First-half totals typically run a bit under half of the full total (~46–49%); you'll use that when checking 1H spread leans for consistency.
- **Key numbers:** CFB spreads cluster on 3, 7, 10, 14, 17, 21 but with less density than the NFL; 1H spreads cluster on 3 and 7. Totals have weak key numbers; don't pay for half points on totals the way you would on NFL spreads, but do avoid buying across nothing.
- **Line movement reading:** distinguish informational moves (injury/weather news) from flow moves. A total moving against your lean on confirmed news is a kill criterion; a flow move without news is not.
- **Limits and timing:** lower limits on team totals and 1H markets mean earlier price discovery from sharp action; if your number is still available on Friday in a mainstream game, ask why.
- **Closing line value** is your primary performance metric for each market separately.
- **Correlation:** team totals and 1H spreads are correlated with the main markets; if you bet multiple derivatives in one game, you're concentrating risk, not diversifying.

### 4.16 Regression, sample size, and priors

- **Priors (preseason):** SP+/FEI preseason projections, returning production (QB and OL weighted), recruiting/talent composite, transfer portal net gains/losses by unit, coaching continuity. Use them heavily through Week 3–4 and keep a nontrivial weight on them all season for noisy stats.
- **Blending guideline:** Weeks 0–2 ≈ 70–80% prior; Weeks 3–5 ≈ 50–60% prior; Weeks 6–8 ≈ 30–40%; after Week 8 ≈ 15–25% for efficiency, higher for explosiveness and turnovers. Adjust by stat stability (see Section 11).
- **Stabilization order (fastest to slowest):** tempo/seconds per play → success rate → EPA/play → finishing → explosive rate → third-down % → red-zone % → turnover margin (never fully).
- **Regression flags to put on every sheet:** turnover margin vs. expected; close-game record (one-score W/L); red-zone and third-down outliers; FG% outliers; "points allowed" built on a soft schedule; second-order wins vs. actual wins.
- **Opponent adjustment:** always, and recompute weekly. A defense that looked elite against three bad offenses isn't elite yet.
- **Garbage time:** define it (quarter-dependent margin thresholds or a win-probability cutoff of ~95–98%) and apply it consistently in your own tables. Note that the *market* often doesn't fully strip garbage time, which is a source of overreaction after blowouts.
- **FCS games:** exclude from efficiency; use only for health/depth information.

### 4.17 Season-phase angles

**Weeks 0–3**
- Information is thin; priors dominate. The best edges are *structural*: QB competitions unresolved, new OL combinations, new coordinators with a known tempo history, P4-vs-G5 trench gaps, and heat.
- Totals in Week 1 are often set off brand and last season's stats; new-system offenses tend to underperform their brand early.
- Overreaction to Week 1 is the most reliable early-season market inefficiency to fade in Week 2–3 (in both directions).

**Conference play (Weeks 4–10)**
- Current-season adjusted stats carry most of the weight. Scheme-fit and availability become the differentiators. Midweek G5 games and cross-division matchups are where derivative markets are sloppiest.

**November**
- Weather (wind, cold) enters; depth and attrition compound; eliminated teams and lame-duck staffs show effort variance; rivalry week play-calling conservatism. Secondary injuries by November are the most common hidden explosives driver.

**Conference championships / CFP / bowls**
- Opt-outs and portal departures (verify unit by unit; a missing OL starter matters more than a missing RB), interim coaches, three-to-five-week layoffs (defense rust and offense rust are both real; the net effect is more variance), on-campus CFP first-round games in December weather, neutral-site crowds, and motivation asymmetry (hard to measure; use roster availability as the proxy rather than narrative).
- Treat bowl totals as higher-variance and require a larger edge before playing.

### 4.18 Angles people miss

A checklist of items that rarely appear in mainstream handicapping writeups:

1. **Targeting carryover suspensions** (second-half ejection → first-half suspension) — a direct 1H-spread input.
2. **Kicker range** and its effect on 4th-down decisions and finishing.
3. **OL continuity** (same five, career starts) over OL "talent."
4. **Secondary depth** as the primary driver of explosives allowed late in the season.
5. **Backup QB scheme fit and tempo change**, not just "backup = bad."
6. **Pace by game state**, not average pace. The team that controls the game controls the tempo.
7. **Three-and-out rate** as a possession generator on both sides.
8. **Coach lead-management behavior** (bench emptying, run-heavy with lead) for team totals.
9. **End-of-half tendencies** (attack vs. kneel; double dip) for 1H spreads.
10. **Stadium wind geometry** (orientation and enclosure), not just the forecast number.
11. **Weather changing mid-game** (front timing) splitting 1H vs. 2H conditions.
12. **Overtime inclusion** for full-game and team totals vs. exclusion for 1H.
13. **Derivative pricing ratios** (1H ≈ 55–60% of spread; team totals from (T ± S)/2) as a baseline to detect house shading and lag.
14. **Availability report cadence by conference**, including asymmetry in non-conference games.
15. **Portal roster cohesion** in September; opt-out depth charts in December.
16. **Coordinator familiarity** with the opponent's scheme or roster.
17. **Procedure penalties for communication-heavy road offenses** in loud night venues.
18. **Officiating crew penalty rates** as a drive-extension modifier.
19. **Clock-rule era mismatches** in your historical baselines (pre-2023 data overstates plays).
20. **Turnover expectation vs. actual** as a regression flag for defenses "allowing" few points.
21. **Points per scoring opportunity allowed**, not just points allowed.
22. **Deferral and opening-possession patterns** for 1H possession counts.
23. **Altitude and heat as second-half-only effects** (which means they influence full-game markets more than 1H).
24. **DL rotation snap shares** as the depth metric that interacts with tempo.
25. **Target concentration** (how much of the passing offense runs through one receiver) when evaluating WR injuries.
26. **Fourth-down go rates by field zone** as a variance and finishing input.
27. **Spring/summer portal departures at OL and DB** that don't show in "returning production" headlines.
28. **Prior-season second-order wins** vs. actual wins as a preseason regression flag.
29. **Game-on-campus December CFP weather** and northern-venue wind history.
30. **Non-offensive scoring potential** (havoc defense vs. turnover-prone offense) for 1H spreads and totals.

---

## 5. Market-specific checklists

### 5.1 Full-game total

**Possessions**
- [ ] Both teams' adjusted possessions per game and seconds per play by game state
- [ ] Projected possession band for this game (slow/fast control, competitiveness)
- [ ] Three-and-out rates both sides; expected run/pass mix in likely script

**Points per possession**
- [ ] Efficiency grid (4 quadrants), opponent-adjusted
- [ ] Finishing (points per scoring opportunity) both offenses vs. both defenses
- [ ] Explosive rates both ways; secondary health; missed-tackle profile
- [ ] Kicker quality both sides

**Modifiers**
- [ ] Weather (wind ≥ 12–15 mph sustained or significant gusts), stadium geometry, roof status
- [ ] QB/OL/DB availability; targeting carryovers
- [ ] Coach tempo philosophy, 4th-down aggressiveness, lead management
- [ ] Rest/travel/heat/altitude (second-half effects)
- [ ] OT inclusion when the number is near your band edge
- [ ] Regression flags (turnover luck, soft-schedule points allowed)

**Market**
- [ ] Open, current, direction, and whether moves are informational
- [ ] Your band vs. the number; does the number sit outside the band by enough?
- [ ] Kill criteria written down

### 5.2 Team total

- [ ] Derived team total from (T ± S)/2 vs. posted; note shading
- [ ] This offense vs. this defense: the two relevant quadrants of the grid
- [ ] This team's possessions given *both* tempos and expected script
- [ ] Finishing: points per opportunity for this offense vs. this defense; kicker
- [ ] Explosiveness: does this offense need many possessions or can it score in few?
- [ ] Game script: if favored, does the coach keep scoring or sit? If the dog, can it throw in garbage time? Does the favorite's defense empty the bench?
- [ ] Availability: QB, OL, WR1 (target concentration), opponent's CBs/safeties
- [ ] Weather vs. this offense's air dependency
- [ ] Opponent's defensive style (bend-don't-break vs. havoc) and points allowed per opportunity
- [ ] OT inclusion
- [ ] Market lag: did the main total/spread move after the team total posted?

### 5.3 First-half spread

- [ ] 1H spread ratio vs. full spread (compare to your book's typical 55–60%); is this game more or less front-loaded than standard?
- [ ] Starting-lineup quality gap (talent composite, adjusted efficiency with starters)
- [ ] First-half suspensions (targeting carryover), late scratches, availability report timing
- [ ] Scripted-opener history and first-drive success rates (tiebreaker weight only)
- [ ] OL continuity and pass-rush mismatch (early turnovers and early stalls)
- [ ] Explosive capability of the underdog (can it steal an early lead?)
- [ ] End-of-half management by both coaches; two-minute offense quality; deferral habits
- [ ] Early-game variance sources: turnover-prone QB vs. high-pressure defense; return game
- [ ] Weather at kickoff vs. later (front timing)
- [ ] Heat/altitude/depth: these favor the *full-game* favorite more than the 1H favorite; discount them here
- [ ] Favorite's historical first-half margin share (front-loaded vs. back-loaded) — use several seasons under the same staff
- [ ] Underdog's "hang around" profile: methodical run game + sound defense = low 1H variance (favors the dog on inflated 1H numbers); boom/bust = high variance
- [ ] Key numbers for 1H (3, 7); buy/sell decisions

---

## 6. What not to lean on

**Stats that mislead**
- Raw points per game and points allowed per game (schedule and tempo).
- Total yards and yards per game (tempo).
- Time of possession (tempo artifact).
- Third-down conversion % as a standalone skill (it's early-down success wearing a costume).
- Red-zone % in small samples.
- Turnover margin as a skill (outside of pressure-rate-driven interceptions).
- Sack totals as pass-rush quality (QB and scheme dependent).
- Any season stat that includes FCS games or garbage time.
- Historical baselines that mix pre- and post-2023 clock rules.
- Preseason polls and brand names as strength proxies.

**Trends and narratives**
- Over/under records ("they're 7–1 to the over"); ATS records; coach ATS records; "X is 12–3 as a home dog."
- Head-to-head history and last year's score.
- Revenge, "statement game," senior day, homecoming, coach-vs-former-school emotion.
- "Second-half team" and "halftime adjustments" without multi-season efficiency evidence.
- "Fade the public" and betting-percentage splits; public money is not a signal in CFB derivatives.
- Conference stereotypes ("Big 12 = shootout," "SEC = defense"); realignment and staff turnover have scrambled these.
- Single-game recency: one 60-point outing against a bad defense or one shutout against a bad offense.
- Hangover after an upset win, "trap games," and "lookahead" without a concrete mechanism.
- Rain as an automatic under; cold as an automatic under. (Wind is the one that counts.)
- Rivalry = under as a rule.
- "They need this game" / bowl eligibility motivation.

**Market behaviors to avoid**
- Chasing Saturday-morning weather moves that are already priced.
- Paying for half points on totals as if they were NFL key numbers.
- Betting multiple correlated derivatives in one game as if they're independent.
- Treating steam without news as information for a fundamental lean.
- Grading your angles by weekend W/L instead of CLV and sample size.

**Modeling behaviors to avoid**
- Point estimates instead of bands.
- Unadjusted stats at any point in the season.
- Dropping priors too early (Weeks 1–4) or holding them too long for fast-stabilizing stats (tempo, success rate).
- Counting explosives, turnovers, and red zone at full weight before they stabilize.
- Ignoring game script when handicapping team totals and 1H spreads.

---

## 7. The repeatable weekly process

The cadence assumes a Saturday-centric slate; shift for midweek games.

### Sunday — close out and open up
1. Grade last week: results, CLV by market, angle tags, and a one-line "what I got right/wrong about the mechanism" per play.
2. Update the data tables: pull new PBP, recompute adjusted efficiency, pace by game state, explosives, finishing, havoc, field position, turnover expectation. Re-blend priors.
3. Capture availability-relevant events from the week: injuries, targeting ejections (second-half ejections → list for 1H suspensions), QB changes, coaching changes, suspensions.
4. Scan openers and look-ahead lines; note any numbers that look off on first principles (possession mismatches, QB uncertainty, obvious trench gaps).
5. Build the weather watch list: venues with open stadiums in windy regions, northern games in November/December, early-season heat games.

### Monday — triage the slate
1. Build the slate sheet: every FBS game with open/current spread and total, implied team totals, tempo for both teams, adjusted efficiency grid, explosive rates, finishing, injury flags, weather flag.
2. Filter to **candidates**: games where (a) the possession projection disagrees with what the total implies, (b) the efficiency grid is lopsided in a way not reflected in the team totals, (c) availability is unsettled or asymmetrically disclosed, (d) weather is potentially material, or (e) there's a 1H structural factor (suspension, slow-starting staff, option prep).
3. Cap the deep-dive list to a manageable number (8–15). Pass on the rest.

### Tuesday–Wednesday — deep dives
1. For each candidate, complete the per-game template (Section 8).
2. Read beat reporting and coach pressers for availability, OL combinations, QB status, scheme notes.
3. Watch condensed film or cut-ups on the two or three scheme-fit questions that matter for the lean.
4. First weather look (5-day): flag games that could become plays or become unplayable.
5. Write the thesis per market and the kill criteria. Assign a confidence grade.

### Thursday — derivative markets
1. Team totals and 1H lines are posted or firm by now. Compare posted to derived values and to your thesis.
2. Place plays where (a) the number is outside your band, (b) the information is likely to move the market against you later (confirmed wind, pending availability news), or (c) the derivative hasn't moved with the main market.
3. Second weather look (48–72 hours): wind and gust confidence; front timing relative to kickoff.

### Friday — availability and final weather
1. Availability reports and final depth charts; adjust or kill plays per the criteria.
2. Final weather check for Saturday games; act on high-confidence wind if not yet priced; stand down on numbers that already moved.
3. Line shop; finalize sizing by confidence grade and market liquidity.

### Saturday — execution and notes
1. Pregame availability (90-minute to 2-hour reports); last chance to kill a 1H play on a late scratch.
2. During games, note mechanisms for later review: did the possession count land in the band? Did the script match? Did the coach behave as expected with a lead? These notes feed Sunday's grading and your coach-behavior tables.

### Monthly / end of season
- Review angle performance by tag with CLV and hit rate; retire angles that don't produce CLV over a meaningful sample; promote angles that do.
- Re-verify rule changes, data definitions, and book pricing ratios.

---

## 8. Per-game research template

Copy this per candidate game.

```
GAME: ______ at ______      KICK: ______ (local time / TV window)   VENUE: ______ (surface, roof, orientation)

MARKET SNAPSHOT
  Spread open/current:          Total open/current:
  Implied TTs: (T+S)/2 = ___   (T−S)/2 = ___   Posted TTs: ___ / ___   Shading notes:
  1H spread posted: ___   Ratio to full: ___%   1H total: ___
  Moves and whether informational:

POSSESSIONS
  Team A sec/play (lead / close / trail):          Team B:
  Adjusted possessions/game A: ___  B: ___  3-and-out rates A: ___ B: ___
  Who controls pace in the likely script:
  Projected possession band for the game: ___–___

EFFICIENCY GRID (opp-adjusted, no garbage time)
  A pass O vs B pass D: ___   A rush O vs B rush D: ___
  B pass O vs A pass D: ___   B rush O vs A rush D: ___
  Early-down success / passing-down success notes:

EXPLOSIVENESS & VARIANCE
  Explosive rate A O / B D:          B O / A D:
  Secondary health, missed tackles, deep-ball profile:
  Variance verdict (wide / normal / tight):

TRENCHES
  Line yards / stuff / opportunity / power: A vs B, B vs A
  Pressure vs protection (time to throw): 
  OL continuity (same five? career starts?):    DL rotation depth:

FINISHING
  Pts per scoring opportunity: A O / B D, B O / A D
  Kickers (range, accuracy):     4th-down aggressiveness:

FIELD POSITION / TURNOVERS / ST
  Starting FP, net punting, returns:
  Turnover expectation vs actual (regression flag?):
  Non-offensive scoring potential:

PERSONNEL / AVAILABILITY (tag each: FACT / LIKELY / UNKNOWN)
  QB status both sides; backup profile and tempo effect:
  OL / DB / EDGE / WR1 (target share):
  Targeting carryover (1H suspensions):
  Availability report timing for each team:

COACHING
  Tempo philosophy; PROE by state; 4th-down; lead management; end-of-half behavior; opener script history:
  New coordinator / interim / familiarity angles:

GAME SCRIPT
  Expected margin band:   Favorite's bench behavior:   Dog's garbage-time passing capability:
  1H: who defers, end-of-half tendencies, early variance sources:

SITUATIONAL
  Rest / travel / short week / heat / altitude / crowd / time zone:
  (Second-half-only effects marked as such.)

WEATHER
  Forecast (wind sustained/gust/direction, precip, temp) at T−72 / T−48 / T−24:
  Stadium geometry effect:        Front timing vs halves:

RULES / OFFICIALS
  OT relevance:   Crew penalty tendency (if known):

REGRESSION FLAGS
  Turnover luck / close-game record / RZ & 3rd-down outliers / soft-schedule PA / 2nd-order wins:

THESIS BY MARKET
  Full total: lean ___ | band ___–___ | number ___ | confidence A/B/C | kill criteria:
  Team total (A): lean ___ | band ___–___ | number ___ | confidence | kill criteria:
  Team total (B): ...
  1H spread: lean ___ | mechanism ___ | number ___ | confidence | kill criteria:

TAGS (for review): e.g., pace-mismatch, wind, backup-qb, targeting-1h, ol-continuity, lead-mgmt, derivative-lag
```

---

## 9. Turning research into a lean without a score model

You are not projecting a score. You are checking whether the market number sits outside a defensible band and whether the mechanisms that would push it there are identifiable and not already priced.

**Step 1 — Build the possession band.** From 4.1, pick a low and high for the game's possessions per team (e.g., 10–12). Justify the width with script uncertainty.

**Step 2 — Build points-per-possession bands for each offense.** Use the efficiency grid, finishing, and explosiveness to place each offense in a qualitative band relative to the FBS average points per possession for the current season (recompute each year; it has typically been in the low-2s). Example: "A's offense vs. B's defense: above average, 2.4–2.8; B vs. A: below average, 1.6–2.0."

**Step 3 — Multiply to get a range, not a number.** Low possessions × low PPP to high possessions × high PPP gives a wide band; the interior 60% of that band is your "fair zone." If the posted total is inside the fair zone, pass. If it's outside, you have a candidate.

**Step 4 — Apply modifiers with explicit direction.** Weather (−), OL/DB availability (±), coach lead management (− for favorite TT), derivative lag (±), OT inclusion (+ small when near the edge). Each modifier either widens the band, shifts it, or does nothing; write which.

**Step 5 — Count independent mechanisms.** A lean supported by one mechanism (e.g., wind) is a C; two independent mechanisms (wind + possession mismatch) is a B; three or more with no contradicting Tier-1 factor is an A. Judgment-only inputs cap you at B.

**Step 6 — Check the market's story.** Ask what the market would have to believe for the posted number to be right. If that belief is reasonable (e.g., it assumes the backup QB plays, and he might), downgrade. If it's clearly stale (team total didn't move with the main market), upgrade.

**Step 7 — Kill criteria and sizing.** Write the facts that would void the play. Size by grade and liquidity; derivatives get smaller stakes because they're thinner and your CLV measurement is noisier.

For 1H spreads, replace Steps 1–3 with: (a) the front-loaded/back-loaded margin assessment (is the favorite's advantage starter-driven and immediate, or depth/conditioning-driven and late?), (b) the early-variance assessment (turnover-prone QB, return game, explosive dog), and (c) the standard ratio check (does the posted 1H number imply more or less front-loading than this matchup supports?).

**Weighting tiers (default; override with evidence):**
- Tier 1: QB status, possessions/pace by game state, efficiency grid, wind.
- Tier 2: explosiveness/secondary health, trenches/OL continuity, finishing and kicker, coach lead management and end-of-half behavior, targeting carryovers, derivative pricing lag.
- Tier 3: field position/special teams, 4th-down aggressiveness, rest/travel/heat/altitude, officiating crew, roof/surface.
- Tier 4 (information only, no weight on their own): motivation, rivalry, trends, public splits.

---

## 10. Logging, review, and angle validation

Log every play and every *pass* on a candidate game (passes tell you whether your filter is too tight or too loose).

**Fields:** date, game, market, side, number at bet, closing number, CLV, stake, result, confidence grade, primary mechanism tag, secondary tags, possession band vs. actual possessions, script expected vs. actual, weather forecast vs. actual, availability assumptions vs. actual, one-line post-mortem.

**Review rules**
- Evaluate angles on CLV first; require a sample before trusting hit rate (hundreds of bets for totals, not dozens).
- Audit mechanism accuracy separately from outcome: a possession band that contained the actual count and a correct script read is a good process even on a losing ticket.
- Retire or demote angles that fail to generate CLV over a meaningful sample; promote angles with consistent CLV even if short-run results are poor.
- Re-check derivative pricing ratios and book behaviors quarterly; houses change their derivative models.

---

## 11. Reference: thresholds, definitions, stabilization

**Definitions to fix once and keep**
- Success rate: 50% of needed yards on 1st down, 70% on 2nd, 100% on 3rd/4th.
- Standard downs: 1st down, 2nd-and-≤7, 3rd/4th-and-≤4. Passing downs: everything else.
- Explosive play: choose 10+ rush / 20+ pass or 15+/20+ and keep it.
- Scoring opportunity: first down at or inside the opponent's 40.
- Line yards, stuff rate, opportunity rate, power success, havoc: use the Football Outsiders / Connelly formulas as implemented in CFBD.
- Garbage time: choose a quarter-dependent margin threshold (Connelly-style) or a win-probability cutoff (~95–98%) and apply it to every table.
- Expected turnovers: ~50% of fumbles recovered; interceptions as a fixed fraction of pass breakups plus interceptions.

**Weather thresholds (starting points; refine with your own logs)**
- Wind: 12–15 mph sustained begins to matter; 20+ mph significant; account for gusts and direction relative to field orientation.
- Rain: material only when heavy/sustained or combined with wind.
- Cold: minor above ~25°F; combined with wind it compounds.
- Heat: 85°F+ with humidity, afternoon kicks, early season — second-half effect.

**Approximate stabilization (games into the season before a stat is mostly signal)**
- Seconds per play / tempo: 2–3
- Success rate (offense and defense): 4–6
- EPA per play: 5–7
- Points per scoring opportunity: 6–8
- Explosive rate: 8+ (keep prior weight all season)
- Third-down %: 8+ (and still derivative of early downs)
- Red-zone TD %: rarely stabilizes within a season
- Turnover margin: does not stabilize; regress toward expectation

**Derivative pricing baselines (verify against your books each season)**
- Team totals: favorite ≈ (T + S)/2, dog ≈ (T − S)/2, then shading.
- 1H spread ≈ 55–60% of full spread, increasing with spread size.
- 1H total ≈ 46–49% of full total.

**Rules to re-verify each August**
- Clock rules (first-down clock, two-minute timeout, injury-timeout handling).
- Overtime format and OT inclusion in your markets' house rules.
- Targeting enforcement and carryover.
- Kickoff/touchback spots.
- Availability-report requirements by conference.
