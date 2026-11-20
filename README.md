# Living Scent Ledger — Participant Result

This static GitHub Pages site displays one participant's result when the same QR card used for TUI training is scanned with a phone.

Result URL: https://morggan-lgtm.github.io/LSL-Result/?c=LSL-0005

## Page content

The page follows the visual language of the M6 participant journey. The poster with the card ID and assigned planet appears first on phones. The page then presents the actual Part 1 scent blend and the participant's separate recorded response, the six Part 2 element values, the original Part 3 drawing, the TUI scent materials used in all three parts, the personal odour map (POM), the five-axis visitor and planet profiles, and the model's six-planet allocation weights. The participant can open the POM and drawing at full size.

All visible page copy is in English. Planet scent references are design interpretations, not measured planetary odours. The model weights describe allocation, not a measured smell.

## Files

- index.html: single-file result page; no build step
- results/LSL-xxxx.json: participant result and TUI data
- posters/LSL-xxxx.jpg: generated planet image; the page overlays the card ID and planet name
- pom_LSL-xxxx.png: personal odour map for the current TUI session
- drawing_LSL-xxxx.png: original Part 3 pixel drawing

The three current registered TUI records are LSL-0001, LSL-0005, and LSL-0006. LSL-0118 is an archive example without original TUI station data, POM, or drawing; the page marks those items unavailable instead of inventing them.

## Data sources

Current TUI station data, POMs, and drawings were taken from the corresponding LSL card sessions in the main AI-Agent project. The scent catalog and planet scent match labels follow the three user-provided TUI formulation sheets: Part 1 (3067.PNG), Part 2 (3068.PNG), and Part 3 (3069.PNG). Classification weights and generated poster images are the result files previously published for each card.

The result page checks the Pages-relative JSON first for a fast same-origin request, then falls back to the GitHub raw file endpoint when Pages has not yet published a newly committed result. The Part 1 sample blend and the participant's recorded choice are shown separately because the workbook records the choice label, not the sample composition. The Part 2 formulation sheet lists Ocean / Marine as the sixth scent, while the current TUI workbook labels its sixth slider Mineral; the page keeps the recorded slider label and lists the physical scent separately.

## Privacy

Card IDs are sequential and result URLs are guessable. The published files contain no personally identifying information, but anyone who knows a card ID can view that card's result.
