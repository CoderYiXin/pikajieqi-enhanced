# PikaJieQi Enhanced

PikaJieQi cờ úp engine with algorithms ported from multiple sources.

## Algorithms Ported

### ✅ 1. Sigmoid Flip Aggregation (from official Pikafish jieqi branch)
- **Source**: `official-pikafish/Pikafish` jieqi branch (commit 9b963f7)
- **File**: `src/misc.h` — `ScoreCalc::CalcEvg()`
- **Change**: Replace linear average with sigmoid winrate aggregation
- **Result**: +75% win rate vs original (3W-0L-1D)
- **Why**: Sigmoid correctly handles non-linear score distributions

### ✅ 2. Chance Branch Reduction (from AB-JChess)
- **Source**: `lxsgx23/AB-JChess`
- **File**: `src/search.cpp` — `reveal_depth_reduction()`
- **Change**: Reduce search depth for low-value reveals (pawn/advisor by 1 ply)
- **Why**: Save search time on less important reveals

### ✅ 3. Mate Fix in Flip Search (from official Pikafish jieqi branch)
- **Source**: `official-pikafish/Pikafish` jieqi branch (commit 10334fe)
- **File**: `src/misc.h` — `ScoreCalc::CalcEvg()` allDecisive check
- **Change**: Track best_win_mate / best_loss_mate, handle all-decisive positions
- **Why**: Correct mate detection in flip search

## Base Engine

- **Fork**: `brianhliou/pikafish-jieqi-wasm` (branch `jieqi_old-mistboard`)
- **Commit**: `e75cee3a` (pinned in `pikafish-jieqi.ref`)
- **NNUE**: Standard `pikafish.nnue` from Pikafish releases

## Build

```bash
cd src
make -j ARCH=x86-64-sse41-popcnt build
```

## Test with JieqiArena

```bash
# Build JieqiArena from https://github.com/Velithia/JieqiArena
echo -e "jai
setoption name Engine1Path value ./PikaJieQi
setoption name Engine2Path value /path/to/other/engine
setoption name Engine1Options value name EvalFile value pikafish.nnue
setoption name TotalRounds value 10
setoption name MainTimeMs value 3000
isready
startmatch
quit" | ./jieqi_arena
```

## Sources

| Algorithm | Source Repo | Impact |
|---|---|---|
| Sigmoid aggregation | official-pikafish/Pikafish (jieqi) | HIGH |
| Chance branch reduction | lxsgx23/AB-JChess | MEDIUM |
| Mate fix | official-pikafish/Pikafish (jieqi) | MEDIUM |
| qsearch stop fix | brianhliou/pikafish-jieqi-wasm (mistboard) | HIGH |
| dark-piece recursion fix | brianhliou/pikafish-jieqi-wasm (mistboard) | HIGH |

## License

GPL v3 (inherited from Pikafish)
