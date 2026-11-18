# RR-pressure-performance-model-By-blossom
An interactive IPL and T20I pressure-performance analytics project for Rajasthan Royals SupeRR Selector Season 2. Uses ball-by-ball data and win-probability modelling to identify and rank reliable batters and bowlers under pressure.

Rajasthan Royals – Pressure Performance Model

SupeRR Selector Season 2 | Version 2

1. About the Project

Cricket is not just about how many runs a batter scores or how many wickets a bowler takes. What matters just as much is how a player performs when the match is under pressure.

A batter scoring 40 runs in a comfortable chase may not have the same impact as a batter scoring 25 runs when the team is struggling. Similarly, a bowler taking wickets in an easy situation may not have the same value as someone who controls the game during the final overs.

This project was developed to explore one important question:

Who performs when the match is actually on the line?

The objective is to identify batters and bowlers who can make a positive contribution in difficult match situations and use those insights to support Rajasthan Royals' player evaluation and squad-building decisions.

The analysis covers approximately 195,000 deliveries since 2022, with 145 eligible batters and 148 eligible bowlers displayed in the dashboard.

2. How I Approached the Problem

I started by looking beyond traditional cricket statistics.

Instead of ranking players only by total runs, wickets, strike rate or economy, I wanted to understand the context in which those performances happened.

I structured the analysis around five main stages:

Understanding the match situation.

Identifying high-pressure deliveries.

Measuring individual player contributions.

Comparing pressure performance with normal performance.

Ranking players based on performance, resilience and consistency.

The idea was to build a more meaningful comparison between players who may have very different roles and opportunities.

3. How the Pressure Model Works

Step 1: Understanding the match situation

The first challenge was deciding what makes a delivery important.

I used a gradient-boosted win-probability model to estimate the probability of a team winning immediately before each delivery.

The model considers match-state information such as:

Current score

Wickets lost

Balls remaining

Required run rate

Venue par score

Team strength

The model's reported chase-prediction AUC is 0.88 on unseen matches.

This gives us an estimate of how likely a team is to win at a particular point in the match.

Step 2: Identifying pressure deliveries

Not every delivery carries the same importance.

A delivery in a comfortable situation may have very little influence on the result, while a single delivery in a close match can change the direction of the game.

To identify these situations, I used the concept of leverage.

Leverage measures how much the next delivery can move the estimated win probability.

For this analysis, a delivery is classified as a pressure delivery when its leverage is at least 1.5 times the average leverage.

Using this threshold, approximately 22% of deliveries are classified as pressure deliveries.

The dashboard also shows that 69% of these pressure deliveries occur in tight contests, where the estimated win probability is between 25% and 75%.

Step 3: Measuring player performance under pressure

Once pressure deliveries are identified, the next step is to evaluate what players actually contribute during those moments.

For batters and bowlers, the analysis considers:

Runs above expected

Boundary-minus-dot rate

Wicket security

Win-probability added

These measures are compared against the average performance for the same over and wickets state.

This is important because players should be compared in similar match situations. Scoring runs in the powerplay is different from scoring them in the final overs, just as bowling with wickets available is different from bowling when a batting team has wickets in hand.

The model also reduces the influence of small samples by shrinking scores towards zero. Performances against weaker opposition are given half weight.

Step 4: Measuring resilience

Performance under pressure is only one part of the story.

I also wanted to understand whether a player maintains their standard when the situation becomes difficult.

This is where resilience comes in.

Resilience compares a player's performance under pressure with their own normal performance.

A player who performs consistently well in ordinary situations but struggles when the match becomes difficult may be less valuable in pressure situations than their overall statistics suggest.

Step 5: Measuring consistency

A player might produce one outstanding performance but fail to contribute in several other matches.

To avoid relying too heavily on isolated performances, I included consistency.

Consistency measures the percentage of pressure matches in which a player recorded a positive impact.

This helps distinguish players who repeatedly contribute under pressure from players whose rankings may be influenced by a few exceptional performances.

4. Final Player Rating

The final rating combines three components:

Performance

Resilience

Consistency

The default weighting is:

Component

Weight

Performance

55%

Resilience

20%

Consistency

25%

The rating is calculated as a weighted average:

Rating = (Performance × 55 + Resilience × 20 + Consistency × 25) / 100

I also added alternative weighting strategies because player selection priorities can change depending on the team's requirements.

The dashboard includes four presets:

Strategy

