#  Loader Policy Builder _(loader-policy)_

> Document loader policy builder for JSON-LD, DIDs and VCs

## Table of Contents

- [Security](#security)
- [Background](#background)
- [Usage](#usage)
- [Contribute](#contribute)
- [Commercial Support](#commercial-support)
- [License](#license)

## Security

As with most security- and cryptography-related tools, the overall security of
your system will largely depend on your design decisions.

## Background

From the `jsonld-signatures` README:

The default `documentLoader` used by many JSON-LD related libraries is very 
strict for security and content integrity purposes. It will only load locally 
available copies of the context documents that define the terms it uses 
internally. Any attempt to load any other documents (including other contexts) 
will throw an error. If other documents such as verification methods (e.g., 
public key documents), cannot be provided directly to the API and thus need to 
be loaded, a custom document loader must be passed. 
For the sake of clarity, the default document loader will only load locally 
available copies of the following documents:

- https://w3id.org/security/v1
- https://w3id.org/security/v2

To allow other documents to be loaded (such as your JSON-LD contexts), the
developer must construct and pass in a custom `documentLoader` object.

**This library providers a convenient Builder-style API to help construct
document loaders.**

## Usage

```js
const policy = require('loader-policy');

const didKey = require('did-method-key').driver();
const didVeresOne = require('did-veres-one').driver({ /* options */ });

const myCustomContext = require('...'); // Load your own custom context

const documentLoader = policy.allowDidMethod(didKey)
    .allowDidMethod(didVeresOne)
    .allowVcContext()
    .allowContext('https://example.com/context2.json', myCustomContext) // preferable
    .allowWebContext('https://example.com/context1.json') // will be fetched via http
    .create();

// You can now use this documentLoader for vc-js, jsonld-signatures, json-ld
// and other similar libraries.
```

## Contribute

See [the contribute file](https://github.com/digitalbazaar/bedrock/blob/master/CONTRIBUTING.md)!

PRs accepted.

Note: If editing the Readme, please conform to the
[standard-readme](https://github.com/RichardLitt/standard-readme) specification.

## Commercial Support

Commercial support for this library is available upon request from
Digital Bazaar: support@digitalbazaar.com

## License

[New BSD License (3-clause)](LICENSE) © 2020 Digital Bazaar
