# 4. Metode Discovery Modul, Screen, State, dan Komponen

## 4.1 Output discovery
* Module: Code, name, purpose, owner, entity, scope, dependency.
* Screen: Screen ID, name, mode, entry/exit, related screen.
* State: Initial, loading, add, edit, view, dirty, invalid, saving, error, conflict, unauthorized, not found.
* Component: ID, label, type, screen, section, parent/container.
* Action: Trigger, precondition, permission, validation, result, error, navigation.
* Data: Source of truth, attribute, type, constraint, lifecycle.

## 4.2 State inventory
* Initial: screen first render dan default values.
* Loading: skeleton/spinner, disabled actions, timeout behaviour.
* Add/Edit/View: field editability dan permission berbeda.
* Dirty: unsaved changes dan navigation guard.
* Saving: double-submit prevention dan idempotency.
* Error/Conflict: recovery path, reload, retry, dan data preservation.
* Unauthorized/Not Found: secure handling tanpa information leakage.