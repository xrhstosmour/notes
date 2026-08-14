#erp #sbo #localization #greece #mydata #e-invoicing

myDATA is the Greek tax authority's (AADE) electronic invoicing/bookkeeping platform, businesses transmit sales and expense documents to it, and it maintains an official digital ledger ("e-books") used for VAT/income reporting.

SAP Business One's Greek localization (from the 10.0 FP2008 wave) integrates with myDATA by:

- Classifying transactions by income/expense category and invoice type (`MARK`/invoice-type-style classification fields) so each document maps to the correct myDATA document category.
- Transmitting qualifying documents to myDATA as part of the normal posting flow, instead of a separate manual submission step.
- Keeping the transmitted document's myDATA status/reference visible on the B1 document, for reconciliation when something needs resubmitting or fails validation.

This is a Greek-specific localization feature, not present in other country versions of SAP Business One. Check the current SAP Business One Greek localization guide for the exact setup steps and required master data (income/expense classification codes), those get updated as AADE changes myDATA's requirements.
