# Firebase sync setup

This app uses the existing Firebase project `couple-battleship` and stores kitchen data under:

`kitchenHomes/<6-digit-home-code>`

Anonymous Authentication must remain enabled.

## Important
Do NOT replace the project's whole Realtime Database Rules with the snippet below if other apps already use the same Firebase project. Merge only the `kitchenHomes` child into the existing top-level `rules` object.

```json
"kitchenHomes": {
  "$homeCode": {
    ".read": "auth != null",
    ".write": "auth != null",
    ".validate": "$homeCode.matches(/^[0-9]{6}$/)"
  }
}
```

This deliberately keeps access scoped to authenticated Firebase clients and valid six-digit household paths. It is appropriate for a low-sensitivity household shopping list. It must NOT be reused for patient or clinical data.
