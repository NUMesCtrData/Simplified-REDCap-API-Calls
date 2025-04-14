## 🔄 `load_fields_forms_events()`

Simplifies REDCap API calls by building the structured `fields`, `forms`, and `events` parameters programmatically — no more manually aligning `fields[0] = "x"` and `fields[1] = "y"`.

### 🧠 Purpose

REDCap API calls often require indexed parameters like `fields[0]`, `fields[1]`, etc., which can be tedious to write manually — especially with large variable sets. This function allows you to pass simple vectors of fields, forms, and events, and automatically constructs the properly indexed list (`formData`) for use in the REDCap API call.

---

### 📥 Arguments

| Argument | Type | Default | Description |
|----------|------|---------|-------------|
| `fields` | `character vector` | `NULL` | Variable names to pull from REDCap. Converted to `fields[i]` format. |
| `forms`  | `character vector` | `NULL` | REDCap form names. Converted to `forms[i]` format. |
| `events` | `character vector` | `NULL` | REDCap event names. If `"_arm_1"` is missing, it's appended automatically. |

---

### ⚙️ Behavior

- Appends user-defined parameters into a global `formData` list.
- Automatically creates properly indexed REDCap-compatible API parameters.
- Transforms `forms` and `events` into a standardized format:
  - Spaces replaced with underscores.
  - All lowercase formatting.
  - Adds `_arm_1` to events (for single-arm studies).

---

### 📦 Example

```r
load_fields_forms_events(
  fields = c("global_id", "dob"),
  forms = c("contact", "scores"),
  events = c("staff_arm_1")
)
```

This creates the following entries in the `formData` object:

```r
$`fields[0]` = "global_id"
$`fields[1]` = "dob"
$`forms[0]`  = "contact"
$`forms[1]`  = "scores"
$`events[0]` = "staff_arm_1"
```

---

### 🚨 Notes

- Requires `formData` to be a pre-existing object in the **global environment**.
- Uses `<<-` to assign globally. Be cautious in environments where global scope may cause conflicts.
- Only compatible with **single-arm studies** if `_arm_1` is auto-inserted.
