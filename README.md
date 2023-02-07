# URL Redirection Service

This is a simple web page that redirects to the URL encoded in the URI fragment (the part after the "#").
For example <https://tom93.github.io/redirect/#https://example.com> redirects to <https://example.com>.
It is useful for preventing "intelligent" software from processing URLs of a particular form.

The target URL can be encoded using `encodeURIComponent()`.
Alternatively, the following function preserves most special characters for readability while still producing a valid encoding:

```js
function encodeURIFragment(s) {
  /* Encode a string for inclusion in the URL fragment. */
  /*
    Relevant syntax specification (https://www.rfc-editor.org/rfc/rfc3986.html):
    fragment      = *( pchar / "/" / "?" )
    pchar         = unreserved / pct-encoded / sub-delims / ":" / "@"
    unreserved    = ALPHA / DIGIT / "-" / "." / "_" / "~"
    sub-delims    = "!" / "$" / "&" / "'" / "(" / ")"
    / "*" / "+" / "," / ";" / "="

    The set of safe characters is almost the same as for encodeURI(), except encodeURI() does not encode "#".
    So we just use encodeURI() and then encode "#" manually.
  */
  return encodeURI(s).replace(/#/g, "%23");
}
```
