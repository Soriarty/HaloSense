# <type>(<scope>): <subject>
# |<----  Using a Maximum Of 72 Characters  ---->|

# Explain why this change is being made
# |<----   Try To Limit Each Line to a Maximum Of 72 Characters   ---->|

# Provide links or keys to any relevant tickets, articles or other resources
# Example: Closes #23

# --- COMMIT END ---
# Type can be
#    feat     (new feature)
#    fix      (bug fix)
#    refactor (refactoring code)
#    style    (formatting, missing semi colons, etc; no code change)
#    docs     (changes to documentation)
#    test     (adding or refactoring tests; no production code change)
#    chore    (updating grunt tasks etc; no production code change)
#    perf     (performance improvements)
#    build    (build system changes)
#    ci       (CI configuration changes)
#    revert   (revert a previous commit)
# --------------------
# Scope examples:
#   Hardware: pcb, schematic, bom
#   Firmware: esphome, sensor, network, power
#   Enclosure: 3d-model, mounting
#   Docs: docs, readme, guide
#   Project: deps, config, release
# --------------------
# Subject should use imperative tone and say what the commit does
# Body should explain why the change is being made
# --------------------
# Remember to:
#   - Use the imperative mood in the subject line ("add" not "added")
#   - Do not end the subject line with a period
#   - Don't capitalize the first letter of subject (unless proper noun)
#   - Separate subject from body with a blank line
#   - Use the body to explain what and why vs. how
#   - Can use multiple lines with "-" or "*" for bullet points in body
# --------------------
# Breaking changes:
#   - Add "BREAKING CHANGE:" in the footer
#   - Describe what breaks and migration path
# --------------------
# Examples:
#
# feat(sensor): add DFRobot C4001 mmWave radar support
#
# fix(esphome): correct UART baud rate for C4001
#
# docs(guide): update installation instructions
#
# feat(pcb): replace USB-C with USB-B connector
#
# BREAKING CHANGE: USB-C connector replaced with USB-B.
# Existing cables and enclosures are not compatible.
# --------------------
