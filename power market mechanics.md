# power market mechanics
46755
Jalal Kazempour (DTU), Spring 2025 semester

## introduction (lecture 1)
[[31761 – Lecture 12b.pdf]]

### electric power systems
	- generators (conventional (choal, gaz) or renewable (solar farms, wind etc))
    - transmission (high, low, medium -voltage)
    - demands (consumers)

2 ways to organize the electric power systems : centralized (no market) or on electricity market 

### the centralized power system (no market)

a single entity make all operational and planning decisions for the entire power system (needs a system operator).
operational decisions : decisions we take in real time or close future (exemple : for a specific time period how much each generator should produce (Gen X generate Y MW for Z timeframe), load curtailment (cut) )
planning decisions : decisions we take in long term plans

the system operator :
	- wants to min the operational cost. (To produce it costs). 
	- supply demand w/ minimal costs.
	- goal “to meet the entire demand by dispatching power generators across the network in a **feasible** and **cost-effective** manner"

feasible : work within constraints and with security (btw : security “n-1” scheduled in the system -- iven if 1 Gen is out it's still can deliver: some kind of redundancy)

### electricity market
Generators belong to different producers. (portfolio for producers). so the producer goal is to maximize profit by making optimal operation and planning decisions. → Multiple decision-makers involved (interacting w/ each other, decisions are not independent = game theory).

Planning decisions of producers : portfolios extension for exemple.

how it operates when having many ‘participants’ that makes their own profit-maximizing. 

electricity can't be stored at larger scale as of today. --> changing. possible to transform eklecricity unde other forms

###  market
- supply-curve : a non decreasing curve so we rank sellers based on the based on the least-cost. “Merit order principle"
- demand curve : ( non-increasing curve) 
- utility = value of product for a given buyer. = profit (value-cost)*qte [control that formula is correct ?]


- intersection of the demand and supply curve : equilibrium price (**market-clearing**); carried by a market operator (non profitable) 

the area below the demand cruve = total value of utilities (or commodities), similarly represents the total cost for the demand curve area.
![alt text](img/image.png) 
![alt text](img/image2.png)

we want to increase blue, decrease red. leads to social welfare (surplus) area between supply curve and demand curve. by **maximizing social welfare**, the total value of commodities for consumersis maximized, while the total cost for suppliers is minimized—resulting insatisfaction for both the demand and supply sides.

equilibrium point = social welfare is maximized. market clearing price and quantity are determined. (terminology comes from game theory)
based on the equilibium point --> uniform price. qtes are traded at a determined price. and we pay all sellers at the same price. (electrcity markets are often not uniform pricing)

![alt text](img/demand-supply.png)
We do not want to supply all demand. E.g. in this case we see that the demand on the right hand side of the equilibirum (and below) exists but i do not supply. that demande is not willing to pay enough. No free market. 

renewable generators = operational cost = 0 
the gas market price influence what the supply price of the gas generators are willing to pay. 
 

pay-as-bid (other schema) : you pay whatever you bet for. (e.g. w/ wind farms)

in a perfect market, we bid the true op costs. it's  possible to bid negatives prices based on tarifs or government rules may support to balance out the low cost

electricity market is different from other commodity markets
- not possible to store on a large scale.
- electricity demand is highly inelastic to price (this is changing !) = people pay whatever the price 
- physics governed (kirchoff's, etc)
- remark : it's possible to transform/convert it to have it stored (e.g. hydrogen, heat). either convert back (efficiency losses) or use it = integrated energy grid or multi-carrier energy systems.

market clearing algorithms = finding equilibrium supply-demand. the market clearing outcomes are: clearing price ($/MWh), generation/consumption level of each producer/demand (MW)

offer and bids. generators submitt they willing pric to sell = offer, while bid for demand. 

## fundamentals of electricity markets (lecture 2)

### key topics from the previous lecture
- Centralized power systems vs. electricity markets
- Supply and demand curves and their role in market dynamics
- Merit-order principle: Least-cost dispatch in the supply side
- Market clearing: Determining prices and quantities based on supply and
demand curves
- Social welfare: Definition and significance in market efficiency
- Equilibrium concepts: Market-clearing price and traded quantities
- Pricing mechanisms: Uniform pricing (single price for everybody) vs. pay-as-bid pricing (what you offer)
- Unique characteristics of electricity markets compared to other commodity
markets: demand elasticity aspect, physical constraints and not storable.

market clearing algorithm = optimization problem

### goals - agenda 
- market actors
- electricity markets
- usa vs eu electricity markets
- linear optimzation formulation 

### market actors
- **power producers** : conventional gen unit (coal, gas, combined heat, CHP, nuclear, etc), renewbable (hydro, wind, etc.) can be constructed as portfolio. 
- **power demands** : large consumers (industrial plants), retailers (intermediate market actor who purachses electricity in bulk from electricity market and sell it to large number of small scale consumers)
- **market operators** : non profit entity. clears the market by socializing social welfare. 

we need other actors because market clearing outcomes = fiancial contracts (buying/selling). But who is responsible for *operating* the system. For that we need are system operator: 
- **TSO** (transmission system operator) :reponsable for safe operation in the *high-voltage transmission level* where the gris is *meshed*. They ensure system stability (frequency stability, voltage stability, etc   ), supply security, real-time power. (swissgrid in CH, REN in PRTGL. entsoe-e is an TSO on a european level. it exists for coordination of the TSO). TSOs are called ISO in USA. 
- **DSO** (distribution system opertio): responsable for safe operation on *mid and low voltage* (often radial grid). Every DSOs has its own territory. 
- **tso-dso coordinator** : coordination mechanism. they need to work together.

- **market regulator** for short and long run. responisble for monitoring market performance.

- **other market actors** : traders (both pysical or purely financial (exemple buy head market and sell day market)), Balancing Responsible Parties (BRPs), flexibility aggregators.

### types of electricity market
#### capacity market (MW)
designed to ensure *sufficient* generation capacity is available to maintain supply security and reliable operation.

any producer submitting an offer to the electricity market is *elligble* for compensation

capacity payment serve as an incentive for power producers to invest in new gen assets
#### energy market (MWh)
the main market where energy (electricity) is traded. temporal sequence of energy markets :

- **futures market** : long-term contracts, up to 6 years ahead. financial hedging, risk management.
- **day-ahead market** (spot market) : cleared 12-36h before delivery. e.g. Nord Pool Elspot. auction-based, one clearing per day for all hours of the next day.
- **intraday market** : after day-ahead, closer to real-time. continuous trading + discrete auctions. e.g. Nord Pool Elbas. allows adjustments (e.g. updated wind forecasts).
- **balancing market** (real-time / imbalance market) : very close to real-time. TSO activates reserves to maintain system balance. settles deviations from day-ahead/intraday contracts.

#### ancillary service (reserve) markets
ensure system reliability and stability. reserves are capacity booked to be activated if needed in the balancing stage.

- **primary reserves (FCR)** : frequency containment reserve, activated within ~30 seconds. automatic response.
- **secondary reserves (aFRR)** : automatic frequency restoration reserve, activated within ~5 min.
- **tertiary reserves (mFRR)** : manual frequency restoration reserve, activated within ~12.5 min.
- also : black-start capability, reactive power / voltage control.

### from market to operation
by the market operator (e.g. Nord Pool) :
day-ahead market → contracts → intraday market → modified contracts

then TSO (e.g. Energinet) checks : do these contracts ensure safe operation of the system?
- if no → balancing market → actual operation of the system
- ancillary service (reserve) markets : reserve capacities booked to be activated later (if needed) in the balancing stage

(day-ahead = lecture 3, intraday & balancing = lecture 5, ancillary service = lecture 6)

### european vs US electricity markets

#### market and system operation
- **EU** : market operators and system operators are **separate** entities (e.g. Nord Pool = market operator, Energinet = TSO)
- **US** : an Independent System Operator (ISO) is responsible for **both** clearing the market and operating the system (e.g. CAISO, PJM)

#### network modeling for market clearing
- **EU** : transmission network modeled in a simplified manner using a **zonal** representation within day-ahead and intraday market-clearing. no detailed network modeling within each bidding zone.
- **US** : transmission network fully modeled using a **nodal** representation and a linearized power flow model in all market-clearing problems.

#### energy and reserve markets
- **EU** : reserve markets are cleared **separately** by TSOs (e.g. Energinet) *before* the day-ahead energy market is cleared by the market operator.
- **US** : a **joint** energy and reserve market exists in the day-ahead time stage, cleared by the ISO → energy and reserve dispatch **co-optimization** problem.

#### complex offers vs complex market clearing
- **EU** : market actors **internalize** their technical constraints (ramp limits, min production, min up/down time) within their own offers/bids. they offer/bid for their entire portfolio within a bidding zone (not per asset). → complex orders (e.g. block orders in Nord Pool), but market-clearing process remains relatively simple.
- **US** : market actors **submit** all their technical constraints to the market. → market-clearing problem becomes a unit commitment problem with on/off (0/1 binary) variables. → complex market-clearing, but simple bids/offers. introduces pricing challenges due to binary variables.

### market-clearing as a linear optimization problem

#### illustrative example
W1 (wind farm) : forecast 20 MW, offer price €0/MWh
G1 (conventional) : capacity 50 MW, offer price €20/MWh
G2 (conventional) : capacity 100 MW, offer price €30/MWh
total demand = 40 MW (price-inelastic)

supply curve (merit order) : W1 first (0€), then G1 (20€), then G2 (30€)

market-clearing outcomes : W1 = 20 MW, G1 = 20 MW, G2 = 0 MW, clearing price = €20/MWh

#### optimization formulation
minimize total production cost (objective function) :
min 0·p^W1 + 20·p^G1 + 30·p^G2

subject to (constraints) :
- generation limits : 0 ≤ p^W1 ≤ 20, 0 ≤ p^G1 ≤ 50, 0 ≤ p^G2 ≤ 100
- power balance : 40 - p^W1 - p^G1 - p^G2 = 0

primal variables = p^W1, p^G1, p^G2 (production levels)
dual variables (lagrange multipliers) = μ (lower/upper bounds), λ (power balance)

**λ (dual of power balance) = market-clearing price** under uniform pricing.

#### lagrangian function and KKT conditions
standard form : min f(x), s.t. h(x)=0 : λ, g(x)≤0 : μ

lagrangian : L(x,λ,μ) = f(x) + λᵀh(x) + μᵀg(x)

KKT (Karush-Kuhn-Tucker) optimality conditions :
- ∂L/∂x = 0 (stationarity)
- h(x) = 0 (primal feasibility - equality)
- 0 ≤ -g(x) ⊥ μ ≥ 0 (complementary slackness + dual feasibility)
- λ ∈ free (no sign restriction on equality dual)

complementary slackness : g(x)·μ = 0 → either the constraint is active or the dual is zero.

#### verifying market-clearing price via KKT
use the marginal producer (most expensive dispatched gen) to verify price.
G1 is marginal (partially dispatched, 0 < p^G1 < 50) → both bounds inactive → μ^G1 = 0, μ̄^G1 = 0
from KKT stationarity for G1 : 20 + μ̄^G1 - μ^G1 - λ = 0 → λ = 20 → confirms market-clearing price = €20/MWh

#### different demand scenarios
- demand = 10 MW → only W1 dispatched (10 MW), price = €0/MWh (wind is marginal)
- demand = 70 MW → W1=20, G1=50 (fully dispatched), G2=0 → price ∈ [20,30] (price multiplicity, demand falls exactly at boundary between G1 and G2)
- demand = 110 MW → W1=20, G1=50, G2=40 → price = €30/MWh (G2 is marginal)