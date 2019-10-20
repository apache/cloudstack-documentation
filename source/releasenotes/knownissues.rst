Mentione here:
- custom number protocols will break ACL - that rule and anything that should come after it.
- multi-homed VM will be stuck in expunging state
- DRS might cause CloudStack to observe VM as off, and thus remove it's DNS/DHCP settings from VR, although the VM is happily running (on another host)
- etc?
