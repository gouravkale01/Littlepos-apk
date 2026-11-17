# LittlePOS V2 – Kaayansh Collective

Offline-first Flutter POS source. Existing V1 database is upgraded additively to SQLite schema v3; V1 product/user records are preserved. `deleteProduct()` now archives instead of physically deleting.

## Build APK using GitHub Actions (mobile friendly)
1. Upload/replace the repository files with this ZIP's contents (keep your repository private if it contains business data).
2. Open GitHub → Actions → **LittlePOS V2 Android APK** → Run workflow.
3. Download artifact `littlepos-v2-release-apk` after the workflow succeeds.

## Implemented in this source
- V1 login, product catalog, image/PDF/Excel inventory export, local Wi-Fi shelf server.
- SQLite V2 migration and tables for product variants, customers, suppliers, purchases, expenses, sales, returns, credit/debit notes, company/GST settings, stock movements, audit log and daily closing.
- Unique personal product code and barcode validation at product insertion/update.
- Purchase entry increases product stock and stores unit cost.
- Sale transaction records cost snapshots and reduces stock; cancellation restores stock and retains the cancelled sale.
- Customer return records refund and restores stock.
- Gross-profit estimate (sales less recorded cost of sold goods), expense register and net estimate.
- Supplier entry, daily closing record, GST/company settings storage.
- Main inventory hides zero-stock and archived products; archive replaces hard delete.
- V2 Business Tools screen provides purchase, expense, supplier, returns/notes, cancellation, profit snapshot and closing UI.

## Important limitations to verify before live business use
- This source ZIP is based on the exact seven-file source archive available in the conversation. The repository did not contain the previously described richer V1 variant/POS implementation. Existing code that is not in that source cannot be reconstructed safely.
- GST settings are stored, but statutory tax invoice calculations/numbering and CGST/SGST/IGST rules are not yet a complete compliant invoicing implementation. Have a CA validate GST configuration and invoices.
- Camera barcode scanning, Bluetooth thermal printer integration, complete customer purchase-history UI, backup/restore UI, PIN hashing/staff permission enforcement, and full-size/colour selection in checkout remain to be implemented.
- Flutter compilation was not available in the preparation environment. Run the included GitHub Actions workflow and test on a spare device/database before replacing any live V1 installation.
- Default login in this supplied source: `admin` / `password123`. Change it before real use; do not store sensitive customer data in an unsecured test build.
