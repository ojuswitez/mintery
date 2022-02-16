# Prerequisites

Dependencies required before proceeding to Installation and Run:

- docker-compose
- yarn
- psql (from postgresql, only needed for using the `script/dbconn` script, not a necessity)


# Installation

Before starting the mintery docker-compose setup, we need to first deploy an
NFT contract that will be owned by you.

Run the `script/deploy-contract.bash` script, giving your public tezos key (aka your tz1 address) as first argument, and the corresponding private key as second argument. For example:

```bash
./script/deploy-contract.bash tz1g3coajkc9N77XDy55pVEgBGWspQfYqMiH edsk...
```

# Run

After installation is done, simply call `docker-compose up`.

When docker-compose is up, you can connect to the database with `script/dbconn`

# Brief intro of each component

The following components are run by docker-compose:

- [Peppermint](https://github.com/tzConnectBerlin/peppermint)
- [Que Pasa](https://github.com/tzConnectBerlin/que-pasa)
- A [PostgreSQL](https://www.postgresql.org/docs/13/index.html) database

Peppermint mints NFTs. Que Pasa reads what happens onchain and delivers a representation of
that in the PostgreSQL database.

Peppermint lives in 1 schema in the database: `peppermint`.

Que Pasa lives in 2 schemas in the database:

- `que_pasa`; for tables that aren't directly related to the contract storage values (such as the `levels` table, which just stores some info about what levels have been processed)
- `onchain_mintery`; for tables that are directly related to the contract storage values