Performance

Resilience

Consistency

Default

55%

20%

25%

Performance First

80%

10%

10%

Reliable

30%

20%

50%

Form vs Own Normal

30%

50%

20%

Users can also adjust the sliders manually.

The rankings automatically change according to the selected weights. This makes it possible to understand how different selection priorities affect the final player list.

5. What Makes Version 2 Different?

Version 2 was developed to make the analysis more useful for actual player evaluation, rather than simply displaying a static ranking.

The main improvements include:

Interactive player rankings

Users can switch between batters and bowlers, view the top 25 players, search for specific names and expand individual player details.

Dynamic weighting system

Users can adjust performance, resilience and consistency weights and immediately see how the rankings change.

Rank movement

The dashboard shows how many positions a player gains or loses compared with the default weighting.

This helps identify players whose rankings depend heavily on the selection strategy.

Player confidence categories

Players are grouped into categories based on their positive pressure-match share and pressure-ball sample:

High confidence: at least 60% positive matches and 250 or more pressure balls.

Promising: at least 60% positive matches with a smaller sample.

Inconsistent: 45–59% positive matches.

High risk: below 45% positive matches.

These are practical screening categories, not formal statistical confidence intervals.

Performance vs consistency chart

I added a scatter plot to compare players across two important dimensions.

Further right means stronger performance under pressure.

Higher up means greater consistency.

Larger circles represent players with more pressure balls.

This makes it easier to identify players who combine strong pressure performance with repeatable contributions.

Player shortlist

Users can star players and build a personal shortlist across both roles. The shortlist is saved in the browser when local storage is available.

Rajasthan Royals team analysis

The dashboard also includes:

IPL team bowling impact under pressure.

Rajasthan Royals bowling performance by phase compared with the league.

Rajasthan Royals IPL wins by season.

Potential death-over bowling targets.

The phase analysis helps identify where RR may need improvement, particularly during the death overs.

CSV export

Users can download the current player rankings for further analysis and comparison.

6. How to Use the Dashboard

Open the dashboard in a modern web browser.

Select either Batters or Bowlers.

Choose a weighting preset or adjust the sliders.

Search for a player or apply a confidence filter.

Click a player to see their detailed pressure statistics.

Compare their performance, resilience and consistency.

Use the scatter plot to identify promising players.

Star players to create a shortlist.

Review the Rajasthan Royals team analysis.

Export the rankings as a CSV file.

The dashboard is built as a standalone HTML, CSS and JavaScript application. It does not require a separate server or API key.

7. Limitations and What I Would Improve Next

I do not consider any player ranking to be a final answer on its own.

The current analysis has limitations:

Wicket and win-probability measures can be noisy.

Split-half reliability of the underlying measures is low.

Player samples range from approximately 80 to 500 pressure balls.

Fielding and run-outs are not included.

Batter-bowler matchups are not modelled.

Small sample sizes can affect individual rankings.

For that reason, small differences in ranking positions should not automatically be treated as meaningful.

Future improvements could include fielding impact, batter-bowler matchup analysis, uncertainty intervals, more detailed validation and auction-budget scenarios.

8. Technical Implementation

The current Version 2 dashboard uses:

HTML for the dashboard structure.

CSS for layout, styling and responsive design.

JavaScript for ranking calculations, filters, charts, interactions and CSV export.

Embedded precomputed player and team metrics.

Browser local storage for the player shortlist.

Important methodology note: The gradient-boosted win-probability model is part of the upstream analysis described by the dashboard. Version 2 displays the resulting precomputed player metrics and recalculates rankings when the user changes the weights. It does not train the gradient-boosted model in the browser.

The complete model-training code, feature-engineering process and data-preparation pipeline would need to be published separately to make that part of the analysis fully reproducible.

9. Final Objective

My goal with this project was to move beyond conventional cricket statistics and create a practical way to evaluate players based on how they respond when the game becomes difficult.

For Rajasthan Royals, the most valuable players are not necessarily those who perform well only when conditions are favourable. They are players who can make a difference when the match is close, the required run rate is high, wickets are falling or the final overs demand control.

The central idea behind this model is simple: don't just measure how well a player performs. Measure how well they perform when it matters most.

Disclaimer: This is an independent analytical project developed for SupeRR Selector Season 2. It is not an official Rajasthan Royals selection model, and its rankings should be used as decision-support insights rather than guaranteed predictions of future performance.
