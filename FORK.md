# Funding Hedge execution fork

The `fix/reduce-only-order-size-0.65.0` branch is based on upstream revision
`7b766f8825b2539c5b2ac1375e9d97b41c509edb` (Rust crates 0.65.0).

The execution matching engine caps synchronized reduce-only leaves by the order's
current leaves. A fill in another order cannot enlarge an independent resting
grid order to the whole remaining position. Position and parent caps remain in
effect, and reduce-only enforcement remains enabled.

This is a scoped behavior change for Funding Hedge's independent GTC grid orders.
It is not a general implementation of upstream
[RFC 5348](https://github.com/nautechsystems/nautilus_trader/issues/5348).
Orders cannot grow back after an automatic shrink through this synchronization
path. OTO children which need to grow as a parent continues filling are outside
the supported use of this branch. No submitted-quantity ceiling is tracked.

The consumer pins the Git revision and verifies independent partially filled
reduce-only orders through its native backtest regression. This branch does not
change order construction, fees, accounting, fill models, or strategy logic.
