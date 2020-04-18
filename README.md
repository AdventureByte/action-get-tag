# Get tag name

This action gets tag name from commit that triggered the action and puts it into an environment variable GIT_TAG_NAME.  It will also export is as an output named "tag".

You can also use optional parameters `tagRegex` and `tagRegexGroup` to extract a part from tag string.

## Usage

Dead simple:

```yaml
    steps:
      - uses: AdventureByte/action-get-tag@v2
        id: tagName
        with:
          tagRegex: "foobar-(.*)"  # Optional. Returns specified group text as tag name. Full tag string is returned if regex is not defined.
          tagRegexGroup: 1 # Optional. Default is 1.
      - name: Some other step # Output usage example
        with:
          tagname: ${{ steps.tagName.outputs.tag }}
      - name: Yet another step # Environment variable usage example
        run: |
          docker build . --file Dockerfile --tag docker.pkg.github.com/someimage:$GIT_TAG_NAME

```
