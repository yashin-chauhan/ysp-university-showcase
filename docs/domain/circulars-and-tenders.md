# 📑 Domain: University Circulars, Tenders & Notices

## 1. Domain Overview

Institutional websites in the public sector are heavily utilized for statutory disclosures, public procurement tenders, recruitment notices, and regional agricultural advisories (see [https://uhf.ac.in/](https://uhf.ac.in/)).

The Circular & Notice Management Engine provides:
- **Taxonomic Classification:** Notices are partitioned into dedicated operational silos:
  - `tenders`: Procurement notices and Request for Proposals (RFPs).
  - `vacancy` / `employment`: Academic and administrative job openings.
  - `nirf`: National Institutional Ranking Framework data and accreditation reports.
  - `farmer`: Agro-meteorological advisories and horticulture crop advisories.
  - `notification`: General university circulars and student notices.
  - `links`: Quick access institutional URLs.
- **Automated Deadline Expiry:** Eliminates the manual burden of unpublishing outdated RFPs or past-due job notices.

---

## 2. Dynamic Expiration Logic

Notices are tagged with an optional `last_date` attribute. The application controller evaluates the current date and automatically restricts query results to active notices:

```php
public function tenders()
{
    $date = date('Y.m.d', strtotime("-1 days"));
    $data['links'] = DB::table('notification_links')
        ->where('section', 'tenders')
        ->where(function($query) use ($date) {
            $query->where('last_date', '=', null)
                  ->orWhere('last_date', '>', $date);
        })
        ->orderBy('id', 'desc')
        ->get();

    $data['header'] = "other_header";
    return view('tenders', $data);
}
```

---

## 3. Multi-Format Asset Attachment

Each notice record supports dual delivery modes:
1. **Direct Document Delivery (`type == 'pdf'`):** Uploaded PDF files are stored on disk under `public/uploads/docs/` with timestamped unique names, preventing namespace collisions.
2. **External Link Referral (`type == 'url'`):** Outbound URLs to external portal systems (e.g., government e-procurement portals, ICAR portals).
