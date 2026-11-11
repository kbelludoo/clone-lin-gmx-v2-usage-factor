# clone-lin-gmx-v2-usage-factor

Experimental LIN clone of GMX V2 `getUsageFactor` (uint64-scale: `toFactor(reserved, applyFactor(pool, reserveFactor))`).

- **Upstream:** [gmx-io/gmx-synthetics](https://github.com/gmx-io/gmx-synthetics) `contracts/market/MarketUtils.sol` commit `a85ea3491c19c93bb4b5a002d9b358fb769b7849` (GPL-2.0-or-later after BUSL Change Date 2026-08-31).
- **LIN kernel:** [`src/lin_gmx_v2_usage_factor.lin`](src/lin_gmx_v2_usage_factor.lin)
- **C11 oracle copy:** [`test/oracles/gmx_v2_usage_factor_c11.c`](test/oracles/gmx_v2_usage_factor_c11.c)
- **Proofs (lin-open only):** [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open) `examples/gmx_v2_usage_factor/` and `python3 test/prove_gmx_v2_usage_factor_external.py`
- **Class:** EXPERIMENTAL. Not Arbitrum GMX V2 uint256. Not FLOAT 1e30. Not a production replacement. Not reserved/pool utilization, not Compound `utilizationRate`, not fused `reserved*FLOAT^2/(pool*factor)`, and not `getBorrowingFees`.

Named goldens (uint64-scale, FLOAT'=1e6): reserved 4e7 pool 1e8 rfactor 5e5 usage **800000** vs reserved/pool **400000** vs Compound **285714** vs applyFactor-only **50000000** vs fused-at-scale **0**; remainder 400/1001/5e5 nested **800000** vs fused **799200**; dust 1/3 floor **333333** vs ceil **333334**; reserved=0 max=0 **0/ok=1**; reserved>0 max=0 **ok=0**; over-reserve 6e7/5e7 **1200000** vs cap **1000000**; full max **1000000**; borrow-fee trap **50000000**; 7e9*2e9 **ok=0** vs naive i64 wrap **-4446744073709551616**.
