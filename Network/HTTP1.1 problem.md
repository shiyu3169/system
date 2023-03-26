only 5-6 http connections can be made on a TCP connections at the same time.

Max Number of default simultaneous persistent connections per server/proxy:

* Firefox 2:  2
* Firefox 3+: 6
* Opera 9.26: 4
* Opera 12:   6
* Safari 3:   4
* Safari 5:   6
* IE 7:       2
* IE 8:       6
* IE 10:      8
* Edge:       6
* Chrome:     6

Multiple TCP connections is not a solution to the problem of HTTP/1 because:
1. it adds infrastructure and maintenance cost
2. Each connection consumes a great chunk of server and client resources
3. Optimization requires specific domain knowledge and more expensive specialists
4. Many other side effects. For example, one of them is higher battery consumption on the mobile devices

Other methods that engineers are using
   
   Make fewer requests
   1. caching
   2. spriting (Image bundling)
   3. CSS & JS Bundling
   4. Critical resources inlining
      * Cons: increased traffic, there will be possibly unused code

