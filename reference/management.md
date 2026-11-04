# Management and automation

## Choosing an interface

Check the version-specific manual for supported options, such as the web interface, MQTT, metrics, events, or other documented interfaces. The Zigbee Hub MQTT API and the general SLZB-OS MQTT API are not interchangeable; confirm the version, mode, topics, and authentication before use. The supplied documentation places the general MQTT API at version 3.2.4 and later, but specific features may require newer versions.

The web interface's internal API is not a stable public contract. If an operation has no documented interface for the installed version, state that and suggest an available official procedure; do not guess endpoints, parameters, or return semantics.

Restrict management access to a trusted network and protect credentials and keys. Confirm that the version supports TLS before transmitting secrets; if it does not, consider an appropriate secure tunnel instead of exposing the interface directly to the internet.

## Ansible automation

Ansible is one automation option, not a requirement. First identify the documented management method and where the modules will run; do not assume SSH access to the device. Compare actual and desired state when the interface allows it, store secrets with an appropriate mechanism, and keep them out of logs. Explicitly state any idempotency, check-mode, and recovery limitations that cannot be verified.

Obtain confirmation before applying changes and test first in an isolated environment or on an authorized device. After applying a change, read the state again when possible; an accepted request does not prove that the change worked.

Without a reliable state read, do not claim idempotency or post-change verification. Ansible check mode alone does not guarantee that an API has no side effects.

Source: [Manufacturer MQTT API](https://smlight.tech/support/manuals/books/slzb-os/page/mqtt-api) and the official documentation for the installed version.
