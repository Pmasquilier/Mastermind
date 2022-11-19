---
deck: Mastermind my memory::ReactJS
---

# Custom Hooks

<!-- basicblock-start oid="ObsusrE3mMOvb0MlkpUGXjwq" -->
**What is a custom Hook ?**::
A custom Hook is a JavaScript function whose name starts with ”`use`” and that may call other Hooks.** Building your own Hooks lets you extract component logic into reusable functions.
<!-- basicblock-end -->

For example, `useFriendStatus` below a custom Hook:

```
import { useState, useEffect } from 'react';

function useFriendStatus(friendID) {  
const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```

and we simply use this fonction :

```
function FriendStatus(props) {
  const isOnline = useFriendStatus(props.friend.id);
  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

**Do two components using the same Hook share state?** No. Custom Hooks are a mechanism to reuse _stateful logic_ (such as setting up a subscription and remembering the current value), but every time you use a custom Hook, all state and effects inside of it are fully isolated.

We can also pass informations between hooks :
```
  const [recipientID, setRecipientID] = useState(1);
  const isRecipientOnline = useFriendStatus(recipientID);
```
