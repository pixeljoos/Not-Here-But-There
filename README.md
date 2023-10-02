# Not Here But There

This bookmarklet prevents your status from appearing idle on web-based applications like Microsoft Teams.

## Installation

1. **Visit [This Link](https://pixeljoos.github.io/Not-Here-But-There/) and drag the "Not Here But There" bookmarklet link to your bookmarks bar**.

2. If you don't see your bookmarks bar, make sure it's visible:
   - **Chrome**: Go to the three vertical dots on the top right > Bookmarks > Show bookmarks bar.
   - **Firefox**: Go to the hamburger menu on the top right > Bookmarks > View Bookmarks Toolbar.
   - **Safari**: Go to View in the top menu and select "Show Favorites Bar".

## Usage

1. Navigate to the web-based application (like Microsoft Teams) where you wish to remain active.
2. Click on the "Not Here But There" bookmarklet you just added to your bookmarks bar. 
3. An alert will display, notifying you that "Not Here But There" is activated.
4. To deactivate, simply click the bookmarklet again. An alert will inform you when "Not Here But There" is deactivated.

## Code

```javascript
javascript:(function(){
    if(typeof window.myWakeLock === 'undefined' || window.myWakeLock.released){
        if('wakeLock' in navigator){
            async function requestWakeLock(){
                try{
                    window.myWakeLock=await navigator.wakeLock.request('screen');
                    alert('Not Here But There is activated. \nTo deactivate press the Not Here But There bookmarklet again. \nWARNING: Not Here But There will automatically deactivate if the tab is changed or a new window opens.');
                    document.addEventListener('visibilitychange',async ()=>{
                        if(document.visibilityState==='visible' && window.myWakeLock && !window.myWakeLock.released){
                            await navigator.wakeLock.request('screen');
                        }
                    });
                    window.myWakeLock.addEventListener('release', function(){
                        alert('Not Here But There deactivated');
                    });
                } catch(err){
                    alert('Unable to activate Not Here But There: ' + err.name + ' - ' + err.message);
                }
            }
            requestWakeLock();
        } else {
            alert('Not Here But There is not supported in this browser.');
        }
    } else {
        window.myWakeLock.release();
    }
})();

