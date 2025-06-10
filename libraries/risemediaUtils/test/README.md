# Test Risemedia Adapter Locally

## Prerequisities 
1. Set up the prebid js repository as per libraries/risemediaUtils/setup.md file
2. gulp cli 
```bash
npm install gulp-cli -g
```
3. Auction Service & Backend Test Service on Local Machine

## Risemedia Application Set up
1. Create a SSP for prebid testing if not created. The integration type should be direct. Open RTB 2.6 is also supported
2. Subsequently create a SSP Site for prebid js.
3. Keep the ssp_id and site_id handy. Insert the following data into the table "auction_service_configs"
```sql
INSERT INTO public.auction_service_configs
("key", value)
VALUES('prebid_js_site_id', '{INSERT site_id HERE}');
INSERT INTO public.auction_service_configs
("key", value)
VALUES('prebid_ssp_id', '{INSERT ssp_id HERE}');
```
4. Create a publisher for Prebid
5. Create a website within the Publisher

Note: If UI Is not set up in local, then just execute the following queries
```sql
INSERT INTO public.ssps
(id, "name", "domain", website, email, icon, supply_type, rev_share, bcat, badv, bapp, bcrid, include_bidders, exclude_bidders, qps, custom_bid_request_fields, created_at, last_updated, status, supply_chain_entity, supply_chain_seller_id)
VALUES('ssp-ed78652d91ab28b8', 'Prebid Test', 'prebid.org', 'http://localhost:9999/libraries/risemediaUtils/test/test.html', 'prebid@test.com', NULL, 2, 100.0, NULL, NULL, NULL, NULL, NULL, NULL, '{"global":10}'::json, NULL, '2025-05-28 10:32:05.006', '2025-05-28 10:32:05.006', 0, 0, NULL);
INSERT INTO public.ssp_sites
(id, ssp_id, "name", integration_type, rtb_version, request_timeout, bcat, badv, bapp, bcrid, include_bidders, exclude_bidders, qps, floor_price, custom_bid_request_fields, burl, created_at, last_updated, status, vast_tag_config, last_few_results, os_ua_validation)
VALUES('site-c009333dc041368b', 'ssp-ed78652d91ab28b8', 'Prebid JS', 1, '2.6', 500, NULL, NULL, NULL, NULL, NULL, NULL, '{"global":5}'::json, '{"global":1.5,"IND":0.8,"USA":2.5}'::json, NULL, false, '2025-05-28 11:52:59.753', '2025-05-28 11:52:59.753', 0, NULL, false, true);
INSERT INTO public.auction_service_configs
("key", value)
VALUES('prebid_js_site_id', 'site-c009333dc041368b');
INSERT INTO public.auction_service_configs
("key", value)
VALUES('prebid_ssp_id', 'ssp-ed78652d91ab28b8');
INSERT INTO public.publishers
(id, "name", "domain", website, email, icon, api_key, rev_share, iab_categories, app_ads_txt, bcat, badv, bapp, bcrid, created_at, last_updated, status, supply_chain_entity, supply_chain_seller_id)
VALUES('p-be227ed8bfd1d52f', 'Local Prebid', 'localhost:9999', 'http://localhost:9999/libraries/risemediaUtils/test/test.html', 'pub@prebid.com', NULL, 'PyRRGyD7uTFsLz0pw5mI93CbIZp5q17R', 95.0, '{""}', false, NULL, NULL, NULL, NULL, '2025-06-05 12:08:40.427', '2025-06-05 12:08:40.427', 0, 1, '1');
INSERT INTO public.websites
(id, publisher_id, "name", page, "domain", icon, request_timeout, privacy_policy, bcat, badv, bapp, bcrid, iab_categories, keywords, created_at, last_updated, status)
VALUES('w-a5d990f95401b944', 'p-be227ed8bfd1d52f', 'Prebid JS Local HTML', 'http://localhost:9999/libraries/risemediaUtils/test/test.html', 'localhost:9999', NULL, 496, false, NULL, NULL, NULL, NULL, '{IAB1-7}', 'key12', '2025-06-09 04:01:27.267', '2025-06-09 04:01:27.267', 0);
```


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