# Nondominium Odoo Modul

Odoo module (`nondominium_connector`) that integrates the Nondominium decentralized resource-sharing network directly into the Odoo product workflow. Users can publish products from their Odoo inventory to the Nondominium DHT with a single click, making them discoverable and shareable across organizations without leaving the Odoo interface.

This addon is the ERP-native counterpart to the [nondominium-erp-bridge](https://github.com/Sensorica/nondominium-erp-bridge) Python library. While the bridge provides a standalone client with mock data for development and testing, this addon operates on live Odoo product records.

#### Features

- **Gateway configuration** in Settings with connection testing
- **"Sync to Nondominium" button** on the product form — creates a ResourceSpecification and EconomicResource in one action
- **Sync tracking** per product: Holochain action hashes, sync status, and timestamp
- **Nondominium tab** on product form and optional sync column in list view

#### How It Works

```
Odoo Product → nondominium_connector → hc-http-gw → Holochain Conductor → Nondominium DHT
```

The addon calls Nondominium's `zome_resource` coordinator functions via the `hc-http-gw` HTTP gateway using base64url-encoded JSON payloads (RFC 4648, no padding). Field names match the Rust zome types exactly for correct JSON transcoding.

#### Requirements

- Odoo 18.0 (or ERPLibre)
- Running Holochain conductor with the Nondominium hApp
- Running `hc-http-gw` gateway instance
- DNA hash from `hc sandbox call list-apps`
