# hyp_165 — APOE4 vs APOE3 iPSC-microglia (mock, D30, astrocyte co-culture)

Worked alone: no Agent tool available; no external retrieval or other model calls. Background biology is
unverified prior knowledge; only supplied IDs are cited.

## Data selection, units, missingness
2304 observations. RNA: 2212 rows, "reported log fold change", base unspecified and left as reported;
every row adjusted p<0.05, |effect|>=1.06 (range -7.94..15.46). Pre-selected DE list, not a whole
transcriptome: 1705 positive / 507 negative = **77.1% positive background**, the null for all sign
comparisons below. Genes absent (ABCA1, ABCG1, NPC1, LIPA, PLIN2, HSPA5, XBP1, HERPUD1, CALR) are
**unknown, not unchanged**. One row is unusable ("gene:??"). Protein: 92 2D spots, log2 scale, 2-6
candidate genes each; 47 significant, 64/92 positive, median +0.48. No spot identifies one protein, so
spots test compatibility/contradiction only.

## Evidence table (membership fixed from canonical lists before directions were seen; all represented members counted)
| Program (queried n) | rep | + / − | median effect (RNA log FC, IQR) | binom P(≥k | p0=0.771) | exceptions |
|---|---|---|---|---|---|
| Sterol/FA synthesis, SREBP (32): SREBF1/2, HMGCS1, ACAT2, LSS, DHCR7/24, EBP, INSIG1, LDLR, SCD, FADS1 | 12 | 12/0 | 1.95 [1.46,2.96] | 0.044 | none represented |
| Lipid uptake/transport/storage (34): SCARB1 8.22, MGLL, DGAT1, SLCO2B1, CD36, TREM2, SOAT1, APOE, NPC2, PLA2G7, FABP5, SCARB2, PLTP, ABHD5, VPS13C, OSBPL1A | 18 | 16/2 | 1.20 [1.06,1.46] | 0.183 | ACSL4 −2.14, OSBPL8 −1.90 |
| Lysosome/CLEAR (51): GAA 9.96, CTSK, GBA, NAGLU, HEXA, SMPD1, CTSB, DPP7, ATP6V1A, CTSD, TFEB, HEXB, MAN2B1, CTSH, GLA, LAMP1, SGSH, CLN3, GPNMB, ATP6AP1 | 22 | 20/2 | 2.34 [1.41,5.60] | 0.091 | CTSS −5.57, IDS −1.56 |
| ER translocation/N-glycosylation QC (47): MLEC 10.21, DDOST 6.22, SRP72, STT3A, UGGT1, STT3B, EMC4, RPN1 | 8 | 8/0 | 2.98 [1.36,4.28] | 0.125 | none |
| UPR sensors/effectors + ER chaperones (48) | 14 | 10/4 | 1.74 [−0.64,2.65] | 0.800 | ERAD arm down: SEL1L −2.09, EDEM1 −1.37, DERL1 −1.19, PDIA3 −1.26; HSPA5/XBP1/HERPUD1/CALR absent |
| COPII/Golgi secretory (45) | 8 | 6/2 | 1.45 | 0.729 | GOLPH3L −7.40, SEC24D −1.39 |
| Mito/OXPHOS/glycolysis (64) | 24 | 17/7 | 2.14 [−1.17,3.40] | 0.835 | split: nuclear TCA/ETC up (MDH1 8.72, OGDH 8.56, ACO2, UQCRC2) vs **all 4 MT-encoded down** (MT-ATP6 −3.35, MT-CYB, MT-ND4, MT-CO2), HK2 −3.67, PFKP −3.08 |
| Phagocytic/complement/homeostatic (44) | 21 | 19/2 | 1.36 | 0.109 | CSF1 −5.91, CCL4 −1.46; no interferon program (2/31) |

Protein spots, used as tests: lysosomal-hydrolase-candidate spots go **both** ways (protein_spot:012 +0.68,
:013 +0.77, :006/:007 +0.58, :063 +0.68 up; :058 −0.85, :067 −1.00, :069 −1.38 down) — compatible with
compartment/processing remodeling, not with a clean hydrolase increase. ER-chaperone-candidate spots are
**not** up (protein_spot:001 −0.49 p=0.11, :004 −0.68 p=0.14, :005 (HSPA5 among candidates) −0.14 p=0.25);
the significant HSP90-containing spot :002 (+0.93) also contains cytosolic HSP90AA1/AB1 and PLEC.

## Mechanism choice and the strongest competitor
Assigned focus (ER proteostasis/UPR/secretory bottleneck) is **rejected as primary**: the UPR set is the
weakest-signed program (10/4, below background), ERAD members move down, canonical markers are absent
(unknown), and no ER-chaperone spot rises. The up ER glycosylation/QC arm (MLEC, DDOST, STT3A/B, UGGT1,
RPN1, EMC4) is retained only as biosynthetic support for N-glycosylated lysosomal hydrolases.

Selected mechanism: **altered lipid routing / a lipid-loading cell state**. The decisive pattern is
co-occurrence of increased uptake and storage machinery (SCARB1, CD36, SLCO2B1, TREM2, SOAT1, DGAT1,
AGPAT2, LPCAT1) with an un-suppressed SREBP program (12/12 up) plus oxysterol/LXR-side genes (CH25H,
CYP27A1, MYLIP) — sterol signalling is split, as expected when delivered sterol sits in ester/lysosomal
pools invisible to the ER sensor rather than in the ER regulatory pool.

Competitor: **successful adaptation / increased throughput** — higher lipid flux handled well. It explains
the same rows and cannot be excluded, since no flux was measured; it is disfavoured only by the
sterol-signalling split (a successful high-flux state should repress SREBP targets) and by TFEB. A third
competitor, lysosomal bottleneck ("failed compensation"), is disfavoured because hydrolase and v-ATPase
transcripts are up, not down. **Decisive unknowns:**
esterification and efflux flux, SREBP2 cleavage, ER-accessible sterol, lysosomal hydrolytic rate,
and ABCA1/ABCG1/NPC1 (unmeasured).

## Counter-evidence, unexplained patterns, limitations
- Strongest unexplained pattern: the mitochondrial split (nuclear TCA/ETC and MDH1/OGDH strongly up while
  all four represented MT-encoded transcripts are down). The lipid mechanism does not predict this; it
  could be mitochondrial transcript depletion, mitophagy, or a technical/ambient artefact of 10X Flex.
- Serious contradiction: down-moving cathepsin-containing spots (:058, :067, :069) and CTSS −5.57 sit
  against the "expanded lysosomal output" step; spot ambiguity prevents resolving this.
- The signed enrichments are modest against the 77% positive background (P 0.04–0.18), genes are not
  independent, and this is descriptive coherence, not a formal enrichment test. No causality is
  established; direction, localization, activity and flux are all inferred, not observed.
