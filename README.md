# tiddlywiki-plugin-tiddlywebadapter-browser-storage-sync
A plugin for TiddlyWiki that syncs new or modified tiddlers stored locally by the browser-storage plugin while offline with a TiddlyWeb server, including the Tiddlywiki NodeJS server, when server connection is restored. Using the browser-storage plugin enables syncing local changes even if browser is restarted. 

## Installing
* Install by adding it to the plugins folder of your Node JS TiddlyWiki server. For details, see [tiddlywiki.com](https://tiddlywiki.com/static/Installing%2520custom%2520plugins%2520on%2520Node.js.html) OR
* Open the index.html file in the repo and drag and drop the plugin link to your running TiddlyWiki. 

NOTE: This plugin works in conjunction with the Tiddly Web plugin and the Browser Storage plugin, both of which are required for proper operation. 

## Using
The Browser Storage plugin will only be saving state tiddlers by default. You'll want to update the SaveFilter to include all tiddlers that you want to be in scope for syncing with the server. The second option provided in the Browser Storage plugin's settings tab is a good choice. 

## Limitations
This plugin works by adding any tiddlers found in browser storage to the server when you reconnect. This is a simple mechanism intended only as a backstop to avoid losing data when you are temporarily disconnected from the server. Importantly, it does not maintain a full audit of all actions you've taken while offline and re-apply them, nor does it compare revisions and handle conflicts for tiddlers edited concurrently by multiple users or devices. This means that among other limitations:

* **Deletes are not tracked while disconnected.** If you delete tiddlers previously synced to the server while offline, they will still be on the server after you reconnect.
* **Title changes will result in both new and old tiddlers upon reconnecting.** TiddlyWiki keeps track of tiddlers by title, so the tiddler saved in browser-storage will appear to be a new tiddler when it is synced back to the server. You'll need to delete the tiddler with the old title when you reconnect with the server.

A more complete **disconnected wiki** solution would be NoteSelf, which uses PouchDB and CouchDB to enable full wiki storage locally and robust syncing with the server.
