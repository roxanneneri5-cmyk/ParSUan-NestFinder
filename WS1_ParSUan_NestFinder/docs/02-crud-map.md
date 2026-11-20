# Task 2 · CRUD Map: ParSUan NestFinder

Database: `parsuan_nestfinder` (16 tables, MySQL 8 / InnoDB).
Roles: **Guest** (not logged in), **Student**, **Owner**, **Admin**.

## 1. CRUD map

| Table | C | R | U | D | Pages | Who |
|-------|---|---|---|---|-------|-----|
| users | ✓ | ✓ | ✓ | – | register, login, profile, admin-users | Self: C, R, U own profile · Admin: R all, U status (Active/Suspended). **No delete:** history tables point to the user's profile, so the account is suspended instead (BR4, BR28). |
| students | ✓ | ✓ | ✓ | – | register (student), profile | Self: C, R, U · Admin: R. **No delete:** stays and inquiries must stay on record. Removed only if the user account is removed (cascade). |
| owners | ✓ | ✓ | ✓ | – | register (owner), profile, admin-owners | Self: C, R, U (ID proof) · Admin: R, U verification_status (Pending/Verified/Rejected). **No delete:** owners with properties are protected (RESTRICT); suspend instead. |
| campuses | ✓ | ✓ | ✓ | ✓ | admin-campuses (list + form in one page) | Admin: C, R, U, D · Everyone: R (shown on property pages). Delete is blocked when a property uses the campus. |
| properties | ✓ | ✓ | ✓ | ✓ | properties-list, property-view, property-form, owner-dashboard, admin-properties | Guest/Student: R (Approved only) · Owner: C, R, U own, D own only if no inquiries/stays · Admin: R all, U status (Approve/Reject), D. |
| rooms | ✓ | ✓ | ✓ | ✓ | property-view, room-form, owner-dashboard | Guest/Student: R · Owner: C, U (price, slots), D on own property · Delete is blocked when an inquiry or stay refers to the room. |
| inclusions | ✓ | ✓ | ✓ | ✓ | admin-inclusions (list + form in one page), room-form (as checkboxes) | Admin: C, U, D · Others: R. Delete is blocked when a room uses the inclusion. |
| room_inclusions | ✓ | ✓ | – | ✓ | room-form (checkbox list), property-view | Owner: C, D by ticking/unticking boxes · Everyone: R. **No update:** the row is only keys, so changing an inclusion = delete + insert. |
| property_photos | ✓ | ✓ | – | ✓ | property-form (upload), property-view (gallery) | Owner: C, D on own property · Everyone: R. **No update:** a photo is replaced by deleting it and uploading a new one. |
| favorites | ✓ | ✓ | – | ✓ | property-view (Save button), favorites, compare | Student: C, R, D own · Owner/Admin: counts only (dashboard, reports). **No update:** a favorite has no editable data; it exists or it doesn't. |
| inquiries | ✓ | ✓ | ✓ | – | inquiry-form, my-inquiries, owner-inquiries | Student: C, R own · Owner: R for own properties, U status (Accepted/Declined/Stayed) · Admin: R. **No delete:** kept as history (BR28). |
| stays | ✓ | ✓ | ✓ | – | stay-form, owner-inquiries, my-stays | Owner: C (from an accepted inquiry), R, U (dates, confirmed_by_owner) · Student: R own · Admin: R. **No delete:** kept as history and it unlocks the review. |
| reviews | ✓ | ✓ | – | ✓ | review-form, property-view, admin-reviews | Student: C (only for a confirmed stay, one per stay) · Everyone: R · Admin: D abusive reviews. **No update:** reviews are "verified", so editing after posting would weaken trust. |
| review_replies | ✓ | ✓ | ✓ | ✓ | property-view (reply box), owner-dashboard | Owner of the property: C, U (one reply per review) · Everyone: R · Admin: D (also removed automatically when its review is removed, BR24). |
| reports | ✓ | ✓ | ✓ | – | report-form, admin-reports | Student: C · Admin: R, U status (Open/Resolved/Dismissed). **No delete:** moderation record is kept. |
| notifications | ✓ | ✓ | ✓ | – | notifications (and a bell icon in the nav) | System: C automatically (e.g. inquiry accepted) · Owner/Student/Admin: R own, U mark as read. **No delete:** marked read instead of removed. |

**Rule used:** every "–" has a reason in the same row. Nothing is deleted when it is history (inquiries, stays, reports), when other records depend on it (users, owners), or when a row has no editable data (favorites, room_inclusions, property_photos).

## 2. Form fields for the two most important tables

### 2.1 `properties` (property-form: Add / Edit property, Owner)

| Column | Form control | Required? | Note |
|--------|--------------|-----------|------|
| property_id | none (hidden on Edit) | – | AUTO_INCREMENT |
| owner_id | none (taken from the logged-in owner's session) | – | Never typed by the user |
| campus_id | `<select>` filled from `campuses` (value = campus_id, shows campus_name) | Yes * | NOT NULL, foreign key |
| name | `<input type="text" maxlength="150">` | Yes * | VARCHAR(150) |
| address | `<input type="text" maxlength="255">` | Yes * | VARCHAR(255) |
| latitude | `<input type="number" step="0.000001" min="-90" max="90">` | Yes * | DECIMAL(9,6), matches the CHECK |
| longitude | `<input type="number" step="0.000001" min="-180" max="180">` | Yes * | DECIMAL(9,6), matches the CHECK |
| landmark_directions | `<textarea>` | No | TEXT, NULL allowed |
| rules | `<textarea>` | No | TEXT, NULL allowed |
| curfew | `<input type="time">` | No | TIME, empty = no curfew (NULL) |
| gender_policy | `<select>` or radio: Male Only / Female Only / Mixed | Yes * | Options are the CHECK values; default Mixed |
| description | `<textarea>` | No | TEXT, NULL allowed |
| status | none on the owner form | – | DEFAULT 'Pending'; only the Admin changes it (Approve/Reject) |

### 2.2 `rooms` (room-form: Add / Edit room, Owner)

| Column | Form control | Required? | Note |
|--------|--------------|-----------|------|
| property_id | none (hidden field, from the property the owner is working on) | – | Part of the composite PK + FK |
| room_no | `<input type="text" maxlength="10">` | Yes * | Part of the PK, **typed by the owner** (not auto-increment); must be unique per property. On Edit it is read-only/hidden. |
| room_type | `<select>`: Single Room / Shared Room / Bedspace / Apartment Unit | Yes * | Options are the CHECK values |
| price | `<input type="number" step="0.01" min="0.01">` | Yes * | DECIMAL(8,2), CHECK price > 0 |
| total_slots | `<input type="number" min="1" step="1">` | Yes * | SMALLINT, CHECK >= 1 |
| available_slots | `<input type="number" min="0" step="1">` | Yes * | SMALLINT, CHECK 0 ≤ available ≤ total |
| inclusions (room_inclusions) | Checkbox group, one box per row of `inclusions` (value = inclusion_id) | No | Saved as rows in `room_inclusions` |

## 3. Schema changes

1. **Added `reports.date_filed`** (`TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP`). While planning the admin-reports page I noticed the Admin needs to see the newest reports first, and the `reports` table was the only activity table (like `inquiries.date_sent` and `reviews.date_posted`) without a date. It has a default, so it does not appear on the report form.

```sql
ALTER TABLE reports
  ADD COLUMN date_filed TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP;
```

All other tables work as they are, so there are no other changes. `database/schema.sql` is updated with the new column.