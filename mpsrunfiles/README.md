# MPS run files

The linear programme (LP) of each scenario of this model, as the TIMES model
generator builds it, in MPS format. Any LP solver can read these files, with
no GAMS, Veda or TIMES installation.

The files are attached to the release
[`mps-times-v4.9.7`](https://github.com/esma-ie/OTNYC/releases/tag/mps-times-v4.9.7) rather than kept in git, so that cloning
this repository stays fast. This folder holds only this description.

## Files

| File | What | Size | SHA-256 |
| --- | --- | --- | --- |
| [`OTNYC+s1_nyc_ref+as_run.mps.gz`](https://github.com/esma-ie/OTNYC/releases/download/mps-times-v4.9.7/OTNYC%2Bs1_nyc_ref%2Bas_run.mps.gz) | the LP, free MPS, gzipped | 9.8 MB | `26851d144ff694ffdec2d96d291f2878f6df1521ac640a03ab49a729b0e5e2ea` |
| [`OTNYC+s1_nyc_ref+as_run.dict.txt.gz`](https://github.com/esma-ie/OTNYC/releases/download/mps-times-v4.9.7/OTNYC%2Bs1_nyc_ref%2Bas_run.dict.txt.gz) | GAMS names of its rows and columns, gzipped | 4.1 MB | `8391d3f5ea2c2368bdfd495421c419efd8b9602ae810a4f5a99c79a19ae440dc` |

| Scenario | Rows | Columns | Nonzeros | Objective (CPLEX, in GAMS) |
| --- | --- | --- | --- | --- |
| `s1_nyc_ref` | 236,650 | 557,258 | 1,870,931 | 9,657,725.87 |

Rows and columns as GAMS counted them; the rows include the objective equation `EQ_OBJ`.


## How they were made

- **Scenario, "as run":** the run file `dd/s1_nyc_ref/s1_nyc_ref.run` of this repository, unchanged:
  every option, REDUCE included, as the model sets it.
- **TIMES:** v4.9.7, [etsap-TIMES/TIMES_model](https://github.com/etsap-TIMES/TIMES_model) @ `d9a6a25`.
- **GAMS:** GAMS 54.6.1, the `CONVERT` tool, which writes the model GAMS generated
  for the SOLVE statement: same rows, columns, coefficients, right-hand sides
  and bounds.
- **By:** the reference harness of [TIMES.jl](https://github.com/esma-ie/TIMESjl)
  (`reference/README.md`), the open Julia/JuMP translation of TIMES by ESMA.
  TIMES.jl's checks compare its own LP of each scenario with GAMS's
  `CONVERT` output of these same runs, entry by entry, at 1e-9.

## Reading them

- The objective is a minimisation (`OBJSENSE MIN`) of the single column
  `OBJz`, so its optimal value is the TIMES objective, in the model's
  currency unit.
- GAMS `CONVERT` gives rows and columns generic names: `e1`, `e2`, ... and
  `x1`, `x2`, ... The `.dict.txt.gz` file beside each LP maps them to the TIMES
  names, for example `e1  EQ_OBJ` or `x1  VAR_ACT(REG1,2005,2005,AOTETOT,ANNUAL)`
  (demo12).
- When TIMES moves to a new version, the files are made again and attached to
  a new release (for example `mps-times-v4.9.8`); earlier releases stay.

## Licence

These files are derived from this model and carry its licence,
[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). When you use them:

- credit "OTNYC, Energy Systems Modelling Analytics Ltd (ESMA)" and the original COMET-NYC model by the US EPA Office of Research and Development;
- link to the licence and say whether you made changes;
- share your adaptations under the same licence (ShareAlike).
