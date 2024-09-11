
## Brainstorming on expected UX and performance issues after more languages comes on board.
As more languages will get added to the portal, few anticipated challenges will need to be figured out before they surface -

Challenges expected - 


1. More languages will need more font files and hence more HTTP request which is going to impact the rendering time.
1. Font look up time - current implementation, applying fonts on body level all together, If a font for a language comes in last of the array then look up time will increase and hence the text may not render properly for few milli-seconds. which is expected to degrade UX. 
1. In some languages few characters may have common uni-code and may conflict.
1. APP - Size of app will increase significantly

Rough solutions -


1. upgrade to http2
1. merge  fonts
1. apply font in batches based on user
1. use a font which solves the problem



*****

[[category.storage-team]] 
[[category.confluence]] 
