This is an evolving concept on versioned mutable and replyable decentralized storage.

*(Skip to [proposal](#proposal))*
# Purpose
The purpose of this is to provide a means for anyone to reply to any piece of content, with future versions or (dis)similar content of any form, using the existing peer discovery methods already used in **trackerless** torrents, IPFS, and others.

*(Trackers can of course be optionally used too.)*

A result of this **may** be to "invert" web indexing so that it is outward from content of interest, rather than top down: which (lacking a central entity) must index all content in order to find all references to a single content. -- This would make search, into a filter and trust problem only.

> For the purposes of this proposal, mutable and replyable will be taken as roughly the same thing, and content will mean ANY content: This could be social media replies. It could mean likes, dislikes, or reviews, signed by a cryptographic identity. It could mean videos or photos. It could mean edits or "forks" of content (educational, encyclopedic, blog, anything!). It could mean user id's and bio's, or encrypted personal browsing history. Anything!
> 
> Additionally, a peer will be taken as any person or computer interested in some content or related content.

# Motivation
Centralized social media and search engines have proven themselves to be very bias, and even limited in their view of the world. Even decentralization systems can fail if an artificial consensus mechanism fails to capture the needs of a minority voice. This needs to be improved ever more, because every time that bias shows, it fragments the greater community, causing further isolation and tension.

Additionally: We can not keep loosing our history! Archival must be done on a much larger scale, in a way that is still fully interactable and relatable with the current content, as though it were the original!

Finally: The content relations that people share must be discoverable with much less energy and effort, without the risk that a centralized entity can then choose to censor (or down rank!!!) that content, more effectively so than any other without that being desired by the individual user in question.

# Cause
> Thoughts on how the problem this is meant to solve persists.

Bias does not have to be human bias or malicious, it can be and sometimes is very systematic. Only a few percent of the "web" is actually indexed (reference) and what is, is now long since done with priority on search results that pay most.

The latter is understandable from an economics standpoint, but it is not as necessary as it would first appear, and it can be done with much less. On all sides!!! -- This would ultimately serve massively many more people if true!

In reality, the failure of the markets to realize this, is stifling economic growth.

For instance:
> In researching FPGA's (as one very small example!), there is a lot of introductory educational material and products that will come up in the maker community fairly quickly in most search results, but there is also still a rather large amount of content in the more middle to advanced level that is very hard to find given current search results. Number of quality results do not relate to quality of search phrase, but rather deals made with search providers, popularity, undisclosed metrics, and identicalness to the then unknown content you would hope to find.
> 
> All who are reading this, likely know this at heart!!! I can list dozens of technical and non technical examples like this, but this one comes from a very well paid industry, researched in English and in the United States, not stopping or giving up early, and researched for months on end. I can not even imagine how bad it would be in under served languages and communities!

Such biases are in no small part the fault of the fact that indexing the web, while it is frequently regarded as a "solved" problem, and has indeed helped society a great deal for the most part... Is VERY slow and expensive to do well. It can take months (reference about Archive.org!!) to scan the current 'version' of the internet. So slow that in many cases, pages disappear before you get to them if you are a single entity doing the archival or indexing. Even if you are as determined as can be.

This means that any "decentralized" social media or storage replacement, must either:
1. Suffer the non-discoverability of the replies to content (given the time taken to FIND them)
2. Build **very** computationally or memory inefficient consensus mechanisms to facilitate discoverability, within any of a frequently very limited sized communities suffering from massively many similar but nearly incompatible implementations (eg, blockchains).
3. Rely on a central entity still, to facilitate the descoverability by hosting the relationships held between pieces of content. -- Whether those pieces of content are held decentrally or not.

Additionally, as a search provider, you have to sufficiently understand the content to understand it's relations to other content.

These combined make search a very resource intensive task, to do well!

This causes us to have to rely on centralized entities for social media, because if they house the content, they don't have to go connect it all, and not even the very best of search engines can compete with that. It also however gives them too much control, that no-one but them really likes. Even those who would seek to pay for that opportunity to control, compete with each other!

# Existing Methods
## Decentralized Methods
### 1) Non Cryptography Content Addressed:
Without an algorithmically cleaver way to address content, in a way that lets a computer intelligently choose which peers get which information about other peers, that they can then use to find each other themselves efficiently: Peers can not effectively find each other without central entity(s) on top of them to manage their connectivity. This can be broken up hierarchically to better serve yes, but it leaves you with a technical requirement that there are less so called trackers than their are peers, which means that there is a greater ability of the network to ignore content of minority interest, than the world it self. This ultimately does raise everyone, but the feeling it creates in the lesser served ever widens. Peer discovery for related content is the only problem here.

Content addressing is 1 such cleaver way to discover peers. (Not just a means to name files!)

### 2) Cryptography Content Addressed:
Existing decentralized content addressed storage methods (such as BitTorrent!) are IMMUTABLE. This means that they can not be changed after the fact, because the content it self is used to generate an address of the content using a hash function. Changing the content, means changing it's location that everyone would hope to find it at.

The hash function chosen is designed with the advantage of making it easier for computers to find others with the same content (or a desire for it!) very efficiently! This makes sharing very possible, fast, decentralized, and unstoppable, but it makes that content impossible to link to newer related content without an additional system to facilitate it.

A new system to facilitate such linking, from the peers interested in the original content themselves, is what is proposed here. First however, we will look at other existing methods.

(TODO)
### Note:
> This is NOT the same problem as giving that content a name that a human can remember!
> 
> Although some solutions have chosen to solve that problem together with mutability, they are not required to be solved together, and the later is quite easy to do with existing systems or others (optionally such as IP based DNS and HTTP, or a blockchain [or multiple!]).
> 
> Additionally, if mutability were fully solved, implementing a mapping of human readable name to content address, and storing that decentrally, would be trivial.

# Proposal
## Part 1
*Content Relation Sharing*

Add a single message & reply to facilitate passing of related content addresses or supporting URIs between peers.

This could possibly be part of DHT's or PEX, to facilitate mutable torrents, and others in one swoop. Or added as a second thin protocol, post peer discovery.

Eg:
```python
class ContentAddress()...

def get_related(
	key:ContentAddress, n:int,
	relation_type:str
) -> List[ContentAddress]: ...
```
This would get at most 'n' other keys related to 'key' of a certain type of relationship_type.

- 'key' could be anything. -- Info hashes, content addresses, message|DID, anything!
- By convention, anything over 'n' could be considered an attack by that peer, causing them to be dropped.
- "relation_type" strings would be chosen by the community like port numbers, but could first include as a standard:
> - "next" : returns a list of keys of any changes to the content, in sequential order, either by that peer or that that peer is aware of.
> - "previous" : returns a list of keys for any content this content modified, in reverse sequential order (reverse because remember, only n is requested to prevent spamming, going back further would just require requesting again from the same peer [or others!] for the last key returned)
> - "references" : returns a list of keys for any content this content partly or wholly references without modification. (This could be a new way for scientific sources to inform each other of references without requiring a shared database or direct contact to do that!)
> - "replies" : returns a list of keys to any replies to the content. These could be from anyone, from only your own peer, to others that you are aware of, or even a list of replies of others you host as a social media service, chat section, forum, or email. Every piece of content could be replied to with this… From anyone. And no one would have to host what replies they were not interested in. Reply content could be encrypted or public.
> - "children" or "parent" : Directed Graph data structures
> - "archive" : Think of this like returning a git pack file. An efficient file compression of all versions of text or code for a thing.
> - "signature" : facilitates any third party signing a piece of content.
> > - Others could include: likes / dislike, rating, etc. All of those are just content, signed by an identity. (which is it self, content)

I would think that, "type" could include, by convention, some sort of filter syntax as well (possibly on top of those base operations and others), but what that looks like or why I'll leave to the reader.

In this way, all content DAGs can be transversed, mutably, using what ever relationships the community wishes to specify.

## Part 2
*Developing Trust in Peers*

??
(TODO)