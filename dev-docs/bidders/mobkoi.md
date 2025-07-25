---
layout: bidder
title: Mobkoi
description: Mobkoi Bidder Adapter
biddercode: mobkoi
tcfeu_supported: true
dsa_supported: false
gvl_id: 898
usp_supported: false
coppa_supported: false
gpp_sids: tcfeu
schain_supported: false
dchain_supported: false
userId: mobkoiId
media_types: banner
safeframes_ok: false
deals_supported: false
floors_supported: false
fpd_supported: true
pbjs: true
pbs: true
prebid_member: false
multiformat_supported: will-bid-on-one
ortb_blocking_supported: partial
privacy_sandbox: no
sidebarType: 1
---

### Note

The Mobkoi Bidding adapter requires setup and approval before beginning. Please reach out to <platformteam@mobkoi.com> for
more details.

### Bid Params

{: .table .table-bordered .table-striped }
| Path                                        | Scope    | Description                    | Example                               | Type     |
|---------------------------------------------|----------|--------------------------------|---------------------------------------|----------|
| `placementId`                               | required | Mobkoi Provided Placement ID   | `'DF2FFFFF'`                          | `string` |
| `adServerBaseUrl`                           | optional | Mobkoi adserver url (PBS only) | `https://adserver.maximus.mobkoi.com` | `string` |

#### Example Configuration

```js
const adUnits = [
  {
    code: 'banner-ad',
    mediaTypes: {
      banner: { sizes: [[300, 600]] },
    },
    bids: [
      {
        bidder: 'mobkoi',
        params: {
          placementId: '<-- Placement ID provided by Mobkoi -->',
        },
      },
    ],
  },
];

pbjs.que.push(function () {
  pbjs.addAdUnits(adUnits);
});
```

#### User ID Module Integration

For optimal targeting and yield, configure the Mobkoi User ID module alongside the bidder adapter.

**Required modules:** `mobkoiBidAdapter`, `mobkoiIdSystem`, `userId`, `consentManagementTcf`, `tcfControl`

```js
pbjs.que.push(function () {
  // Configuration for enabling the User ID module
  pbjs.setConfig({
    userSync: {
      userIds: [
        {
          name: 'mobkoiId',
          storage: {
            type: 'cookie',
            name: '_mobkoi_id',
            expires: 30, // days
          },
        },
      ],
    },
  });

  pbjs.addAdUnits(adUnits);
});
```

#### User Sync Configuration (Alternative)

Alternatively, enable user sync without the User ID module.

**Required modules:** `mobkoiBidAdapter`, `consentManagementTcf`, `tcfControl`

```js
pbjs.que.push(function () {
  // Configuration for enabling getUserSyncs functionality
  pbjs.setConfig({
    userSync: {
      filterSettings: {
        image: {
          bidders: ['mobkoi'],
          filter: 'include'
        }
      }
    }
  });

  pbjs.addAdUnits(adUnits);
});
```

#### Additional Resources

For comprehensive setup guidelines and detailed integration instructions, visit our [complete integration documentation](https://mobkoi.gitbook.io/docs).
