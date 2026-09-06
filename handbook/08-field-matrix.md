# 8. Detailed Field Matrix Standard

## Kolom dan Tujuan
* Component ID: Stable reference.
* Screen/Section: Lokasi UI.
* Field/Type: Label dan component type.
* M/O/C/System: Required classification.
* Data Type, Min/Max: Constraint eksplisit.
* Format/Allowed Value: Regex, enum, character set.
* Default/Placeholder: Initial presentation.
* State: Enabled, disabled, hidden, read-only.
* Validation: Client/server, cross-field, uniqueness.
* Event/Behaviour: Click/change/blur/Enter/save.
* Message ID: Reference ke catalog.
* Permission: Role/action scope.
* Data Attribute: Reference data/API.
* Source/Assumption: Evidence status.

## 8.1 Standard validation questions
* Apakah null, blank, whitespace-only, zero, dan omitted mempunyai arti berbeda?
* Apakah uniqueness global atau scoped by company/principal/channel/status?
* Apakah boundary date bersifat inclusive?
* Apakah normalization dilakukan sebelum duplicate check?
* Apakah field immutable setelah digunakan transaksi?
* Apakah perubahan field memerlukan cascade, revalidation, atau approval?