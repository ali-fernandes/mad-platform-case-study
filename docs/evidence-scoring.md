# Evidence coverage and scoring

MAD separates how strong the available evidence appears from how much of the model has supporting evidence. This prevents a favorable partial assessment from appearing complete.

Each criterion has a weight and a score from 1 to 5 when usable evidence exists. Missing evidence has no score. Some criteria use dated financial or price inputs; qualitative criteria require a user rating and note.

Let total model weight be T, covered weight be C, and earned points be E, calculated as the sum of weight multiplied by score divided by five.

- Available-evidence score = 100 × E / C, when C is positive.
- Coverage = 100 × C / T, when T is positive.
- Supported points = 100 × E / T, when T is positive.
- Completion requires positive total weight and coverage of every weighted criterion.

## Synthetic example

| Criterion | Weight | Score | Earned points |
| --- | ---: | ---: | ---: |
| Reported earnings | 40 | 5 | 40 |
| Valuation | 30 | 4 | 24 |
| Business assessment | 30 | Missing | 0 |

Total weight is 100, covered weight is 70, and earned points are 64. Rounded results are a 91% available-evidence score, 70% coverage, and 64 supported points. The assessment remains incomplete.

The useful engineering property is the explicit missing-evidence state. A polished summary should preserve that state, including if an AI system later explains the result. This scoring example is deterministic logic; it is not a language-model evaluation or a backtested return prediction.
