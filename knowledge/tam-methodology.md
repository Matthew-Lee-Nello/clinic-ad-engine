# TAM methodology (repeatable market sizing for a treatment in a country)

The standard, repeatable way to size a treatment's market in a specific country. Run it the same way every time so the number means the same thing across clients. Danny asks "what is the TAM size?" for every treatment, this is the answer, done rigorously and fast.

Never invent a number. Every figure is either sourced or a stated assumption. Show the working. A defensible estimate with clear assumptions beats a confident guess.

## The three numbers

- **TAM** (Total Addressable Market): everyone in the country who could plausibly want this treatment, as annual spend.
- **SAM** (Serviceable Available Market): the slice the clinic can actually reach and serve (geography, language, price tier, clinic capacity).
- **SOM** (Serviceable Obtainable Market): what is realistically winnable in 12 months at the current ad budget and close rate. This is the one that decides whether the treatment is worth launching.

## Top-down calculation (the spine)

Work top to bottom, writing each factor, its value, and its source or assumption:

```
Country population (target age + gender)          [source]
  × prevalence or demand rate for the treatment    [source or assumption]
  = people with the want/need per year
  × share who can afford the price tier            [assumption, from price + income data]
  × share who act (convert to a paying procedure)  [assumption, benchmark]
  = annual procedures in the country (demand)
  × average procedure price                        [from research / the clinic]
  = TAM (annual market value)
```

Then narrow:
- **SAM** = TAM × (reachable geography share) × (language/segment share) × (this clinic's price-tier share).
- **SOM** = SAM × realistic 12-month market share, sanity-checked bottom-up below.

## Bottom-up sanity check (always do this)

Cross-check SOM from the clinic's actual funnel, so the top-down number cannot run away:

```
Monthly ad budget ÷ realistic cost per booked consult   = consults/month
  × consult→procedure close rate                          = procedures/month
  × average price                                          = monthly revenue
  × 12                                                     = bottom-up SOM
```

If top-down SOM and bottom-up SOM are wildly apart, say so and explain which to trust and why. They rarely match exactly; the gap itself is information (headroom or a bottleneck).

## Where to get the inputs (Exa / web research)

- Population by age/gender: national statistics office, UN/World Bank.
- Treatment demand/prevalence: medical journals, industry reports (e.g. aesthetics market reports), procedure-volume stats, association data.
- Price: the clinic's own pricing, competitor pricing, market reports.
- Income/affordability: national median income, the treatment's price as a share of it.
- Benchmarks (act/convert rates): stated as assumptions with a rationale; refine with the clinic's real numbers when available.

Prefer the clinic's own real numbers (price, close rate, CPL) over generic benchmarks wherever they exist.

## Worked example (illustrative, numbers are placeholders)

Rhinoplasty, Singapore:
- Population 20–45, all genders: ~2.0M `[stats office]`
- Annual demand rate for rhinoplasty: ~0.3% `[aesthetics market report — assumption]` → ~6,000 people/yr
- Can afford ~SGD 12,000 procedure: ~35% `[income distribution — assumption]` → ~2,100
- Act within the year: ~25% `[benchmark — assumption]` → ~525 procedures/yr
- × SGD 12,000 = **TAM ≈ SGD 6.3M/yr**
- SAM (reachable, English-speaking, this price tier ~40%): **≈ SGD 2.5M/yr**
- SOM top-down (5% share yr 1): **≈ SGD 126k/yr**
- SOM bottom-up: SGD 300/day budget ≈ SGD 9k/mo ÷ SGD 150 CPL = 60 consults, × 20% close = 12 procedures/mo × SGD 12k = **SGD 144k/mo** → the funnel implies far more than the 5% top-down share, so demand is not the constraint; delivery and budget are. Flag it.

(Replace every placeholder with a real, sourced figure per treatment. The example shows the shape, not the answer.)

## Output (goes into the brief's market-sizing section)

- TAM, SAM, SOM, each with the factor table (value + source/assumption).
- The bottom-up cross-check and what the gap tells us.
- One-line verdict: is demand, budget, or delivery the constraint, and is this treatment worth launching at the current budget.
