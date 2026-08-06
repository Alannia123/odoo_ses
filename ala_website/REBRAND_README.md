# St. Eugene CBSE School — Website Rebrand Notes

This module was previously branded for **two** other schools, mixed together:

- **St. Anne's Convent School**, Chotojagulia, North 24 Parganas, West Bengal
- **Mary Immaculate School ("MIS")**, Basirhat, West Bengal

All of that has been removed and replaced with St. Eugene CBSE School content, written
around the school **opening in June 2027 (Academic Year 2027-28)**.

---

## 1. Before you go live — 13 placeholders to fill

Every unknown detail is marked in the code with the token `SEC-TODO`. Find them all with:

```bash
grep -rn "SEC-TODO" --include=*.xml --include=*.py .
```

| # | File | Line | What to supply |
|---|------|------|----------------|
| 1 | `views/website_header.xml` | 46 | School address + PIN (currently `[School Address], Tamil Nadu - [PIN]`) |
| 2 | `views/website_header.xml` | 48 | CBSE affiliation wording + affiliation number — see §4 |
| 3 | `views/prospectus_template.xml` | 106 | Name of the Trust / Society running the school |
| 4 | `views/prospectus_template.xml` | 249 | Office phone number and e-mail |
| 5 | `views/ala_home_template.xml` | 1713 | Confirm all admission dates with the Management Committee |
| 6-10 | `views/ala_home_template.xml` | 2107, 2121, 2135, 2149, 2165 | Campus location under each leadership profile (President, Secretary, Principal, Manager, Administrator) |
| 11 | `views/privacy_policy.xml` | 67 | School address |
| 12 | `views/razor_pay_templates.xml` | 224 | Legal jurisdiction — currently `[District], Tamil Nadu` |
| 13 | `views/app_release_temp.xml` | 162 | Google Play URL (currently `href="#"`) |

### Placeholder contact details also in use

These are **invented placeholders**, not real addresses. Replace them everywhere:

- E-mail `info@steugeneschool.edu.in` — `views/privacy_policy.xml:68`, `views/razor_pay_templates.xml:102, 170, 228`
- Website `https://www.steugeneschool.edu.in` — `views/privacy_policy.xml:40`

---

## 2. Old branding that was removed

| Removed | Replaced with |
|---|---|
| St. Anne's Convent School / St. Anne's School | St. Eugene CBSE School |
| Mary Immaculate School / Mary Immaculate E.M. School | St. Eugene CBSE School |
| Patroness of the Congregation, Oblates, OMI, Foundress Thatipathri Gnanamma | New St. Eugene content (see §3) |
| Chotojagulia, Chhoto Jagulia, Basirhat, Patilachandra, North 24 Parganas, West Bengal | Placeholders (§1) |
| Marianathapuran, Dindigul, Tamil Nadu - 624003 | Placeholder (§1) |
| **ICSE** (6 places) | **CBSE** — the payment pages contradicted the header |
| `st.annes@gmail.com`, `misbasirhatomi@gmail.com` | Placeholder e-mail |
| `https://misbasirhat.com` | Placeholder website |
| CSS class prefix `mis-` (238 uses) | `seu-` — renamed consistently in markup and styles |
| Route `/ala_oblates`, template `ala_oblates` | Route `/institution`, template `institution_page` |
| Route `/omi_and_education`, template `omi_and_education` | Route `/management`, template `management_page` |
| Route `/download/mis-app` | `/download/steugene-app` |

### Three external links worth knowing about

These pointed at live third-party assets and have all been fixed:

1. **`app_release_temp.xml`** linked to the **St. Anne's Android app** on Google Play
   (`play.google.com/store/apps/details?id=annes.management`). Now `href="#"` — see §1 item 13.
2. **`prospectus_template.xml`** hero image was **hotlinked from `st.annes.school`**.
3. **9 iStock photos** were hotlinked directly from `media.istockphoto.com` (a licensing risk).

All now point at the local asset `/ala_website/static/src/img/school_web.jpg`.
Swap in real campus photography when you have it.

---

## 3. New content written for the 2027-28 opening

The 2026-27 academic year is already running, so "next year" is treated as **AY 2027-28**,
first session beginning **June 2027**.

The consistent story used across every page:

- English-medium, co-educational, CBSE curriculum
- Founding batch admitted to **LKG, UKG and Classes I to V**
- School grows by **one class each year until Class XII**
- Small founding classes; no written entrance test for primary
- Open to all children irrespective of caste, creed or community

