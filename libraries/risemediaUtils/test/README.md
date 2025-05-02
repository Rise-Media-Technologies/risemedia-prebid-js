# Test Risemedia Adapter Locally

## Prerequisities 
1. Set up the prebid js repository as per libraries/risemediaUtils/setup.md file
2. gulp cli 
```bash
npm install gulp-cli -g
```
3. Auction Service & Backend Test Service on Local Machine

## Steps
1. Run the Auction Service & Backend Test Service Locally
2. Build the prebid js project with RM Adapter
```bash
gulp build --modules=risemediatechBidAdapter
```

3. Run
```bash
gulp serve
```



