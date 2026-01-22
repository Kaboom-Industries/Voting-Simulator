  Overall Goal: Improve voting algorithm clarity through enhanced logging, unit test display, and a new "Voter
  Journey" tab for individual voter visualization.

  Key Knowledge:
   - Primary application: /Users/rbredow/temp/Voting-Simulator/bake-off-voting.html.
   - Simulates RRV and STV voting systems.
   - Narrows 20 films to 10 nominees; ~35 voters across 6 archetypes.
   - runRRV and runSTV log voter-specific details, storing rrvJourney, stvJourney, and stvChoices on voter objects.
   - runSingleSimulation populates voterJourneys globally.
   - Unit tests run on load, displaying in log-rrv and log-stv.
   - New "Voter Journey" tab (tab #4) visualizes voter contributions.

  Recent Actions:
   - Fixed ReferenceError: runUnitTests is not defined via script order.
   - Modified runRRV to store rrvJourney on voter objects and return modified votes.
   - Modified runSTV to store stvJourney and stvChoices on voter objects and return modified votes.
   - Updated runSingleSimulation to aggregate rrvJourney and stvJourney into voterJourneys.
   - Re-ordered UI tabs, adding "Voter Journey" as #4.
   - Added "Voter Journey" HTML: dropdown, RRV/STV displays.
   - Implemented populateVoterSelect() and renderVoterJourney(voterId).
   - Integrated populateVoterSelect() into runSingleSimulation().
   - Added CSS for voter journey cards and impact.
   - Corrected renderInspector to use v.stvChoices and updated its call in runSingleSimulation.

  Current Status:
   - Fixed the "Voter Journey" tab; it now correctly populates and displays individual voter paths.
   - Optimized algorithms (RRV and STV) to skip journey data collection when logging is disabled (e.g., during Monte Carlo), significantly improving performance.
   - Enhanced "Voter Journey" visualization to include 'Auto-Elected' status as high-impact.
   - Cleaned up minor UI styling issues.

  Known Issues:
   - None currently identified.

  Next Steps:
   - Explore more complex voter behaviors or deeper bubble analysis as requested.

