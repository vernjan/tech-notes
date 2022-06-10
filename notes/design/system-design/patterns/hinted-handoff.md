# Hinted Handoff
- While writing data, if the required node is unreachable, another node can accept writes on its behalf. The write is
  then kept in a local buffer and sent out once the original node is healthy again.
- makes system "always writable"