# Academy Voting Lab

**[Experiment with the Deployed Version Online](https://kaboom-industries.github.io/Voting-Simulator/)**

> **⚠️ IMPORTANT CAVEATS**
> - This unofficial test "voting lab" is designed to be easy to read and use, and does not fully implement the voting procedures of the Academy. Results do not match official Academy procedures, but it generally illustrates the common differences between the voting systems.
> - All data is fabricated. I (and others) don't know actual votes or even voting patterns. The voting groups are editible to allow for experimentation.

**A Single-File HTML/JS Simulation Tool for Comparative Voting Analysis**

This application allows users to simulate and compare two distinct voting systems—**Range Reweighted Voting (RRV)** and **Preferential Single Transferable Vote (STV)**—side-by-side. It is designed to model "Academy-style" elections, specifically narrowing a field of 20 films down to 10 nominees using a committee of ~35 voters divided into specific archetypes.

---

## Key Features

### 1. Interactive Simulation Dashboard
*   **Real-time Controls:** Adjust voter counts per branch (VFX, Animation, Generalist, etc.) and see results instantly.
*   **Human Nature Engine:** A "Noise" slider allows you to move from "Robots" (voters vote exactly as their archetype dictates) to "Chaos" (voters deviate significantly from group norms).
*   **Deterministic Seeding:** Enter a specific seed to reproduce exact election scenarios, or randomize to test stability.

### 2. Matrix Editor & Dynamic Archetypes
*   **Spreadsheet Interface:** Define the "Master Opinions" (0-10 scores) for each voter archetype.
*   **Customizable Groups:** You are not locked into the default archetypes.
    *   **Rename:** Click any group name to rename it.
    *   **Remove:** Click the 'X' to delete a group.
    *   **Add:** Create entirely new voter blocs with the "Add Archetype" button.
*   **Save/Load & Merge:** Export your configuration to JSON. When loading, you can choose to **Replace** your current setup or **Merge/Append** new archetypes from a file into your existing session.

### 3. Voter Journey Visualization
*   **Trace the Vote:** Select any individual voter (e.g., `gen_01`) to see exactly how their ballot was processed in both systems.
*   **Detailed Step-by-Step:**
    *   **RRV Journey:** See how a voter's "weight" decreases as their favorite films win (preventing them from dominating the slate).
    *   **STV Journey:** Watch a vote transfer from candidate to candidate as they are elected or eliminated. Includes global context (who was elected/eliminated this round) alongside the specific voter's status.
*   **Navigation:** Use on-screen arrows or Keyboard Arrow Keys (Up/Down) to rapidly cycle through voters to spot patterns.

### 4. Monte Carlo Analysis
*   **Probability Engine:** Run 1,000 simulations in seconds.
*   **Bias Detection:** The system flags films as **"Consensus"** (favored by RRV's score aggregation) or **"Passion"** (favored by STV's #1 ranking requirement).

---

## The Algorithms

### Range Reweighted Voting (RRV)
*   **Philosophy:** Maximizes collective satisfaction.
*   **Mechanism:** Voters score films 0-10. The film with the highest total score wins.
*   **The Twist (Reweighting):** Once a voter helps elect a winner, their voting power (weight) is permanently reduced for subsequent rounds.
*   **Formula:** `New Weight = 1 / (1 + Total Satisfaction Score of Winners / 10)`
*   **Outcome:** Ensures minority factions eventually get representation, but prioritizes films with broad support (6s, 7s, 8s) over niche favorites.

### Preferential STV (Weighted Inclusive Gregory Method)
*   **Philosophy:** Prioritizes intense support (#1 rankings) and proportional representation.
*   **Mechanism:** Voters rank films. If a film hits the **Droop Quota**, it is elected. Surplus votes are transferred proportionally to the next choice. If no one hits quota, the lowest vote-getter is eliminated, and their votes transfer at full value.
*   **Tie-Breaking:** Uses a deterministic seeded random shuffle. This fixes the "Alphabetical Assassin" bug where films starting with 'A' were statistically more likely to survive tie-breaks.

---

## Technical Implementation

### Single-File Architecture
The entire application lives in `bake-off-voting.html`. No build steps, servers, or external libraries are required. Just open the file in a browser.

### Verification & Testing
*   **Unit Tests:** A suite of unit tests runs automatically every time the page loads. These tests verify the algorithms against known textbook examples (e.g., a standard STV election scenario) to ensure mathematical accuracy.
*   **Audit Logging:**
    *   **Single Sim:** Detailed, verbose logging captures every weight change, fraction transfer, and elimination.
    *   **Monte Carlo:** Logging is disabled to optimize performance, allowing 1,000 iterations to run in under 2 seconds.

### Data Structure
*   **Input:** JSON configuration containing simulation settings, group definitions, and the preference matrix.
*   **State:** The application uses a seeded Linear Congruential Generator (LCG) for random numbers, ensuring that if you share a Seed and Config with another user, they will see the *exact* same simulation results down to the decimal point.

---

## Getting Started

1.  Open `bake-off-voting.html` in Chrome, Firefox, or Safari.
2.  **Tab 1 (Matrix):** Adjust the scores to reflect your best guess of the voters' opinions.
3.  **Sidebar:** Adjust the "Noise" slider to add realism.
4.  **Tab 3 (Results):** See who wins in a single election.
5.  **Tab 4 (Journey):** Pick a voter to understand *why* they voted that way.
6.  **Tab 6 (Monte Carlo):** Click "Run 1,000x Sims" to see the mathematical probabilities of nomination.
