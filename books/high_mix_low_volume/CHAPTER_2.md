# Chpater 2 - Critical Manufacturing Fundamentals

## 2.1 Just-In-Time Manufacturing (JIT)

Keys to JIT:

- suppliers sych their **delivery schedules** to customers **prod schedules**
  - suppliers hold component stocks right up until needed by mfct
  - only the delivery schedules are aligned, not the production (not necessarily)
- the "heart" of JIT is the reduction of setup time

## 2.2 Kanban

3 types of Kanban systems

- 1. Product specific one-card Kanban system
- 2. Product specific two-card system
- 3. Generic one-card Kanban system

POU = point-of-use

## 2.3 Theory of Constraints

Constraints will determine the overall performance of a mfct system

- `constraint` - anything that limits performance relative to the goals of making money now and in the future
- the total number of constraints in a mfct environment is small (not sure by what measure tho)

Types of constraints:

- capacity (can only produce certian count of units)
  - to prevent starvation, keep an appropriately sized buffer. buffers size is adjusted based on actual measures

Theory of constraints often referred to as:

- drum - rate of the constraint process units
- buffer
- rope - the linkage between the time buffer and the gating operation

High-mix, low-volume lines should be:

- process focused
  - using flexible equipment with setup times that will confer a competitive advantage
  - many manufacturers attempt to enhance the flexibility of machines ill-equipped to obtain the setup time reductions necessary to compete effectively
  - while setup time reductions may be achieved, the likelihood is remote they will be equivalent or superior to those of a competitor
    - a competitor who is using equipment specifically designed for setup time flexibility
- as opposed to product focus

HMLV ranges:

- 600 products or greater
- 0-1,000 order quantities

mfcts that product in batches will experience the problem of "moving constraints" and bottlenecks

poor financial performance is often blamed on "unfavorable order mix"

If you have an "unfavorable order mix" the key is not to lump things together

- need to try and align constraints so that no segment of the time vector are:
  - blocked, or
  - starved

the key is smoothness and stability

## 2.4 Available Capacity

- Available capacity = time available x efficiency x availability x activation
- Utilization = availability x activation
- Efficiency = std units of time produced / time available
- Availability = 1 - (time down / time available)
- Activation = 1 - [idle time / (time available - time down)]

## 2.5 Production System Types

Product life cycels drive marketing sales strategies and pricing strategies that, in turn, drive strategic mfct decisions

Two types fo production systems:

- product focused
- process focused

the type of production system selected for high-mix mfct must be flexible to respond to intermittent demands

advanced technologies are integral to the process focused positioning strategy

Optimal technology for high mix manufacturing:

- multi-purpose machinery that can be
  - quickly changed over
  - is highly reliable
  - easy to maintain

product-focused produciton systems are based on continuos or repetitive demand produced on a dedicated production line

volume-focusing is a specialization of product-focusing that carries the high risk of inflexibility. changes in product mix or product lifecycle changes will leave the mfct facility vulnurable to more flexible competitors

|                 | Build-to-Order       | Build-to-Stock       |
| Product-focused | Low Mix, High Volume | Low Mix, High Volume |
| Process-focused | High Mix, Low Volume | High Mix, Low Volume |

Build-to-Stock:

- is typically selected to offer improved customer responsiveness
- expensive and finished goods inventory levels must be forecast to maintain the level of service required at the minimum investment possible

## 2.6 Manufacturing Resource Planning (MRP II)

Business strategy statement should address:

- What is the basis for achieving competitive advantage (quality, corst, delivery, responsiveness, service, technology?)
- What are the financial strategies as pertains to profit, cash flow, ROI, return on assets, and growth, based on the balance sheet and income statement?
- What are ther esource requirements (e.g. technology, workforce skills, plant and eqiupment, distribution, capital and debt financing required to obtain the assets necessary to achieve planned sales volume, deparmental budgets, growth?)

The information required to effectively perform production planning include:

- actual and planned shipments
- customer order rates
- order backlog
- sales forecast
- new product introductions
- inventory status (raw material, work-in-process, finished goods inventory)
- actual and planned production output
- financial constraints (e.g. capital investment or debt limitations)
- material constraints (e.g. purchase part supply or lead time limitations)
- warranty level
- manufacturing defect level or turn-on rate at test

Important to create the minimal number of product family groupings possible to gein efficient and effective control from management

### Build-to-Stock

- Production plan = Forecast + ending inventory - beginning inventory
- Production rate = Production plan / number of monthly periods

The products are stocked at and directly shipped from finished goods inventory. Customer service levels are derermined based on a forecast of independent demand and statistically-based safety stock levels. Make-to-stock manufacturing environments offer customers the fastest delivery

### Build-to-Order

- Production plan = Forecast + beginning backlog - ending backlog
- Production rate = Production plan / number of monthly periods

The production process is initiated after the reciept of a customer order. Sufficient production capacity and flexibility are necessary prerequisites to appropriately schedule incoming orders. Performance to schedule is of paramount importance if correct customer order delivery date promises are going to be made. Build-to-order mfct environments offer customers the longest delivery times. Long lead time components may be stocked based on a forecast to reduce delivery time

### Assemble-to-Order

- Production plan = Forecast + semifinished goods inventory - backlog change
- Production rate = Production plan / number of monthly periods

Special case fo the build-to-order production environment. Product subassemblies or options that are configured based on the customers specification of the final product are stocked in anticipation of customer demand. The level at which product sub-assemblies or options are stocked is based on forecast. Assemble-to-order mfct environments offer customers significantly faster delivery times than build-to-order mfct environments. A final assembly schedule is used to pull the subassemblies or options necessary to satisfy a particular customer order configuration. The final assy process typically takes only a matter of hours, whereas build-to-order mfct environments may take days or weeks to deliver a product

It is typically very difficult to forecast demand of HMLV products, for a variety of reasons

Focus forecasting (tm) is preferred method of predicting future demand

The overriding goal of master planning is to develop a plan that can be executed at least 95% of the time.

## 2.7 Scheduling

The primary objectives of scheduling for HMLV are:

- On-time delivery
- Minimum total processing time
- Maximum resource utilization
- Minimum inventory

In reality, these objectives are in conflict with each other lol

for HMLC, competitive advantages should be pursued in the areas of:

- quality
- responsiveness
- on-time delivery

To achieve competitive advantage, the schedule must be based on relatively small lot size

In order to produce the small lot sizes required, sufficient capacity must exist to facilitate the large number of machine setups required

Maximizing resource utilization in a HMLV mfct environment is not a core competency

### 2.7.1 Multiple Constraint Synchronization (MCS) Algorithm

## 2.8 Test

Mnay HMLV face the problem if insufficient capacity for their test product.

Can test at the sub assy level, or just test the full assy and then send defective subassys to be tested separately

Probably revisit this section later
