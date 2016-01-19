---
layout: post
title: "boot2docker - Docker Toolbox Mac OS X"
excerpt: "Trying to setup Docker with Vagrant on Mac OS using Docker Toolbox"
tags: [docker, boot2docker, vagrant, macosx]
comments: true
---
<figure>
	<img src="https://c2.staticflickr.com/8/7336/14098888813_1047e39f08.jpg">
	<figcaption><a href="https://www.flickr.com/photos/xmodulo/" title="Picture by Linux Screenshots on Flickr">Picture by Linux Screenshots on Flickr</a>.</figcaption>
</figure>

I am trying to setup Docker with Vagrant on Mac OS using Docker Toolbox.

## 1. Keeps asking for docker password

```
==> default: Syncing folders to the host VM...
    default: The machine you're rsyncing folders to is configured to use
    default: password-based authentication. Vagrant can't script rsync to automatically
    default: enter this password, so you'll likely be prompted for a password
    default: shortly.
    default:
    default: If you don't want to have to do this, please enable automatic
    default: key insertion using `config.ssh.insert_key`.
    default: Rsyncing folder: /Workspace/projectfolder/ => /var/lib/docker/docker_1453133500_23726
docker@127.0.0.1's password:
    default: Rsyncing folder: /Workspace/projectfolder/ => /var/lib/docker/docker_build_2a2a4a6d8df9e0e02790023811cfe9f9
docker@127.0.0.1's password:
```

The default password for the user docker is `tcuser`. I got a little confused since it asked me for the password twice. But obviously since it is the same account `docker@127.0.0.1` as you can see in the last two lines above. You should enter the same password. This answer saved me http://stackoverflow.com/a/24376512/1297190. As mentioned in the answer, this is mentioned in the boot2docker documentation but if you took the Docker Toolbox route you might miss it.

## 2. Finally after Vagrant is up, SSH Exception

After Vagrant is up, I get the following exception:

```
packet_stream.rb:206:in `poll_next_packet': padding error, need 413195797 block 16 (Net::SSH::Exception)
	from /opt/vagrant/embedded/gems/gems/net-ssh-3.0.1/lib/net/ssh/transport/packet_stream.rb:92:in `next_packet'
	from /opt/vagrant/embedded/gems/gems/net-ssh-3.0.1/lib/net/ssh/transport/session.rb:185:in `block in poll_message'
	from /opt/vagrant/embedded/gems/gems/net-ssh-3.0.1/lib/net/ssh/transport/session.rb:180:in `loop'
	from /opt/vagrant/embedded/gems/gems/net-ssh-3.0.1/lib/net/ssh/transport/session.rb:180:in `poll_message'
	from /opt/vagrant/embedded/gems/gems/net-ssh-3.0.1/lib/net/ssh/connection/session.rb:463:in `dispatch_incoming_packets'
	from /opt/vagrant/embedded/gems/gems/net-ssh-3.0.1/lib/net/ssh/connection/session.rb:222:in `preprocess'
	from /opt/vagrant/embedded/gems/gems/net-ssh-3.0.1/lib/net/ssh/connection/session.rb:206:in `process'
	from /opt/vagrant/embedded/gems/gems/net-ssh-3.0.1/lib/net/ssh/
```

Turns out this is because of a timing issue and you can simply ignore this and try

```
vagrant ssh
```

Please share your Docker Toolbox woes in the comments section below. Hope this helps!
	
	