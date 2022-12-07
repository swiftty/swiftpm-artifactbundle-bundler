# Swift Artifactbundle Bundler

- create artifactbundle

# Usage

```yml
publish:
  needs: [ build ]

  runs-on: ubuntu-latest

  steps:
  - uses: swiftty/swiftpm-artifactbundle-bundler@v1
    id: bundler
    with:
    variants-version: ${{ github.ref_name  }}
  - uses: softprops/action-gh-release@v1
    with:
    generate_release_notes: true
    body: |
        ## Checksums
        - for `.binaryTarget(name:url:checksum:)`

        ```
        ${{ steps.bundler.outputs.checksums }}
        ```

        ---
    files: |
        ${{ steps.bundler.outputs.path }}/**
```

when finished swiftpm-artifactbundle-bundler step, generated zip files at `${{ steps.bundler.outputs.path }}`.
