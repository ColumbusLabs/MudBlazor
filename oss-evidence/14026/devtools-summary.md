# Chrome DevTools Accessibility inspector evidence for MudBlazor#14026

Captured from local MudDataGrid fixture runs:
- Before: merge-base `ef2caf9` on http://127.0.0.1:5101
- After: PR head `e25f9c0` on http://127.0.0.1:5102

## Settings menu button
- Before: computed Name empty; no aria-label
- After: computed Name "Columns" from aria-label

## Column drag handle (drag-icon-options)
- Before: computed Name empty
- After: computed Name "Reorder column" from aria-label
