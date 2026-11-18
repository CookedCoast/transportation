# TIP lists

The map marks a capital project as **TIP** when its project number appears in one of these lists, which are exported from eco interactive. One file per TIP cycle:

| File | TIP cycle |
|---|---|
| `tip-2025-2028.csv` | Southeastern CT / 25-28 TIP |
| `tip-2027-2030.csv` | Southeastern CT / 27-30 TIP |

`tip-lists.json` tells the site which files to load.

Projects that aren't on a list but have FHWA or FTA funding in CTDOT's funding report also count as TIP, labeled **By reference** (the Bridge and Safety list projects).

## Monthly update (about 5 minutes)

1. In eco interactive, open the **Southeastern CT** project list for the TIP cycle and export it, or copy the table.
2. Save it as a CSV with these column headers in the first row. Extra columns are ignored, and column order doesn't matter:

   `ID, Agency, Review Status, Plan Cycle, Revision, Title, Type, Total Cost`

   Only **ID** is required. **Plan Cycle** (for example `Southeastern CT / 27-30 TIP`) sets the cycle label. If it's missing, the label comes from the file name. Tab-separated text pasted straight from eco interactive also works.
3. On GitHub, open the repository, go to the `data` folder and click the file to replace, for example `tip-2027-2030.csv`. Choose **Edit** (pencil icon) and paste the new contents. Or use **Add file → Upload files** with the same file name.
4. Click **Commit changes** to `main`. Cloudflare redeploys the site in about a minute.
5. Check the site footer. It lists each TIP list with its item count, for example "TIP lists: 25–28 (142 items), 27–30 (96 items)".

## Adding a new TIP cycle

1. Add the new file, for example `tip-2029-2032.csv`.
2. Add a line for it to `tip-lists.json`:

   ```json
   {"file": "data/tip-2029-2032.csv"}
   ```

3. To drop a retired cycle from the site, remove its line from `tip-lists.json`. The file can stay in the folder for the record.

The TIP filter buttons and the FY range presets (FY25–28, FY27–30, …) come from whatever cycles are loaded, so nothing else needs to change.

## How IDs are matched

- An eco ID like `0094-0261` matches CTDOT project `0094-0261`.
- A suffixed ID like `0414-0073CN` matches its base number `0414-0073`.
- Year-coded transit grants (`0170-2027AD`, `0474-2028FR`) and program codes (`0170-BRDG`, `PVMT-MARK`, `VARIOUS27BE`) have no mapped project. They're listed on the TIP tab under "TIP line items not on the map", and they're included in the CSV and PDF exports from that tab.
