# Loudmouth 
<a href="http://groups.google.com/group/loudmouth-dev/">Loudmouth</a> is an async XMPP library written in C.

Example usage:
```Io
acc := Loudmouth with("user@server.com", "super password") do(
  handleConnect = method(
    "Connected!" println)

  handleMessage = method(msg
    "#{msg from} > #{msg plainBody}" println
    body :=  msg plainBody

    if(body indexOf("#") == 0,
      body = doString(body) asString)

    # This way you can manipulate
    # XML nodes with SGML addon
    XmppChatMessage create\
      setPlainBody(body)\
      setTo(msg from)\
      sendVia(self)

    # or simply send the message (must be a Sequence)
    # (this is obviously faster)
    #self send(msg from, body))
)

acc connect
# Any Io code after this line won't be executed
# (unless called as Loudmouth callback or run in separate thread)
Loudmouth startMainLoop
```

# Installation
`loudmouth` should be installed and foundable in your system. Then:
```
eerie install https://github.com/IoLanguage/Loudmouth.git
```
