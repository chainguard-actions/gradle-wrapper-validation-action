<!-- markdownlint-disable -->

# Hardening Report: gradle--wrapper-validation-action/v3.5.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `374911c4be584df24e6da57af2d990570ef0f859`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **gradle--wrapper-validation-action/v3.5.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The composite action step references a tag instead of a full 40-character commit SHA: `uses: gradle/actions/wrapper-validation@v3.5.0`. Pin it to a commit SHA.

Locations:

- `action.yml:29`

### prior-fix (severity: high)

Carried forward from this version's previous harden, which fixed it; fix it again unless the code no longer has the problem. The previous harden changed action.yml without recording a finding for it, and this analysis reported nothing there. Re-apply its security changes unless the code no longer needs them. The previous patch:
```diff
diff --git a/action.yml b/action.yml
index 48d1df2..c65e837 100644
--- a/action.yml
+++ b/action.yml
@@ -1,7 +1,6 @@
 name: 'Gradle Wrapper Validation'
 description: 'Validates Gradle Wrapper JAR Files'
 author: 'Gradle'
-
 inputs:
   min-wrapper-count:
     description: 'Minimum number expected gradle-wrapper.jar files found in the repository. Non-negative number. Higher number is useful in monorepos where each project might have their own wrapper.'
@@ -15,25 +14,39 @@ inputs:
     description: 'Accept arbitrary user-defined checksums as valid. Comma separated list of SHA256 checksums (lowercase hex).'
     required: false
     default: ''
-
 outputs:
   failed-wrapper:
     description: 'The path of the Gradle Wrapper(s) JAR that failed validation. Path is a platform-dependent relative path to git repository root. Multiple paths are separated by a | character.'
     value: ${{ steps.wrapper-validation.outputs.failed-wrapper }}
-
 runs:
   using: "composite"
   steps:
     - name: Wrapper Validation
       id: wrapper-validation
       uses: gradle/actions/wrapper-validation@v3.5.0
       with:
         min-wrapper-count: ${{ inputs.min-wrapper-count }}
         allow-snapshots: ${{ inputs.allow-snapshots }}
         allow-checksums: ${{ inputs.allow-checksums }}
       env:
         GRADLE_ACTION_ID: gradle/wrapper-validation-action
-
 branding:
   icon: 'shield'
   color: gray-dark

```

Locations:

- `action.yml`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, prior-fix

**Notes:**

In action.yml, I pinned gradle/actions/wrapper-validation to the commit for its v3.5.0 tag, d9c87d481d55275bb5441eef3fe0e46805f9ef70, and kept a '# v3.5.0' comment so the version stays readable. The previous patch only deleted blank lines and left the uses: line unchanged, so it had no security change to re-apply. Pinning the reference fixes the problem it was carried forward for. I didn't run the action after the change.

