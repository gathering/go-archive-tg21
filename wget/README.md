# wget Archive

Captured using basic proceedure outlined in [go-archive-tools](https://github.com/gathering/go-archive-tools)

1. `wget -np -m -p -E -o wget.log https://www.gathering.org/tg21/`
2. `extract_urls.sh | keep_asset_urls.sh | grep gathering.org | download_urls.sh`
3. `extract_urls.sh | keep_asset_urls.sh | grep gathering.org | replace_with_local_urls.sh "/tg21"`
4. Manual cleanup

   - Move `/static` files to `/tg21/static`
   - Add files to list and `cat files.list | replace_with_local_urls.sh "/tg21"`
   - Replace references to static files in js and css files
   - Rename client side script to stop it from running (and triggering non-archived api requests)
