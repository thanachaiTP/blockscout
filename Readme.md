# Deploy blockscout

## 1. Download blockscout
> https://github.com/blockscout/blockscout/releases
```
# wget https://github.com/blockscout/blockscout/archive/refs/tags/v4.1.3-beta.zip
# unzip v4.1.3-beta.zip

Case with Logo

# cp logo.png blockscout-4.1.3-beta/apps/block_scout_web/assets/static/images/.
```

## 2. Change Coin name
```
# vim apps/block_scout_web/priv/gettext/en/LC_MESSAGES/default.po
msgid "ETH"
msgstr "POA"

msgid "Ether"
msgstr "POA" 
```

## 3. Build blockscout
```
# cd blockscout-4.1.3-beta/docker
# docker build --build-arg COIN="POA" -f ./Dockerfile -t blockscout_poa ../
```

## 4. Start PostgreSQL
> change password for postgres

```
# docker-compose up -d postgres
```

## 5. Migrations blockscout
Change environment 
- DATABASE_URL=postgresql
- NETWORK=POA
- SUBNETWORK=Mainnet
- ETHEREUM_JSONRPC_HTTP_URL=https://rpc.xyz.io
- ETHEREUM_JSONRPC_WS_URL=ws://ws.xyz.io
- COIN=POA
- LOGO=/images/logo.png
- LOGO_FOOTER=/images/logo.png

```
# docker-compose up migrations
```

## 6. Start blockscout
Change environment                             
- DATABASE_URL=postgresql
- ECTO_USE_SSL=false                      
- NETWORK=POA                              
- SUBNETWORK=Mainnet
- CHAIN_ID=xx
- ETHEREUM_JSONRPC_HTTP_URL=https://rpc.xyz.io
- ETHEREUM_JSONRPC_WS_URL=ws://ws.xyz.io      
- COIN=POA                                                  
- LOGO=/images/logo.png                     
- LOGO_FOOTER=/images/logo.png              

```
# docker-compose up -d blockscout
```


## 7. Case Change Theme and build new images
```
# vim apps/block_scout_web/assets/css/theme/_variables.scss
@import "base_variables";
// @import "neutral_variables";
@import "poa_variables";
```

