# IPCities
Bringing the age of GeoCities to the world of tomorrow

## How?
By utilizing the [InvArch INV4 protocol](https://github.com/InvArch/InvArch-Frames) to give websites not only Non Fungible characteristics but also distributed fractionalizable ownership.

Oh, and also unlike traditional NFTs, we don't sacrife composability, you can change your website all you want. All thanks to the IPS module from [InvArch's INV4](https://github.com/InvArch/InvArch-Frames)!

## Okay, but what am I supposed to do with these files?
Well it's quite simple, really. You see, as of right now the protocol for project IPCities is barely developed, functionality is limited, but it's still pretty damn cool!

To get started, we'll assume you already know how to use the [InvArch Network](https://github.com/InvArch/InvArch-Node) and are familiar with the concepts, if you aren't, feel free to reach out on the [InvArch discord](https://discord.gg/invarch)!

Now, initially for this proof of concept stage we have 2 files. Let's go through them:

`index.html`

This is where the implementation of the protocol actually lives, we start off by including some code we will need, so let's skip to where the fun code starts.
If you scroll down you'll eventually get to these 2 lonely lines
```js
const ips_id = 3;
const index_ipf_metadata = "homepage.html";
```
In the current version of the protocol we hardcode these values for simplicity, the first has to correspond to the IPS where your website will live, and the second has to match the metadata of the IPF that will be the entry point for your website, in this case we are using the same filename of the IPF.

Then we query that IPS on chain and we run through all the IPFs attached to it looking for one with the same exact metadata as we previously defined.

Once we find it, we grab it's data, convert it to an IPFS CID by attaching 1220 to the start of the hexadecimal hash (and removing the 0x) and then converting to base58 (which gets us a CIDv0).

Having that CID we can then fetch the actual file behind it by going through an IPFS gateway, and we can take that data (which we presume to be HTML) and replace the current page's entire HTML content with the one fetched.

`homepage.html`

This is where your actual website goes, nothing out of the ordinary in here!

And that's it, pretty simple, right?

Of course this protocol will evolve and eventually will have features such as referencing other IPFs on the same IPS without having to use their CID or even IPF ID (we should be able to reference them by metadata content, so we can include them by filename).

You may be asking though, what's the point of this crazy HTML file if my website lives in a separate file? Well let me explain in this next session.

## Great, now I have 2 HTML files, what do i do with them?
You should now be able to mint these 2 files as IPFs (make sure to set your actual website's IPF metadata to the string you set back in the crazy looking HTML file!), then you can create an IPS with them.

Having that done, you are ready to use your website! Just use the CID of your crazy looking HTML file (you can even link it to a normal domain name by using [DNSLink](https://www.dnslink.io/#example-ipfs-gateway)!).

But wait a minute, didn't you say something about full composability? What happens if I want to edit my website? Won't I have to change the CID and thus changing the domain?

## I didn't like my website, let's make some changes...
So you want to make changes, huh? Well that's pretty simple, all you have to do is remove the IPF that represents your actual website, mint your changed version with the same exact metadata as the old one and add this new IPF to the IPS. All while never touching the crazy HTML we were talking about before.

Hopefully now your doubts about the composability are gone, you should realize by now that since you didn't change the crazy HTML file, it kept it's original CID and your website domain doesn't have to change!

But since your website's starting page actually goes through your IPS over at InvArch to resolve what file should become your page, it can grab the latest version you added to the IPS and you don't have to manually reroute anything on IPFS!

## Journey's End
You did it! You built your very own IPCities webpage, now feel free to open an issue in this repository talking about it, I'll be happy to know more about your experience with both InvArch and this humble protocol of mine!
