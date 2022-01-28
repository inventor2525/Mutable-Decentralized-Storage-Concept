# What is this?
This is an evolving concept on mutable and replyable decentralized storage

# Motivation

# Existing Methods

# Proposal

Add (a single message?) to DHT? Or Peer exchange? or other overlying protocal:

"get_related(key, n:int, type:str)"
> This would get ‘n’ other keys related to ‘key’ (this could be anything: info hashes, content addresses, message|DID, anything!!!) of a certain type (by convention, anything over n would be considered an attack by that peer, causing them to be dropped), “type” strings would be chosen by the community like port numbers, but could first include as a standard:
- “next” : returns a list of keys of any changes to the content, in sequential order
- “previous” : returns a list of keys for any content this content modified, in reverse sequential order (reverse because remember, only n is requested to prevent spamming, going back further would just require requesting again from the same peer [or others!] for the last key returned)
- “references” : returns a list of addresses for any content this content partly or wholly references without modification. (This could be an official way for scientific sources to inform each other of references without requiring a shared database or direct contact to do that!)
- “replies” : returns a list of addresses to any replies to the content. These could be from anyone, from only your own peer, to others that you are aware of, or even a list of replies you host as a social media service. Every piece of content could be replied to with this… From anyone. And no one would have to host what replies they were not interested in.
- Others could include: likes, dislike, rating, etc. All of those are just content, signed by an identity. (which is it self, content)

Possibly, I would think that, “type” could include, by convention, some sort of filter syntax as well (possibly on top of those base operations and others).

In this way, all chains of mutability can be transversed, and other relationships as well!
