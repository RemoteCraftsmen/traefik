## Step 1 - Install Homebrew (you should have it already)
`$ /usr/bin/ruby -e “$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

## Step 2 - Install dnsmasq
`brew install dnsmasq`

## Step 3 - Create config folder if it doesn’t already exist
`mkdir -pv $(brew —- prefix)/etc/`

## Step 4 - Configure dnsmasq for *.test
`echo ‘address=/.test/127.0.0.1’ >> $(brew — prefix)/etc/dnsmasq.conf`

## Step 5 - Configure the port for macOS High Sierra
`echo ‘port=53’ >> $(brew —- prefix)/etc/dnsmasq.conf`

## Step 6 - Start dnsmasq as a service so it automatically starts at login
`sudo brew services start dnsmasq`

## Step 7 - Create a dns resolver
`sudo mkdir -v /etc/resolver`
`sudo bash -c ‘echo “nameserver 127.0.0.1” > /etc/resolver/test`

## Step 8 - Verify that all .test requests are using 127.0.0.1
`scutil --dns`

## You should see something like this
```
resolver #8
domain   : test
nameserver[0] : 127.0.0.1
flags    : Request A records, Request AAAA records
reach    : 0x00030002 (Reachable,Local Address,Directly Reachable Address)
```

#### You can also test by using ping
```
ping foo.test
ping anything.test
```
