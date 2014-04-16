varnish3to4
===========

Script to assist migrating a VCL file from Varnish 3 to 4.

Currently understands:

V3 | V4
:-- | :--
vcl_fetch | vcl_backend_response
vcl_error | vcl_synth
error code response | return (vcl_synth(code, response))
req.backend | req.backend_hint
req.backend.healthy | std.healthy(backend)
req.grace | -
{bereq,req}.request | {bereq,req}.method
{beresp,obj,resp}.response | {beresp,obj,resp}.reason
remove | unset
return (hit_for_pass) | set beresp.uncacheable = true;<br/>return (deliver);
{client,server}.port | std.port({client,server}.ip)
- | vcl 4.0

Not implemented yet:

V3 | V4
:-- | :--
 | import directors<br/>new xx = directors.yy();<br/>xx.add_backend(ss);<br/>set req.backend_hint = xx.backend()
return (lookup) in vcl_recv | return (hash)
req.* in vcl_backend_response | bereq.*
