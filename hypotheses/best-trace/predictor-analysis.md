# hyp_165 -> lipidome (APOE4 vs APOE3, mock, D30 iPSC-microglia + astrocytes)

Prior = 0 log2FC. Built only from `hypothesis.json` steps via `build_predictions.py`; no
lipid measurement, no cross-modality transfer, no fitting. Tiers are heuristic bins.

## Rule table

Selector = leading class token of `description` (text before the first `(`, `_` or space),
applied to all 618 features in schema order.

| Selector (n) | Hypothesis step | Tier | Observable link | Unresolved assumption |
|---|---|---|---|---|
| CE (23) | 3,4,6: SOAT1 esterifies delivered + synthesised sterol | +1.0 | CE pool; named in step 6 | SOAT1 transcript = capacity, not rate |
| DE (2) | 3,4 | +0.5 | desmosteryl ester via same SOAT1 route | DHCR24 up should drain desmosterol precursor (opposing) |
| TG (15) | 3,6: DGAT1/AGPAT2/ABHD5 up | +1.0 | droplet TG pool; TG named in step 6 | MGLL/ABHD5 lipolytic arm also up |
| DG (15) | 3: AGPAT2 -> PA -> DG | +0.25 | mid-pathway pool | DGAT1 consumes DG; supply != pool |
| HexCer (14) | 2,6 | +1.0 | named accumulating lysosomal substrate | GBA/GALC capacity up would oppose |
| GM3 (7) | 2,6 | +1.0 | named "GM3-type" substrate | ganglioside synthesis not measured |
| Hex2Cer (9), Hex3Cer (3) | 6: class-wide "lysosomal glyco/sphingolipid substrates" | +0.5 | LacCer/Gb3 pools | species not individually named; HEXA/B, GLA up |
| Sulfatide (3) | 6 | +0.25 | glycosphingolipid substrate | ARSA absent from the elevated hydrolase list; no myelin source in mock |
| BMP (30) | 2: TFEB/LAMP1/ATP6V1A compartment expansion | +0.5 | BMP tracks late-endosomal internal membrane | membrane-pool-scales-with-program assumption; BMP not named |
| HB / hemi-BMP (3) | 2 | +0.25 | acyl-BMP of same compartment | intermediate, turnover unknown |
| PC (116), PE (106), PI (26) | 3: LPCAT1/AGPAT2 phospholipid arm; 4: SCD/FADS1 FA supply | +0.25 | bulk membrane pools, expanded endomembrane | bulk PL is buffered; class-wide claim is weak |
| LPC (75) | 3: LPCAT1 up | -0.25 | Lands-cycle consumption of LPC | PLA2 production side unmeasured |
| Ubiquinone (1) | 4: mevalonate/SREBP2 program un-repressed | +0.25 | isoprenoid branch product | branch-point partitioning unmeasured |
| COH (1) | 3 vs 4 | 0 | — | FC:CE ratio and ER-accessible pool are compartmental; uptake+synthesis vs esterification unresolved |
| SM (44) | 2 | 0 | — | SMPD1 capacity up lowers SM; increased sphingolipid delivery raises it |
| Cer (36), dhCer (4), Sph (3), S1P (5), Cer1P (1) | 2 | 0 | — | Cer is both hydrolase product (GBA/SMPD1) and consumed substrate |
| PS (7) | — | 0 | — | no PS-synthase step |
| PG (21), LPG (8) | 2 (BMP precursors) | 0 | — | increased BMP demand could raise flux or deplete precursor |
| LPE (18), LPI (8) | — | 0 | — | no named acyltransferase; LPC sign not transferable |
| AcylCarnitine (14) | 3 | 0 | — | no CPT1/oxidation claim in the hypothesis |

## Vector composition (computed from the final file)

- positive: 373 (+1.0: 59; +0.5: 44; +0.25: 270)
- negative: 75 (all -0.25, LPC)
- zero: 170
- total: 618; all values in the allowed set; `python validate_prediction.py` -> `VALID: 618 complete predictions`.

The positive skew is intrinsic to the hypothesis (a lipid-loading state), not a quota, and
sits mostly in the +0.25 tier. No +/-2.0 was used: the hypothesis gives direction but never
requires a >=4x whole-cell pool change.

## Major abstentions

Free cholesterol (COH), all sphingomyelins, all ceramides/dihydroceramides and sphingoid
bases (Sph, S1P, Cer1P), phosphatidylserine, PG/LPG, LPE/LPI and acylcarnitines. Each is an
unresolved-sign abstention, not a claim of biological zero.

## Caveats and review status

Transcripts are capacity, not flux; multi-candidate protein spots were used only for
compatibility, never to sign a lipid. Cellular source in the co-culture is unresolved, so
effects are whole-culture pools. No Agent was available: I worked alone and no independent
review occurred.
