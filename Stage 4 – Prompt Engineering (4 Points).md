# **Stage 4 – Prompt Engineering (4 Points)**

**Due:** December 12, 2025

---

## **Goal**

Translate your Stage 2 specification and Stage 3 Excel logic into a precise, executable AI prompt capable of generating a complete, professional spreadsheet model. Your prompt must include scenario-specific variables, real market data, and clear modeling requirements aligned with your specification.

You are now practicing the role of a **Finance Technologist / Treasury Analyst** who builds hybrid human–AI analytical pipelines.

Upload the following deliverables to your GitHub repo.

---

# **Deliverable 1 — Structured AI Prompt (1–2 page .md file)**

Your prompt must include the following sections.

---

## **1\. Scenario-Specific Variables**

Use the exact Stage 2 values:

| Variable | Value | Description |
| ----- | ----- | ----- |
| `FC_AMT` | 12,500,000 | EUR receivable amount |
| `S0_in` | 1.0850 | Spot rate (USD/EUR) |
| `F0_in` | 1.0910 | 1-year forward rate |
| `R_USD` | 4.75% | U.S. interest rate (ACT/360) |
| `R_FC` | 3.25% | EUR interest rate (ACT/360) |
| `K_PUT` | 1.0910 | EUR put strike |
| `K_CALL` | 1.0910 | EUR call strike |
| `PREM_PUT` | 0.017 | Put premium |
| `PREM_CALL` | 0.022 | Call premium |
| `T_DAYS` | 360 | Days to maturity |

Compute automatically:

* `T_YRS = T_DAYS / 360`

All values must be explicitly stated in the prompt so the AI does not infer anything.

---

## **2\. Excel Spreadsheet Requirements**

Your prompt must instruct the AI to generate an Excel model with the following:

### **Named Ranges**

The AI must use the following names exactly:

`FC_AMT`, `S0_in`, `F0_in`, `R_USD`, `R_FC`,  
 `K_PUT`, `K_CALL`, `PREM_PUT`, `PREM_CALL`,  
 `T_DAYS`, `T_YRS`

---

### **Color Coding**

Your spreadsheet must follow FIN-321 standards:

* **Yellow** \= Inputs

* **Blue** \= Assumptions

* **Green** \= Formulas

* **Gray** \= Outputs / KPIs

---

### **Model Components**

The spreadsheet must include:

#### **A. Forward Hedge**

* Convert EUR to USD at the forward rate

* Output: total USD received at maturity

#### **B. Money Market Hedge (3-Step)**

1. PV of EUR receivable

2. Convert to USD today

3. Invest USD at domestic rate

#### **C. Option Hedges**

* Put premium

* Payoff logic: `MAX(K – S_T, 0)`

* Net payoff after premium

* Call option logic (for collar comparisons)

#### **D. Sensitivity Table**

* Spot scenarios from `0.95 × S0` to `1.05 × S0`

* Show outcomes for:

  * Forward hedge

  * MM hedge

  * Net put payoff

  * Net call payoff

#### **E. Clean Formatting**

* Labeled sections

* Currency formatting where appropriate

* Clear separation of model blocks

#### **F. Cross-Checks**

* Forward–MM parity

* Put–call parity

* Formula consistency

* Confirm no hard-coded values

---

## **3\. Full Prompt to the AI (What You Submit)**

Below is the exact structured prompt you will include in the .md file.

`You are a Financial Modeling Assistant. Build a complete Excel model for U.S. Tech Services Inc.’s EUR receivable using the specifications below.`

`# GOAL`  
`Create a full FX hedging model including forward, money market, and option hedge scenarios, plus a ±5% sensitivity table.`

`# INPUT VARIABLES`  
`FC_AMT   = 12,500,000`    
`S0_in    = 1.0850`    
`F0_in    = 1.0910`    
`R_USD    = 0.0475`    
`R_FC     = 0.0325`    
`K_PUT    = 1.0910`    
`K_CALL   = 1.0910`    
`PREM_PUT = 0.017`    
`PREM_CALL= 0.022`    
`T_DAYS   = 360`    
`T_YRS    = T_DAYS / 360`

`# SPREADSHEET REQUIREMENTS`  
`Use named ranges: FC_AMT, S0_in, F0_in, R_USD, R_FC, K_PUT, K_CALL, PREM_PUT, PREM_CALL, T_DAYS, T_YRS.`

`Color coding:`  
`- Yellow = inputs`    
`- Blue = assumptions`    
`- Green = formulas`    
`- Gray = outputs`  

`Include:`  
`1. Forward hedge calculation`    
`2. Money market hedge (3-step)`    
`3. Put and call hedge logic (premium + payoff)`    
`4. Sensitivity table from 95% to 105% of spot`    
`5. Verification: parity checks + named range confirmation`    
`6. Clean formatting with labeled sections`  

`# MODEL LOGIC (PSEUDOCODE)`  
`Forward_USD = FC_AMT * F0_in`

`MM_FC_PV        = FC_AMT / (1 + R_FC*T_YRS)`  
`MM_USD_NOW      = MM_FC_PV * S0_in`  
`MM_USD          = MM_USD_NOW * (1 + R_USD*T_YRS)`

`Put_payoff_per  = MAX(K_PUT - S_T, 0)`  
`Put_net         = Put_payoff_per*FC_AMT - PREM_PUT*FC_AMT`

`Call_payoff_per = MAX(S_T - K_CALL, 0)`  
`Call_net        = Call_payoff_per*FC_AMT - PREM_CALL*FC_AMT`

`# VERIFICATION`  
`- Confirm parity: Forward_USD ≈ MM_USD`    
`- Confirm put–call parity`    
`- Confirm named ranges exist`    
`- Confirm color coding`  

`# EXPORT`  
`Return:`  
`1. A downloadable .xlsx file`    
`2. A formula map`    
`3. Verification summary`

---

# **Deliverable 2 — Excel Workbook**

Your spreadsheet must include:

* All scenario-specific inputs

* All named ranges

* Color coding

* Forward hedge

* Money market hedge

* Option hedge calculations

* Sensitivity table

* Cross-checks

(*You already have the working file I generated earlier — that is Deliverable 2\.*)

