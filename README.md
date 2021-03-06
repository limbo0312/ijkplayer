引子：[《回顾&总结：ijkPlayer 直播特性分支》](http://www.ruoxu.me//ijkplayer-liveyy)


### 主要目的：
移动视频直播的需求，一般比较重视的特性和目的，
1. 规避花屏、规避弱网卡顿。只是视频播放最基本的要求了，特别是直播中视频质量息息相关着创收的钱袋子。
2. 直播的秒开。不要太高估用户的耐心，也不要低估产品追求最极致的用户体验的决心。
3. 直播的低延迟。既然直播，互动性占据很大的有趣重要程度。所以以前以视频稳定播放为第一，现在转向了最低延迟播放为第一追求。


### 分支特性：
特性的实现，也都是为着上方的主要目的来的。
1. **规避花屏、规避弱网卡顿**。这点得综合的处理了。规避『花屏』的出现，其实就是在『录制端、中转端、客户端』三处对视频 I、B、P帧编码解码时做『纠错性处理』，不至于出现找不到关键帧 I 的导致花屏。至于卡顿，移动直播在复杂的网络情况下确实难以避免，只能在技术层面动态调整，在『帧率、码率、分辨率』参数间做出折中方案，另外当网络实在糟糕了，则才去优先音频传送，视频画面冻结的思路。
2. 直播的秒开。思路是，a最快拿到第一帧 I帧，b最快将第一张画面渲染到屏幕。这就需要服务器一侧将 gop 进行缓存，在连接建立时第一时间给到。也需要播放端最快获取、解析、渲染上这张画面。所以客户端也需要在几处逻辑中对缓存进行特别的『优先』操作。
3. 直播低延迟。服务器和客户端同时优化多级缓存中的默认时长。其实具体实现时，还需要考虑在网络平均质量、缓存的稳定效率与紧追效率间做出一些折中方案的选择。
4. **紧追效率**。这点金山云直播 sdk 应该是最早做到的。从它的 sdk 注释，以及侦测它的缓存市场参数，可以知道它是采用『维护最佳缓存』方案，就是在 cache 过多时，最快消耗掉缓存，达到紧追视频发生源时间的目的。





---------------

[原 read me txt](https://github.com/Bilibili/ijkplayer)