**Indicative admission timeline** (repeated on the home page and in the prospectus —
change it in both places, or confirm the dates and lock them):

| When | What |
|---|---|
| Sep 2026 | Applications open online |
| Nov 2026 | Campus open days for parents |
| Jan 2027 | Parent interaction & registration |
| Feb 2027 | First list of selected students |
| Mar 2027 | Fee payment & confirmation of seat |
| May 2027 | Orientation for new parents |
| Jun 2027 | First academic session begins |

Age as on 31 March 2027 — LKG 3+, UKG 4+, Class I 5+.

### Where the new content lives

- **`views/ala_home_template.xml`** — rewritten "Our School" section; **new "Opening 2027-28"
  section** (badge, four fact cards, timeline, Apply Online / Prospectus buttons) inserted
  just before the Facilities section. The year is set once via
  `<t t-set="opening_year" t-value="'2027-28'"/>` at line ~1714 — change it there.
- **`views/prospectus_template.xml`** — all five tabs rewritten:
  1. *Welcome to St. Eugene* (was "Patroness of our Congregation")
  2. *The Institution* (was "Oblates")
  3. *Our Management* (was "OMI and Education")
  4. *Aim and Objectives* — new Vision / Mission / Objectives
  5. ***Admissions 2027-28*** (repurposed from "Our Foundress")
- **`views/academics_template.xml`** — rewritten About Us; junk tab "Syllabus1234" renamed to
  "Examination Pattern"; removed stray placeholder text containing a random number.
- **`views/razor_pay_templates.xml`**, **`views/privacy_policy.xml`** — school name, board,
  contact and jurisdiction.

---

## 4. Two things to check before launch

**CBSE affiliation wording.** The header previously read *"(Affiliated to CBSE)"*. For a school
that has not opened yet this may be inaccurate and can cause problems with the Board and with
parents. It now reads **"CBSE Curriculum · Opening June 2027"**. Once affiliation is actually
granted, update `views/website_header.xml:48` to the exact wording CBSE requires, including the
affiliation number.

**The e-mail and website addresses are invented.** Do not print the prospectus or publish the
payment/privacy pages until the real ones are in.

---

## 5. Pre-existing issues (not caused by the rebrand)

These were already in the module. Flagging them so they don't surprise you.

**Dead files — not listed in `__manifest__.py`, so never loaded.** Their branding was cleaned
anyway so nothing leaks, but they are safe to delete:

| File | Note |
|---|---|
| `views/home_template.xml` | Old home page, superseded by `ala_home_template.xml` |
| `views/working_1.xml` | Scratch file — defines a duplicate `ala_home_page` template id |
| `views/cube_working.xml` | Scratch file — defines a duplicate `ala_home_page` template id |
| `views/phoho.xml` | Duplicate of `program_and_events.xml` |
| `views/program_and_events.xml` | Duplicate of `phoho.xml` |
| `views/student_portal_templates.xml` | Not loaded |
| `views/privacy_policy.xml` | Commented out in the manifest — **but see below** |

> `working_1.xml`, `cube_working.xml` and `home_template.xml` all define a template with
> id `ala_home_page`, the same id as the live home page. If any of them is ever added to
> the manifest it will collide with the real home page. Delete them rather than load them.

**Routes that will 500 because their template is not loaded:**

| Route | Controller | Missing template |
|---|---|---|
| `/privacy_policy` | `controllers/home.py` | `ala_school_privacy_policy` — the file exists but is commented out in `__manifest__.py`; uncomment `views/privacy_policy.xml` to fix |
| `/university` | `controllers/online_application.py` | `university` — does not exist anywhere |
| `/library` | `controllers/online_application.py` | `custom_library` — does not exist anywhere |
| (page render) | `controllers/online_application.py` | `custom_website_page` — does not exist anywhere |

---

## 6. Verification done

- All 24 XML files parse as well-formed.
- All Python files compile.
- No duplicate template ids among the 15 files the manifest actually loads.
- Full-text sweep confirms zero remaining references to St. Anne's, Mary Immaculate, MIS,
  Chotojagulia, Basirhat, West Bengal, Marianathapuran, ICSE, or the old e-mail/domain.
- The new "Opening 2027-28" section was rendered and visually checked; flex `gap` fallbacks
  were added so it degrades correctly on older browsers.

**Not tested:** the module has not been installed into a running Odoo instance. Do a test
install on staging before deploying — `ala_website` depends on `ala_website_backend` and
`ala_school_calender`, which were not part of this archive.
