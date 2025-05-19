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
2. Perform a git checkout for the branch "dev-testing-rm-adapter"
3. Build the prebid js project with RM Adapter
```bash
gulp build --modules=risemediatechBidAdapter
```

4. Run
```bash
gulp serve
```

5. Test HTML Page
The server will be running on http://localhost:9999
And the test HTML will be available at the following URL :

http://localhost:9999/libraries/risemediaUtils/test/test.html

6. Open DevTools and check for logs in the console for tracing.

# Unit Testing

1. Run the following command
```bash
gulp test
```
To run the specific risemedia Bid Adapter Unit Test
```bash
gulp test --file "test/spec/modules/risemediatechBidAdapter_spec.js" --nolint
```

2. To generate test coverage
```bash
gulp test-coverage
```

3. To view the test coverage
```bash
gulp view-coverage
```