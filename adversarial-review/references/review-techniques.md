# Review Techniques

Use only the techniques relevant to the implementation under review.

## Boundary Analysis

Consider minimum and maximum values, zero, empty values, one-item and very large collections, and just-inside and just-outside boundaries.

## Negative Testing

Ask what happens with malformed, incomplete, unexpected, duplicated, or contradictory input.

## State Transition Analysis

For stateful behavior, inspect initial, active, repeated, completed, failed, retry, and repeated-after-completion states. Look for transitions the implementation assumes cannot occur.

## Failure Injection

Consider network, filesystem, parsing, validation, external API, dependency, configuration, and user-input failures. Determine whether the resulting behavior is safe and understandable.

## Compatibility Analysis

Ask which existing consumer could break. Inspect callers, exported APIs, CLI interfaces, configuration, and data formats when applicable.

## Test-Evasion Analysis

Ask whether the implementation could be made wrong while all existing tests remain green. If so, identify the missing assertion or scenario.
