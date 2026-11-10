# Separate Refund Request and Refund lifecycles

A Refund Request records the team's decision (Open → Approved / Declined) and a Refund records the money going back (Pending → Issued / Failed), rather than one combined status. Approving and actually returning the money are separate events once a payment processor is involved, and a failed payment must not undo an approval. No processor is connected yet, so today a Refund is created and immediately marked Issued. Modelling the second lifecycle now costs almost nothing, and adding it to the schema later would be expensive.

## Considered Options

- **One status on the Refund Request** (Open → Approved / Declined / Refunded). Rejected because it mixes the team's decision with payment outcome, and has no way to say "approved, but the payment failed".
- **Approval means issued**, with no Refund state. Rejected because it would need reworking as soon as a real processor is connected.
