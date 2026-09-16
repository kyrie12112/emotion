# Source Change Log

This file records source-code changes made during reproduction. The Git baseline is
commit `f750175` (2024-07-23). A working-tree snapshot was copied to
`source_history/20260911_after_repairs/` before this tracking file was created.

## 2026-09-11

### `dataloader.py`

- Replaced the IEMOCAP `__getitem__` return statement's backslash continuations with
  a parenthesized tuple. The original form placed comments after line continuations
  and caused a `SyntaxError` before any data could load.
- Connected the existing `train_sampler` to the IEMOCAP training `DataLoader`; this
  preserves the intended train/validation split when `valid > 0` and is equivalent
  to the previous behavior when `valid=0`.
- Verification: `python -m py_compile *.py` passes.

### `iemocap.py`

- Added the batch index when calling `Model.forward` and passed the explicit `train`
  argument in the correct position.
- Unpacked the eighth value returned by `Model.forward`.
- Verification: `python -m py_compile *.py` passes.

### `train.py`

- Added creation of the `show/` output directory before training, so MELD's t-SNE
  export does not fail solely because the directory is absent.
- Verification: `python -m py_compile *.py` passes.

### `layers.py`

- Replaced three identity-string comparisons using `is not` with `!=`.
- This removes Python `SyntaxWarning` messages without changing the intended logic.
- Verification: `python -m py_compile layers.py` passes.

## Backup and recovery

- The original Git version can be inspected with `git show f750175:<file>`.
- The post-repair working-tree snapshot is under
  `source_history/20260911_after_repairs/`.
- Future source edits should first create a timestamped snapshot under
  `source_history/`, then add an entry here with the reason and verification command.
