# E-commerce-pricing-elasticity-analysis
Does Discounting Actually Grow Sales? A Pricing Analysis on 100K+ E-Commerce Orders
Olist Brazilian E-Commerce Dataset, 70+ product categories
Why I did this

Every e-commerce platform reaches for discounts when they want more sales it's the easiest lever to pull. But it also eats straight into margin, and it's not obvious that it's even working the way people assume. I wanted to dig into real order data and actually test it: when price drops, does volume really go up? And if it does, is that true everywhere, or only in certain categories? 

What I did

I pulled the Olist dataset from Kaggle  five separate CSVs (orders, order items, products, payments, reviews) that needed to be joined together in Pandas before any of this was possible. After merging, I had a single table of just over 100,000 delivered orders spanning 70+ product categories.

A few cleanup decisions along the way: I dropped anything that wasn't a delivered order, translated the category names out of Portuguese, and cleared out a handful of rows with missing data. Since Olist doesn't give you real cost or margin figures, I used freight value and payment installments as rough stand-ins for affordability  not perfect, but the best proxy available.

From there I ran the analysis in a few stages:

Grouped everything by category to get average price, order volume, and revenue.
Split categories into price quartiles to see if cheaper = more sales, in a straight line.
Tried to estimate actual price elasticity  both across categories and within a single category over time  using log-log regression.
Bucketed categories into mass-market (low price, high volume), niche (high price, low volume), and everything in between.
What I found

Honestly, the elasticity regressions didn't hold up. Neither the cross-category version nor the within-category time-series version came back statistically significant (p > 0.28 both times). I chased this a bit further than I probably needed to  even got a suspiciously clean result at one point (elasticity of +6.4, p < 0.001) that turned out to be driven almost entirely by noisy, low-volume months right after the marketplace launched. Once I trimmed those out, the signal disappeared. I'd rather report that honestly than dress up a misleading number, especially since it's a useful finding in its own right  it shows price alone doesn't explain category-level demand once you control for the fact that different categories just have inherently different baseline popularity.

The real story turned out to be in the segments, not the regression:

Mass-market categories are priced 3.4x lower than niche categories, but move 26.9x more volume and bring in 7.3x more revenue per category.

That's a much bigger gap than I expected going in. I also noticed something less obvious in the quartile breakdown: the second price quartile — not the cheapest one — had the highest average volume of all four. Categories priced at rock-bottom actually did worse than the moderately-priced tier. So cheaper isn't simply better; there seems to be a sweet spot.

What I'd recommend
Push discounts into the mass-market categories bed & bath, sports & leisure, furniture, telephony, electronics. These are already the categories where lower prices line up with far higher volume and revenue, so a discount here builds on an advantage that already exists rather than trying to manufacture one.
Leave niche/gift categories alone  watches & gifts, cool stuff, and similar. Demand there looks much less about price and more about occasion or gifting, so discounting is more likely to just give away margin than to move volume.
Don't race to the bottom on price. The quartile pattern suggests that going too cheap can actually backfire — a moderate price point outperformed the cheapest tier. Aim for a sweet spot, not the floor.
Caveats worth knowing
There's no real margin data in this dataset, so freight value and installment count are stand-ins, not the real thing.
Everything here is observational  I'm describing patterns and correlations, not proving causation. A proper elasticity estimate would really need controlled price experiments (A/B testing on price) to nail down cause and effect.
The first few months after Olist launched had very few orders, which made the early data noisy enough that I excluded it from the time-series checks.

Built with Python, Pandas, Matplotlib, and SciPy. Full notebook: ecommerce-pricing-elasticity-analysis.ipynb
