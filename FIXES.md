# Game Bug Fixes

This document describes the bugs from the reproduction log and the related changes made in `app.py` and `logic_utils.py`.

## Reversed higher/lower hints

**Area:** The `check_guess()` call and hint display in `app.py`, backed by `check_guess()` in `logic_utils.py`

The hint text told the player to keep guessing in the same direction. For example, a guess above the secret returned “Go HIGHER!” The even-attempt branch also converted the secret to a string, which could trigger lexicographic comparisons instead of numeric comparisons. The outcome checker was also an unimplemented placeholder in `logic_utils.py`, so the existing game-logic tests could not exercise it.

**Change:** `app.py` now uses the tested helper in `logic_utils.py` to compare integer values, and maps each outcome to the correct hint (`Too High` means “Go LOWER!” and `Too Low` means “Go HIGHER!”). The string conversion was removed.

**Expected result:** Higher and lower guesses produce correct outcomes and useful hints on every attempt, and the existing game-logic tests can verify those outcomes.

## New Game stayed over

**Area:** The `if new_game:` session-state reset

Starting another game reset the attempt count but did not reset `status` from `lost` (or `won`). The subsequent game-over check therefore stopped the app again. The new secret was also chosen from `1` to `100`, regardless of the selected difficulty.

**Change:** New Game now resets the attempt count, score, status, and guess history, and chooses the secret within the currently selected difficulty's `low` and `high` bounds.

**Expected result:** After clicking New Game, the player can submit guesses again, the game starts with a fresh score and history, and the secret respects the selected difficulty.

## Difficulty changes did not start a matching game

**Area:** Difficulty selection and game-state initialization in `app.py`

Previously, the range display followed the selected difficulty, but the current secret and game state did not change until the player clicked New Game. This could leave the displayed range inconsistent with the secret.

**Change:** The app tracks the active difficulty and starts a fresh game as soon as the selected difficulty changes, using the range for the new difficulty. Both this transition and the New Game button use the same state-reset logic. The range prompt displays the selected difficulty's `low` and `high` values.

**Expected result:** Changing difficulty immediately resets attempts, score, status, and history, and generates a secret within the newly displayed range. No extra click on New Game is needed.