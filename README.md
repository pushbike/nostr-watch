> this project is alpha! changes are fast and hard. branching model and tests will come with beta. 

Follow me: npub1uac67zc9er54ln0kl6e4qp2y6ta3enfcg7ywnayshvlw9r5w6ehsqq99rx

LN & NIP-05: bread@sandwich.farm 

# nostr-watch 0.1.0

A client-side nostr network status built with Vue3, Pinia, [nostr-tools](https://github.com/fiatjaf/nostr-tools), [nostr-js](https://github.com/jb55/nostr-js) and [nostr-relay-inspector](https://github.com/dskvr/nostr-relay-inspector). Originally forked from [fiatjaf/nostr-relay-registry](http://github.com/fiatjaf/nostr-relay-registry) but ended up being a rewrite.

nostr.watch aggregates data on nostr relays and the network in general to assist users, developers and relay operators. 

Develop branch is deployed to https://next.nostr.watch

## Features
- [x] Real-time relay status 
- [x] Real-time, client-centric latency tests 
- [x] Relay Identities
- [x] Static JSON API for **all** known relays shared via [/relays.json](https://nostr.watch/relays.json)
- [x] Detailed Relay View
- [x] Relay Behavior Analysis
- [x] NIP Checks
- [x] Geo Checks (build-time)
- [x] Favorite Relays 
- [x] Extension Support 
- [x] Nostr signing, individualized relay testing 
- [ ] Lighting Tips to Relay Operators
- [ ] Relay Statistics 
- [ ] Relay Historical Data
- [ ] Discover relays at runtime (currently buildtime, ready to move to runtime with 0.1) 
- [ ] Discover geo at runtime

## Project setup
```
yarn install
```

## Pre-build


### Compiles and hot-reloads for development
Run once or whenever you want to update geo/discover relays 
```
yarn prebuild
```
```
yarn serve
```

### Compiles and minifies for production
_This runs prebuild every time_
```
yarn build
```

### Lints and fixes files
```
yarn lint
```

### Build Docker
```
yarn docker:build
```
