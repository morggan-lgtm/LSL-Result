# Living Scent Ledger — Participant Result

This static GitHub Pages site displays one participant's result when the same QR card used for TUI training is scanned with a phone.

Result URL: https://morggan-lgtm.github.io/LSL-Result/?c=LSL-0005

## Page content

The page follows the visual language of the M6 participant journey. It presents a poster with the card ID and assigned planet, the familiar smell selected in Part 1, the six Part 2 element values, the original Part 3 drawing, the personal odour map (POM), the five-axis visitor and planet profiles, Earth scent references, and the model's six-planet allocation weights. The participant can open the POM and drawing at full size.

All visible page copy is in English. Planet scent references are design interpretations, not measured planetary odours. The model weights describe allocation, not a measured smell.

## Files

- index.html: single-file result page; no build step
- results/LSL-xxxx.json: participant result and TUI data
- posters/LSL-xxxx.jpg: generated planet image; the page overlays the card ID and planet name
- pom_LSL-xxxx.png: personal odour map for the current TUI session
- drawing_LSL-xxxx.png: original Part 3 pixel drawing

The three current registered TUI records are LSL-0001, LSL-0005, and LSL-0006. LSL-0118 is an archive example without original TUI station data, POM, or drawing; the page marks those items unavailable instead of inventing them.

## Data sources

Current TUI station data, POMs, and drawings were taken from the corresponding LSL card sessions in the main AI-Agent project. Planet scent references and suggested scent labels follow the M0 planet archive and M6 participant journey. Classification weights and generated poster images are the result files previously published for each card.

The result page checks the Pages-relative JSON first for a fast same-origin request, then falls back to the GitHub raw file endpoint when Pages has not yet published a newly committed result. The Part 1 descriptions are concrete smell examples associated with the recorded TUI choices; the workbook records choice names, not the physical sample ingredients.

## Privacy

Card IDs are sequential and result URLs are guessable. The published files contain no personally identifying information, but anyone who knows a card ID can view that card's result.
