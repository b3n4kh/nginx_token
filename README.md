# ngx_token_binding

This NGINX module provides mechanism to cryptographically bind HTTP cookies
to client's HTTPS channel using Token Binding, as defined by following IETF
drafts:

- [draft-ietf-tokbind-protocol](https://tools.ietf.org/html/draft-ietf-tokbind-protocol),
- [draft-ietf-tokbind-negotiation](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation),
- [draft-ietf-tokbind-https](https://tools.ietf.org/html/draft-ietf-tokbind-https).

## Status

Debian based NGINX Docker container with ngx_token_binding plugin.

[Token Bind](https://github.com/google/token_bind)

### `token_binding`

- **syntax**: `token_binding on|off`
- **default**: `off`
- **context**: `http`, `server`

Enables negotiation and verification of the Token Binding protocol.

Token Binding ID variables (described below) are going to be available when
client successfully negotiates Token Binding.

### `token_binding_cookie`

- **syntax**: `token_binding_cookie <cookie>|all|none`
- **default**: `none`
- **context**: `http`, `server`

Binds selected `<cookie>` (or all) to client's HTTPS channel and verifies that
properly bound cookies are received from the client.

Because Token Binding ID can be established only over HTTPS, `Secure` attribute
is going to be added to cookies bound this way. Also, such cookies are going to
be removed from HTTP requests and responses.

### `token_binding_secret`

- **syntax**: `token_binding_secret <secret>`
- **default**: `none`
- **context**: `http`, `server`

Secret used to bind cookies using `token_binding_cookie` directive.

## Variables

### `$provided_token_binding_id`

Returns `base64url(sha256(ProvidedTokenBindingID))` if client negotiated
Token Binding.

### `$provided_token_binding_key_type`

Returns key type of `ProvidedTokenBindingID` if client negotiated Token Binding.

### `$referred_token_binding_id`

Returns `base64url(sha256(ReferredTokenBindingID))` if client negotiated
Token Binding.

### `$referred_token_binding_key_type`

Returns key type of `ReferredTokenBindingID` if client negotiated Token Binding.

## License

    Copyright 2016 Google Inc.

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
