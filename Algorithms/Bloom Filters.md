# Bloom Filters
A bloom filter is a data structure with many practical applications. It can be found in network routers, databases, and web browsers, just to name a few. 

What are bloom filters? Where are they used?

Abloom filter is a space-efficient probabilistic data structure. It has been around for 50 years. It is used to answer thee question - is this element in the set? A bloom filter would answer with either a "firm no", or a "probably yes". In other words, false positives are possible. That is, the element is not there but bloom filter says it is. While false negative are not possible. That is, the element is there but the bloom filter says it is not. The "probably yes" part is what makes a bloom filter probabilistic. 

As with many things in software engineering, this is a tradeoff. The tradeoff here is this: In exchange for providing a sometimes incorrect false positive answer, a bloom filter consumes a lot less memory than a data structure like a hash table that would provide a perfect answer all the time. If a use case can tolerate some false positives but not any false negatives, a bloom filter could be very useful. And another key point though, we cannot remove an item from a bloom filter. It never forgets. 

Now, let' see how it is used. Many NoSQL databases use Bloom filters to reduce the disk reads for keys that don't exist. With an LSM-tree-based database, searching for a key that doesn't exist requires looking though many files and is very costly. If you would like to learn more about how the LSM tree works, check out this video in the description below. Content delivery networks like Akamai use bloom filters to prevent caching "one-hit-wonders". These are web pages that are only requested once. According to Akamai, 75% of the pages are "one-hit-wonders". Using a Bloom filter to track all the URLs seen and only caching a page on the second request, significantly reduces the caching workload and increases the caching hit rate. Web browsers like Chrome used to use a bloom filter to identify malicious URLs. Any URL was first checked against a Bloom filter. It only performed a more expensive full check of the URL if the Bloom filter returned a "probably yes" answer. This is no longer used however as the number of malicious URLs grows to the millions and a more efficient but complicated solution is needed. Similarly, some password validators use a Bloom filter to prevent users from using weak passwords. Sometimes a strong password would be a victim of a false positive, but in this case, they could just ask the user to come up with another password. These are just some well-known examples. There are many ore applications of the Bloom filter. 

Now let's discuss how a bloom filter works. A critical ingredient to a good bloom filter is some good hash functions. These hash functions should be fast, and they should produce outputs that are evenly and randomly distributed. Collisions are okay as long as they are rate. A bloom filter is a large set of buckets, with each bucket containing a single bit, and they all start with a zero. 

Let's imagine we want to keep track of the food I like. For this example, we will use a bloom filter with 10 buckets labeled from 0 to 9. And we would use three hash functions. Let's start by putting "ribeye" into the bloom filter. The three hash functions return the numbers 1,3, and 4. These would set the buckets at those locations to 1. This can be one in constant time. Next, let's put "potato" into the bloom filter. The hash functions return the numbers 0, 4, and 8 this time. Let's set those bits. 

Now, do I like "ribeye"? Well, we can ask the bloom filter. Since the same input always hashes to the same output, "ribeye" still hashes to the numbers 1, 3, and 4. We check all those buckets, and they are all set to 1. So the bloom filter says "I like ribeye". In this case, it is true. Now, let's see if the bloom filter thinks I like "pork chop". In this case, the hash functions return buckets 0, 5, and 8. And even though buckets 0 and 8 are set to 1, but bucket 5 is 0. In this case, the bloom filter can confidently say "No, I don't like pork chop". 

But how do we get the bloom filter to tell us something is there when it's not? Let's walk through an example. Let's say "lemon" hashes to buckets 1, 4, and 8. Since all those buckets are set to 1, even though I don't like lemon, the bloom filter will return yes in this case, which is a false positive. In real-life applications, the size of the bloom filter is much larger than the example here. We can control how often we see false positives by choosing the correct size for the bloom filter based on the expected number of entries in it. These are tradeoffs between space used and accuracy.