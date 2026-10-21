# Security architecture

Version 0.3 extends the control plane. Research design only.

## Trust boundaries

Synthetic fixture or injected public ticker -> Source attestation -> Strategy research rules (long/short observations) + regime overlay -> Risk gate (class caps, kill switch, drawdown, concentration) -> Paper fill only -> Hash-chained audit log.

Trade or withdrawal keys are refused and never loaded. Roles cannot enable live trading. Redaction covers private-key hex, seed phrases, and wallet addresses.

## Roles

| Role | Allowed | Denied |
|---|---|---|
| Researcher | scan, backtest, read audit | place order, withdraw, enable live |
| Auditor | read audit, verify chain, scan | place order, withdraw, enable live |
| Operator | scan, kill switch, read audit | place order, withdraw, enable live |

## Data classes

Public market data (OHLCV, funding), integrity labels (SYNTHETIC/PUBLIC_READ), secrets (refused), sensitive identifiers (redacted), personal data (tripwire).

## Threats and controls

- Secret committed: gitleaks + expanded redaction
- Trade/private key paste: refuse + patterns
- Fixture injection: SYNTHETIC label + attestation
- Stale/jumped feed: feed_status
- Oversized risk: class caps, confidence, vol scaling, concentration
- Runaway loss: drawdown + kill switch
- Audit tamper: SHA-256 chain
- Live mistake: mode guard + RBAC deny

This is not a certified security product.
