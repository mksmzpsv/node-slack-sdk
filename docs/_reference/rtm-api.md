---
title: "@slack/rtm-api"
slug: rtm-api
---

<h1 id="classes" class="undefined auto-anchor-strong">Classes</h1>
<h2 id="rtmclient">RTMClient</h2>
<p>An RTMClient allows programs to communicate with the <a href="https://api.slack.com/rtm" title="">Slack Platform's RTM API</a>. This object uses the EventEmitter pattern to dispatch incoming events and has several methods for sending outgoing messages.</p>
<h4>new RTMClient(token, opts)</h4>
<p>Constructs a new instance of the <code>RTMClient</code> class</p>
<strong>Parameters:</strong>
<table>
<thead>
<tr>
<th align="center">Name</th>
<th align="center">Type</th>
<th align="center">Required</th>
<th align="center">Description</th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">token</td>
<td align="center"><code>string</code></td>
<td align="center">✓</td>
<td></td>
</tr>
<tr>
<td align="center">opts</td>
<td align="center"><code><a href="#rtmclientoptions" title="">RTMClientOptions</a></code></td>
<td align="center">✗</td>
<td></td>
</tr>
<tr>
<td align="center">webClient</td>
<td align="center"><code><a href="web-api#webclient" title="">WebClient</a></code></td>
<td align="center">✗</td>
<td align="center">An optional parameter to provide a customized <a href="web-api#webclient">WebClient</a>. Any desired options for the custom client must be set in this parameter (<code>webClient</code>) as they will take precedence over other arguments passed into <code>RTMClient</code>.</td>
<td></td>
</tr>
</tbody>
</table>
<strong>Options:</strong>
<table>
<thead>
<tr>
<th align="center">Name</th>
<th align="center">Type</th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">agent</td>
<td align="center"><code>Agent</code></td>
<td></td>
</tr>
<tr>
<td align="center">autoReconnect</td>
<td align="center"><code>boolean</code></td>
<td></td>
</tr>
<tr>
<td align="center">clientPingTimeout</td>
<td align="center"><code>number</code></td>
<td></td>
</tr>
<tr>
<td align="center">logger</td>
<td align="center"><code>Logger</code></td>
<td></td>
</tr>
<tr>
<td align="center">logLevel</td>
<td align="center"><code>LogLevel</code></td>
<td></td>
</tr>
<tr>
<td align="center">replyAckOnReconnectTimeout</td>
<td align="center"><code>number</code></td>
<td></td>
</tr>
<tr>
<td align="center">retryConfig</td>
<td align="center"><code>RetryOptions</code></td>
<td></td>
</tr>
<tr>
<td align="center">serverPongTimeout</td>
<td align="center"><code>number</code></td>
<td></td>
</tr>
<tr>
<td align="center">slackApiUrl</td>
<td align="center"><code>string</code></td>
<td></td>
</tr>
<tr>
<td align="center">tls</td>
<td align="center"><code>TLSOptions</code></td>
<td></td>
</tr>
<tr>
<td align="center">useRtmConnect</td>
<td align="center"><code>boolean</code></td>
<td></td>
</tr>
</tbody>
</table>
<h3>Fields</h3>
<table>
<thead>
<tr>
<th align="center">Name</th>
<th align="center">Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">activeTeamId</td>
<td align="center"><code>string</code></td>
<td><p>The team ID for the workspace the client is connected to.</p></td>
</tr>
<tr>
<td align="center">activeUserId</td>
<td align="center"><code>string</code></td>
<td><p>The user ID for the connected client.</p></td>
</tr>
<tr>
<td align="center">authenticated</td>
<td align="center"><code>boolean</code></td>
<td><p>Whether or not the client has authenticated to the RTM API. This occurs when the connect method completes, and a WebSocket URL is available for the client's connection.</p></td>
</tr>
<tr>
<td align="center">connected</td>
<td align="center"><code>boolean</code></td>
<td><p>Whether or not the client is currently connected to the RTM API</p></td>
</tr>
</tbody>
</table>
<h3>Methods</h3>
<h4>addOutgoingEvent(awaitReply, type, body)</h4>
<p>Generic method for sending an outgoing message of an arbitrary type. This method guards the higher-level methods from concern of which state the client is in, because it places all messages into a queue. The tasks on the queue will buffer until the client is in a state where they can be sent.</p>
<p>If the awaitReply parameter is set to true, then the returned Promise is resolved with the platform's acknowledgement response. Not all message types will result in an acknowledgement response, so use this carefully. This promise may be rejected with an error containing code=RTMNoReplyReceivedError if the client disconnects or reconnects before receiving the acknowledgement response.</p>
<p>If the awaitReply parameter is set to false, then the returned Promise is resolved as soon as the message is sent from the websocket.</p>
<strong>Parameters:</strong>
<table>
<thead>
<tr>
<th align="center">Name</th>
<th align="center">Type</th>
<th align="center">Required</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">awaitReply</td>
<td align="center"><code>true</code></td>
<td align="center">✓</td>
<td><p>whether to wait for an acknowledgement response from the platform before resolving the returned Promise.</p></td>
</tr>
<tr>
<td align="center">type</td>
<td align="center"><code>string</code></td>
<td align="center">✓</td>
<td><p>the message type</p></td>
</tr>
<tr>
<td align="center">body</td>
<td align="center"><code>object</code></td>
<td align="center">✗</td>
<td><p>the message body</p></td>
</tr>
</tbody>
</table>
<p><strong>Returns</strong> <code>Promise&#x3C;<a href="#rtmcallresult" title="">RTMCallResult</a>></code></p>
<h4>addOutgoingEvent(awaitReply, type, body)</h4>
<strong>Parameters:</strong>
<table>
<thead>
<tr>
<th align="center">Name</th>
<th align="center">Type</th>
<th align="center">Required</th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">awaitReply</td>
<td align="center"><code>false</code></td>
<td align="center">✓</td>
<td></td>
</tr>
<tr>
<td align="center">type</td>
<td align="center"><code>string</code></td>
<td align="center">✓</td>
<td></td>
</tr>
<tr>
<td align="center">body</td>
<td align="center"><code>object</code></td>
<td align="center">✗</td>
<td></td>
</tr>
</tbody>
</table>
<p><strong>Returns</strong> <code>Promise&#x3C;void></code></p>
<h4>disconnect()</h4>
<p>End an RTM session. After this method is called no messages will be sent or received unless you call start() again later.</p>
<p><strong>Returns</strong> <code>Promise&#x3C;void></code></p>
<h4>send(type, body)</h4>
<p>Generic method for sending an outgoing message of an arbitrary type. The main difference between this method and addOutgoingEvent() is that this method does not use a queue so it can only be used while the client is ready to send messages (in the 'ready' substate of the 'connected' state). It returns a Promise for the message ID of the sent message. This is an internal ID and generally shouldn't be used as an identifier for messages (for that, there is <code>ts</code> on messages once the server acknowledges it).</p>
<strong>Parameters:</strong>
<table>
<thead>
<tr>
<th align="center">Name</th>
<th align="center">Type</th>
<th align="center">Required</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">type</td>
<td align="center"><code>string</code></td>
<td align="center">✓</td>
<td><p>the message type</p></td>
</tr>
<tr>
<td align="center">body</td>
<td align="center"><code>object</code></td>
<td align="center">✗</td>
<td><p>the message body</p></td>
</tr>
</tbody>
</table>
<p><strong>Returns</strong> <code>Promise&#x3C;number></code></p>
<h4>sendMessage(text, conversationId)</h4>
<p>Send a simple message to a public channel, private channel, DM, or MPDM.</p>
<strong>Parameters:</strong>
<table>
<thead>
<tr>
<th align="center">Name</th>
<th align="center">Type</th>
<th align="center">Required</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">text</td>
<td align="center"><code>string</code></td>
<td align="center">✓</td>
<td><p>The message text.</p></td>
</tr>
<tr>
<td align="center">conversationId</td>
<td align="center"><code>string</code></td>
<td align="center">✓</td>
<td><p>A conversation ID for the destination of this message.</p></td>
</tr>
</tbody>
</table>
<p><strong>Returns</strong> <code>Promise&#x3C;<a href="#rtmcallresult" title="">RTMCallResult</a>></code></p>
<h4>sendTyping(conversationId)</h4>
<p>Sends a typing indicator to indicate that the user with <code>activeUserId</code> is typing.</p>
<strong>Parameters:</strong>
<table>
<thead>
<tr>
<th align="center">Name</th>
<th align="center">Type</th>
<th align="center">Required</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">conversationId</td>
<td align="center"><code>string</code></td>
<td align="center">✓</td>
<td><p>The destination for where the typing indicator should be shown.</p></td>
</tr>
</tbody>
</table>
<p><strong>Returns</strong> <code>Promise&#x3C;void></code></p>
<h4>start(options)</h4>
<p>Begin an RTM session using the provided options. This method must be called before any messages can be sent or received.</p>
<strong>Parameters:</strong>
<table>
<thead>
<tr>
<th align="center">Name</th>
<th align="center">Type</th>
<th align="center">Required</th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">options</td>
<td align="center"><code><a href="#rtmstartoptions" title="">RTMStartOptions</a></code></td>
<td align="center">✗</td>
<td></td>
</tr>
</tbody>
</table>
<p><strong>Returns</strong> <code>Promise&#x3C;WebAPICallResult></code></p>
<h4>subscribePresence(userIds)</h4>
<p>Subscribes this client to presence changes for only the given <code>userIds</code>.</p>
<strong>Parameters:</strong>
<table>
<thead>
<tr>
<th align="center">Name</th>
<th align="center">Type</th>
<th align="center">Required</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">userIds</td>
<td align="center"><code>string[]</code></td>
<td align="center">✓</td>
<td><p>An array of user IDs whose presence you are interested in. This list will replace the list from any previous calls to this method.</p></td>
</tr>
</tbody>
</table>
<p><strong>Returns</strong> <code>Promise&#x3C;void></code></p>
<h1 id="enums" class="undefined auto-anchor-strong">Enums</h1>
<h2 id="errorcode">ErrorCode</h2>
<p>A dictionary of codes for errors produced by this package</p>
<h3>Members</h3>
<ul>
<li><strong>KeepAliveClientNotConnected</strong></li>
<li><strong>KeepAliveConfigError</strong></li>
<li><strong>KeepAliveInconsistentState</strong></li>
<li><strong>NoReplyReceivedError</strong></li>
<li><strong>SendMessagePlatformError</strong></li>
<li><strong>SendWhileDisconnectedError</strong></li>
<li><strong>SendWhileNotReadyError</strong></li>
<li><strong>WebsocketError</strong></li>
</ul>
<h1 id="interfaces" class="undefined auto-anchor-strong">Interfaces</h1>
<h2 id="codederror">CodedError</h2>
<p>All errors produced by this package adhere to this interface</p>
<h3>Fields</h3>
<table>
<thead>
<tr>
<th align="center">Name</th>
<th align="center">Type</th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">code</td>
<td align="center"><code><a href="#errorcode" title="">ErrorCode</a></code></td>
<td></td>
</tr>
</tbody>
</table>
<h2 id="rtmcallresult">RTMCallResult</h2>
<h3>Fields</h3>
<table>
<thead>
<tr>
<th align="center">Name</th>
<th align="center">Type</th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">error</td>
<td align="center"><code>object</code></td>
<td></td>
</tr>
<tr>
<td align="center">reply_to</td>
<td align="center"><code>number</code></td>
<td></td>
</tr>
<tr>
<td align="center">ts</td>
<td align="center"><code>string</code></td>
<td></td>
</tr>
</tbody>
</table>
<h2 id="rtmclientoptions">RTMClientOptions</h2>
<h3>Fields</h3>
<table>
<thead>
<tr>
<th align="center">Name</th>
<th align="center">Type</th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">agent</td>
<td align="center"><code>Agent</code></td>
<td></td>
</tr>
<tr>
<td align="center">autoReconnect</td>
<td align="center"><code>boolean</code></td>
<td></td>
</tr>
<tr>
<td align="center">clientPingTimeout</td>
<td align="center"><code>number</code></td>
<td></td>
</tr>
<tr>
<td align="center">logger</td>
<td align="center"><code>Logger</code></td>
<td></td>
</tr>
<tr>
<td align="center">logLevel</td>
<td align="center"><code>LogLevel</code></td>
<td></td>
</tr>
<tr>
<td align="center">replyAckOnReconnectTimeout</td>
<td align="center"><code>number</code></td>
<td></td>
</tr>
<tr>
<td align="center">retryConfig</td>
<td align="center"><code>RetryOptions</code></td>
<td></td>
</tr>
<tr>
<td align="center">serverPongTimeout</td>
<td align="center"><code>number</code></td>
<td></td>
</tr>
<tr>
<td align="center">slackApiUrl</td>
<td align="center"><code>string</code></td>
<td></td>
</tr>
<tr>
<td align="center">tls</td>
<td align="center"><code>TLSOptions</code></td>
<td></td>
</tr>
<tr>
<td align="center">useRtmConnect</td>
<td align="center"><code>boolean</code></td>
<td></td>
</tr>
</tbody>
</table>
<h2 id="rtmnoreplyreceivederror">RTMNoReplyReceivedError</h2>
<h3>Fields</h3>
<table>
<thead>
<tr>
<th align="center">Name</th>
<th align="center">Type</th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">code</td>
<td align="center"><code>ErrorCode.NoReplyReceivedError</code></td>
<td></td>
</tr>
</tbody>
</table>
<h2 id="rtmplatformerror">RTMPlatformError</h2>
<h3>Fields</h3>
<table>
<thead>
<tr>
<th align="center">Name</th>
<th align="center">Type</th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">code</td>
<td align="center"><code>ErrorCode.SendMessagePlatformError</code></td>
<td></td>
</tr>
<tr>
<td align="center">data</td>
<td align="center"><code><a href="#rtmcallresult" title="">RTMCallResult</a></code></td>
<td></td>
</tr>
</tbody>
</table>
<h2 id="rtmsendwhiledisconnectederror">RTMSendWhileDisconnectedError</h2>
<h3>Fields</h3>
<table>
<thead>
<tr>
<th align="center">Name</th>
<th align="center">Type</th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">code</td>
<td align="center"><code>ErrorCode.SendWhileDisconnectedError</code></td>
<td></td>
</tr>
</tbody>
</table>
<h2 id="rtmsendwhilenotreadyerror">RTMSendWhileNotReadyError</h2>
<h3>Fields</h3>
<table>
<thead>
<tr>
<th align="center">Name</th>
<th align="center">Type</th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">code</td>
<td align="center"><code>ErrorCode.SendWhileNotReadyError</code></td>
<td></td>
</tr>
</tbody>
</table>
<h2 id="rtmwebsocketerror">RTMWebsocketError</h2>
<h3>Fields</h3>
<table>
<thead>
<tr>
<th align="center">Name</th>
<th align="center">Type</th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">code</td>
<td align="center"><code>ErrorCode.WebsocketError</code></td>
<td></td>
</tr>
<tr>
<td align="center">original</td>
<td align="center"><code>Error</code></td>
<td></td>
</tr>
</tbody>
</table>
<h1 id="type-aliases" class="undefined auto-anchor-strong">Type Aliases</h1>
<h2 id="rtmcallerror">RTMCallError</h2>
<pre><code class="language-ts">RTMWebsocketError | RTMNoReplyReceivedError | RTMSendWhileDisconnectedError | RTMSendWhileNotReadyError
</code></pre>
One of:
<ul>
<li><a href="#rtmwebsocketerror" title=""><code>RTMWebsocketError</code></a></li>
<li><a href="#rtmnoreplyreceivederror" title=""><code>RTMNoReplyReceivedError</code></a></li>
<li><a href="#rtmsendwhiledisconnectederror" title=""><code>RTMSendWhileDisconnectedError</code></a></li>
<li><a href="#rtmsendwhilenotreadyerror" title=""><code>RTMSendWhileNotReadyError</code></a></li>
</ul>
<h2 id="rtmstartoptions">RTMStartOptions</h2>
<pre><code class="language-ts">RTMStartArguments
</code></pre>
One of:
<ul>
<li><code>RTMStartArguments</code></li>
</ul>