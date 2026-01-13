# Academy Voting Comparison Tool 

**Project Goal:**
A single-file HTML/JS web application to compare two voting systems (**Range Reweighted Voting** vs. **Preferential STV/WIGM**) for narrowing a field of 20 films down to 10 nominees. The simulation models an Academy branch (e.g., Visual Effects) with ~35 voters divided into 6 specific archetypes (e.g., "VFX Purist", "Generalist").

### **1. Core Algorithms Implemented**

* **Range Reweighted Voting (RRV):**
* **Logic:** Voters score films 0-10. Winners are picked by highest weighted sum.
* **Reweighting:** Sequential proportional score voting. After a film wins, voters who supported it lose influence for future rounds.
* **Formula:** .


* **Preferential Voting (STV / WIGM):**
* **Logic:** Procedurally converts the 0-10 range scores into a Ranked Ballot (Highest score = Rank #1). Ties in scores are broken by a deterministic "local seed" per voter.
* **Method:** Weighted Inclusive Gregory Method.
* **Quota:** Droop Quota ().
* **Tie-Breaking (Crucial Fix):** We implemented a **Seeded Random Shuffle** for 0-vote tie-breaks to fix the "Alphabetical Assassin" bug (where films starting with 'A' or 'C' were surviving elimination purely due to sort order).



### **2. Current Features (Version 3.0)**

* **Monte Carlo Engine:** Runs 1,000 simulations in <2 seconds to calculate "Nomination Probability" and "System Bias" (Consensus vs. Passion).
* **Matrix Editor:** A spreadsheet-like interface to define the "Master Opinions" (0-10) for each of the 6 voter archetypes.
* **Voter Inspector:** Visualizes every individual voter, showing their Raw Range Scores (sorted 10→1) side-by-side with their Derived Ranked Ballot.
* **Live Updates:** Sliders for "Voter Count" and "Human Nature (Noise)" trigger real-time re-calculation of the single simulation.
* **Smart JSON Config:** A Save/Load feature that exports the matrix and settings. Includes custom formatting logic to align columns and collapse number arrays onto single lines for readability.

### **3. Key Mathematical Insights Discovered**

* **"Auto" Wins:** In the STV system with small committees (35 voters), films on the bubble often win by "Auto" (survival) rather than hitting the Quota, because votes fragment too much in later rounds.
* **The "Invisible Middle":** Films with broad support (all 7/10s) dominate RRV but are often eliminated early in STV because they lack #1 rankings.
* **Bullet Voting:** In RRV, giving 10s to favorites drastically reduces a voter's influence in later rounds (burnout). In STV, having a favorite win by a landslide is beneficial (you retain weight).

### **4. Code State**

The app is a standalone `academy_voting.html` file.

* **Logging:** The algorithms (`runRRV`, `runSTV`) accept a `doLog` boolean flag. This is set to `true` for single sims (populating the "Calculation Logs" tab) and `false` for Monte Carlo (for speed).
* **Rendering:** The "System Discrepancy" logic (showing which films only appear in one system) is located at the end of `runSingleSimulation`.

**Ready for:** Advanced feature additions (e.g., more complex voter behaviors, deeper bubble analysis, or UI refinements).
