# Docker Ingress


How it works
----------------

#### TODO


Configure DNS
----------------

#### MacOS X - [Detailed description](dnsmasq-mac-osx.md)

1. Install dnsmasq
```sh
brew install dnsmasq
```

2. Startup service
```sh
sudo cp $(brew list dnsmasq | grep dnsmasq.plist) /Library/LaunchDaemons/
sudo launchctl bootstrap system /Library/LaunchDaemons/homebrew.mxcl.dnsmasq.plist
```

3. Configure hostname
```sh
sudo echo 'address=/myhost/127.0.0.1' > /opt/homebrew/etc/dnsmasq.d/myhost.conf
```

4. Configure your resolver to use dnsmasq only for myhost domains
```sh
sudo echo 'nameserver 127.0.0.1' > /etc/resolver/myhost
```

5. Restart dnsmasq and flush local dns cache
```sh
sudo launchctl stop homebrew.mxcl.dnsmasq
sudo launchctl start homebrew.mxcl.dnsmasq
sudo killall -HUP mDNSResponder
```

6. Testing
```sh
ping -c 2 any.my.subdomain.in.myhost
```