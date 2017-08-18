# DB-doc
Readings in Databases, BigData

A list of papers essential to understanding databases and building new data systems. 
<br>
The list is curated and maintained by BlueseaLi, but it came from Reynold Xin (@rxin, https://github.com/rxin/db-readings) initally. 
<br>
BlueseaLi added some new documents. 
<br>
If you think a paper should be part of this list, please submit a pull request. It might take a while since I need to go over the paper.

If you are reading this and taking the effort to understand these papers, we would love to talk to you about opportunities at Databricks.
<br>

<h2><a id="user-content-table-of-contents" class="anchor" href="#table-of-contents" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a><a name="user-content-TOC">Table of Contents</a></h2>
<ol>
<li><a href="#basic-and-algo">Basics and Algorithms</a></li>
<li><a href="#essentials">Essentials of Relational Databases</a></li>
<li><a href="#essentials">Query Optimizer</a></li>
<li><a href="#essentials">Transaction</a></li>
<li><a href="#system-design">Classic System Design</a></li>
<li><a href="#column">Relational database: Row and Columnar store</a></li>
<li><a href="#data-parallel">Data-Parallel Computation</a></li>
<li><a href="#data-parallel">Distributed database</a></li>
<li><a href="#consensus">Consensus and Consistency</a></li>
<li><a href="#trends">Trends (Cloud Computing, Warehouse-scale Computing, New Hardware)</a></li>
<li><a href="#misc">Miscellaneous</a></li>
<li><a href="#external">External Reading Lists</a></li>
</ol>
<h2><a id="user-content--basics-and-algorithms" class="anchor" href="#-basics-and-algorithms" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a><a name="user-content-basic-and-algo"> Basics and Algorithms</a></h2><a name="user-content-basic-and-algo">
</a><ul><a name="user-content-basic-and-algo">
</a><li><a name="user-content-basic-and-algo">
</a><p><a name="user-content-basic-and-algo"></a><a href="http://research.microsoft.com/en-us/um/people/gray/5_min_rule_sigmod.pdf">The Five-Minute Rule Ten Years Later, and Other Computer Storage Rules of Thumb</a> (1997): This paper (and the original one proposed 10 years earlier) illustrates a quantitative formula to calculate whether a data page should be cached in memory or not. It is a delight to read Jim Gray approach to an array of related problems, e.g. how big should a page size be.</p>
</li>
<li>
<p><a href="http://research.microsoft.com/en-us/um/people/gray/papers/AlphaSortSigmod.pdf">AlphaSort: A Cache-Sensitive Parallel External Sort</a> (1995): Sorting is one of the most essential algorithms in databases, as it is used to do joins, aggregations, and sorts. In algorithms 101 class, CS students are asked to reason about big O complexity and ignore the constant factor. In practice, however, the change in constant from L2 cache can be as big as two or three orders of magnitude. This is a good paper to learn about all the tricks fast sorting implementations use.</p>
</li>
<li>
<p><a href="http://research.microsoft.com/pubs/209622/patsort-sigmod14.pdf">Patience is a Virtue: Revisiting Merge and Sort on Modern Processors</a> (2014): Sorting revisited. Actually also a good survey on sorting algorithms used in practice and their trade-offs.</p>
</li>
</ul>
<h2><a id="user-content--essentials-of-relational-databases" class="anchor" href="#-essentials-of-relational-databases" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a><a name="user-content-essentials"> Essentials of Relational Databases</a></h2><a name="user-content-essentials">
</a><ul><a name="user-content-essentials">
</a><li><a name="user-content-essentials">
</a><p><a name="user-content-essentials"></a><a href="http://db.cs.berkeley.edu/papers/fntdb07-architecture.pdf">Architecture of a Database System</a> (2007): Joe Hellerstein's great overview of relational database systems. This essay walks readers through all components essential to relational database systems.</p>
</li>
<li>
<p><a href="http://www.cs.berkeley.edu/%7Erxin/db-papers/Relational-Model-Codd.pdf">A Relational Model of Data for Large Shared Data Banks</a> (1970): Codd's argument for data independence (from 1970), a fundamental concept in relational databases. Despite the current NoSQL trend, I believe ideas from this paper are becoming increasingly important in massively parallel data systems.</p>
</li>
<li>
<p><a href="http://www.cs.berkeley.edu/%7Erxin/db-papers/ARIES.pdf">ARIES: A Transaction Recovery Method Supporting Fine-Granularity Locking and Partial Rollbacks Using Write-Ahead Logging</a> (1992): The first algorithm that actually works: it supports concurrent execution of transactions without losing data even in the presence of failures. This paper is very hard to read because it mixes a lot of low level details in the explanation of the high level algorithm. Perhaps try understand ARIES (log recovery) by reading a database textbook before attempting to read this paper.</p>
</li>
<li>
<p><a href="http://www.cs.berkeley.edu/%7Erxin/db-papers/B-tree.pdf">Efficient Locking for Concurrent Operations on B-Trees</a> (1981) and The <a href="http://www.cs.berkeley.edu/%7Erxin/db-papers/R-tree.pdf">R*-tree: An Efficient and Robust Access Method for Points and Rectangles</a> (1990): B-Tree is a core data structure in databases (not just relational). It is optimized and has a low read amplification factor for random lookups of on-disk data. R-tree is an extension of B-tree to support lookups of multi-dimensional data, e.g. geodata.</p>
</li>
<li>
<p><a href="http://www.cs.duke.edu/courses/spring03/cps216/papers/oneil-quass-1997.pdf">Improved Query Performance with Variant Indexes</a> (1997): Analytical databases and OLTP databases require different trade-offs. These are reflected in the choices of indexing data structures. This paper talks about a number of index data structures more suitable for analytical databases.</p>
</li>
<li>
<p><a href="http://www.cs.berkeley.edu/%7Erxin/db-papers/OCC-Optimistic-Concurrency-Control.pdf">On Optimistic Methods for Concurrency Control</a> (1981): There are two ways to support concurrency. The first is the pessimistic way, i.e. to lock shared data preemptively. This paper explains an alternatively to locking called Optimistic Concurrency Control. Optimistic approaches assume conflicts are rare and executes transactions without acquiring locks. Before committing the transactions, the database system checks for conflicts and aborts/restarts transactions if conflicts arise.</p>
</li>
<li>
<p><a href="http://www.cs.berkeley.edu/%7Erxin/db-papers/SystemR-Optimizer.pdf">Access Path Selection in a Relational Database Management System</a> (1979): The basics of query optimization. SQL is declarative, i.e. you specify using a query language what data you want, not how you want it. There are usually multiple ways (query plans) of executing a query. The database system examines multiple plans and decides on an optimal one (best-effort). This process is called query optimization. The traditional way of doing query optimization is to have a cost-model for different access methods and query plans. This paper explains the cost-model and a dynamic programming algorithm to pick the best plan.</p>
</li>
<li>
<p><a href="http://www.cs.berkeley.edu/%7Erxin/db-papers/Eddies.pdf">Eddies: Continuously Adaptive Query Processing</a> (2000): Traditional query optimization (and the cost model used) is static. There are two problems with the traditional model. First, it is hard to build the cost model absent of data statistics. Second, query execution environment might change in long running queries and a static approach cannot capture the change. Analogous to fluid dynamics, this paper proposes a set of techniques that optimize query execution dynamically. I don't think ideas in Eddies have made their way into commercial systems yet, but the paper is very refreshing to read and might become more important now.</p>
</li>
</ul>
<h2><a id="user-content--classic-system-design" class="anchor" href="#-classic-system-design" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a><a name="user-content-system-design"> Classic System Design</a></h2><a name="user-content-system-design">
</a><ul><a name="user-content-system-design">
</a><li><a name="user-content-system-design">
</a><p><a name="user-content-system-design"></a><a href="http://www.cs.ubc.ca/%7Erap/teaching/504/2010/readings/history-of-system-r.pdf">A History and Evaluation of System R</a> (1981): There were System R from IBM and Ingres from Berkeley, two systems that showed relational database was feasible. This paper describes System R. It is impressive and scary to note that the internals of relational database systems in 2012 look a lot like System R in 1981.</p>
</li>
<li>
<p><a href="http://research.google.com/archive/gfs.html">The Google File System</a> (2003) and <a href="http://research.google.com/archive/bigtable.html">Bigtable: A Distributed Storage System for Structured Data</a> (2006): Two core components of Google's data infrastructure. GFS is an append-only distributed file system for large sequential reads (data-intensive applications). BigTable is high-performance distributed data store that builds on GFS. One way to think about it is that GFS is optimized for high throughput, and BigTable explains how to build a low-latency data store on top of GFS. Some of these might have been replaced by newer proprietary technologies internal to Google, but the ideas stand.</p>
</li>
<li>
<p><a href="http://www.cs.berkeley.edu/%7Erxin/db-papers/Chord-DHT.pdf">Chord: A Scalable Peer-to-peer Lookup Service for Internet Applications</a> (2001) and <a href="http://www.cs.berkeley.edu/%7Erxin/db-papers/Dynamo.pdf">Dynamo: Amazon’s Highly Available Key-value Store</a> (2007): Chord was born in the days when distributed hash tables was a hot research. It does one thing, and does it really well: how to look up the location of a key in a completely distributed setting (peer-to-peer) using consistent hashing. The Dynamo paper explains how to build a distributed key-value store using Chord. Note some design decisions change from Chord to Dynamo, e.g. finger table O(logN) vs O(N), because in Dynamo's case, Amazon has more control over nodes in a data center, while Chord assumes peer-to-peer nodes in wide area networks.</p>
</li>
</ul>
<h2><a id="user-content--columnar-databases" class="anchor" href="#-columnar-databases" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a><a name="user-content-column"> Columnar Databases</a></h2><a name="user-content-column">
<p>Columnar storage and column-oriented query engine are critical to analytical workloads, e.g. OLAP. It's been almost 15 years since it first came out (the MonetDB paper in 1999), and almost every commercial warehouse database has a columnar engine by now.</p>
</a><ul><a name="user-content-column">
</a><li><a name="user-content-column">
</a><p><a name="user-content-column"></a><a href="http://www.cs.berkeley.edu/%7Erxin/db-papers/C-Store.pdf">C-Store: A Column-oriented DBMS</a> (2005) and <a href="http://vldb.org/pvldb/vol5/p1790_andrewlamb_vldb2012.pdf">The Vertica Analytic Database: C-Store 7 Years Later</a> (2012): C-Store is an influential, academic system done by the folks in New England. Vertica is the commercial incarnation of C-Store.</p>
</li>
<li>
<p><a href="http://db.csail.mit.edu/projects/cstore/abadi-sigmod08.pdf">Column-Stores vs. Row-Stores: How Different Are They Really?</a> (2012): Discusses the importance of both the columnar storage and the query engine.</p>
</li>
<li>
<p><a href="http://research.google.com/pubs/pub36632.html">Dremel: Interactive Analysis of Web-Scale Datasets</a> (2010): A jaw-dropping paper when Google published it. Dremel is a massively parallel analytical database used at Google for ad-hoc queries. The system runs on thousands of nodes to process terabytes of data in seconds. It applies columnar storage to complex, nested data structures. The paper talks a lot about the nested data structure support, and is a bit light on the details of the query execution. Note that a number of open source projects are claiming they are building "Dremel". The Dremel system achieves low-latency through massive parallelism and columnar storage, so the model doesn't necessarily make sense outside Google since very few companies in the world can afford thousands of nodes for ad-hoc queries.</p>
</li>
</ul>
<h2><a id="user-content--data-parallel-computation" class="anchor" href="#-data-parallel-computation" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a><a name="user-content-data-parallel"> Data-Parallel Computation</a></h2><a name="user-content-data-parallel">
</a><ul><a name="user-content-data-parallel">
</a><li><a name="user-content-data-parallel">
</a><p><a name="user-content-data-parallel"></a><a href="http://research.google.com/archive/mapreduce.html">MapReduce: Simplified Data Processing on Large Clusters</a> (2004): MapReduce is both a programming model (borrowed from an old concept in functional programming) and a system at Google for distributed data-intensive computation. The programming model is so simple yet expressive enough to capture a wide range of programming needs. The system, coupled with the model, is fault-tolerant and scalable. It is probably fair to say that half of the academia are now working on problems heavily influenced by MapReduce.</p>
</li>
<li>
<p><a href="http://www.cs.berkeley.edu/%7Erxin/db-papers/Spark.pdf">Resilient Distributed Datasets: A Fault-Tolerant Abstraction for In-Memory Cluster Computing</a> (2012): This is the research paper behind the Spark cluster computing project at Berkeley. Spark exposes a distributed memory abstraction called RDD, which is an immutable collection of records distributed across a cluster's memory. RDDs can be transformed using MapReduce style computations. The RDD abstraction can be orders of magnitude more efficient for workloads that exhibit strong temporal locality, e.g. query processing and iterative machine learning. Spark is an example of why it is important to separate the MapReduce programming model from its execution engine.</p>
</li>
<li>
<p><a href="https://amplab.cs.berkeley.edu/publication/shark-sql-and-rich-analytics-at-scale/">Shark: SQL and Rich Analytics at Scale</a> (2013): Describes the Shark system, which is the SQL engine built on top of Spark. More importantly, the paper discusses why previous SQL on Hadoop/MapReduce query engines were slow.</p>
</li>
<li>
<p><a href="http://static.googleusercontent.com/media/research.google.com/en//archive/spanner-osdi2012.pdf">Spanner</a> (2012): Spanner is "a scalable, multi-version, globally distributed, and synchronously replicated database". The linchpin that allows all this functionality is the TrueTime API which lets Spanner order events between nodes without having them communicate. <a href="http://www.cse.buffalo.edu/%7Edemirbas/publications/augmentedTime.pdf">There is some speculation that the TrueTime API is very similar to a vector clock but each node has to store less data</a>. Sadly, a paper on TrueTime is promised, but hasn't yet been released.</p>
</li>
</ul>
<h2><a id="user-content--consensus-and-consistency" class="anchor" href="#-consensus-and-consistency" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a><a name="user-content-consensus"> Consensus and Consistency</a></h2><a name="user-content-consensus">
</a><ul><a name="user-content-consensus">
</a><li><a name="user-content-consensus">
</a><p><a name="user-content-consensus"></a><a href="http://research.microsoft.com/en-us/um/people/lamport/pubs/paxos-simple.pdf">Paxos Made Simple</a> (2001): Paxos is a fault-tolerant distributed consensus protocol. It forms the basis of a wide variety of distributed systems. The idea is simple, but notoriously difficult to understand (perhaps due to the way the original Paxos paper was written).</p>
</li>
<li>
<p><a href="https://ramcloud.stanford.edu/wiki/download/attachments/11370504/raft.pdf">The Raft Consensus Algorithm</a> (2014) : Raft is a consensus algorithm designed as an alternative to Paxos. It was meant to be more understandable than Paxos by means of separation of logic, but it is also formally proven safe and offers some new features.[1] Raft offers a generic way to distribute a state machine across a cluster of computing systems, ensuring that each node in the cluster agrees upon the same series of state transitions.</p>
</li>
<li>
<p><a href="http://www.computer.org/cms/Computer.org/ComputingNow/homepage/2012/0512/T_CO2_CAP12YearsLater.pdf">CAP Twelve Years Later: How the "Rules" Have Changed</a> (2012): The CAP theorem, proposed by Eric Brewer, asserts that any net­worked shared-data system can have only two of three desirable properties: Consistency, Availability, and Partition-Tolerance. A number of NoSQL stores reference CAP to justify their decision to sacrifice consistency. This is Eric Brewer's writeup on CAP in retrospective, explaining "'2 of 3' formulation was always misleading because it tended to oversimplify the tensions among properties."</p>
</li>
</ul>
<h2><a id="user-content--trends-cloud-computing-warehouse-scale-computing-new-hardware" class="anchor" href="#-trends-cloud-computing-warehouse-scale-computing-new-hardware" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a><a name="user-content-trends"> Trends (Cloud Computing, Warehouse-scale Computing, New Hardware)</a></h2><a name="user-content-trends">
</a><ul><a name="user-content-trends">
</a><li><a name="user-content-trends">
</a><p><a name="user-content-trends"></a><a href="http://www.cs.berkeley.edu/%7Erxin/db-papers/cloudcomputing.pdf">A View of Cloud Computing</a> (2010): This is THE paper on Cloud Computing. This paper discusses the economics and obstacles of cloud computing (referring to the elasticity of resources, not the consumer-facing "cloud") from a technical perspective. The obstacles presented in this paper will impact design decisions for systems running in the cloud.</p>
</li>
<li>
<p><a href="http://www.cs.berkeley.edu/%7Erxin/db-papers/WarehouseScaleComputing.pdf">The Datacenter as a Computer: An Introduction to the Design of Warehouse-Scale Machines</a>: Google's Luiz André Barroso and Urs Hölzle explains the basics of data center hardware and software for warehouse-scale computing. There is an <a href="http://dl.acm.org/citation.cfm?id=2019527&amp;bnc=1">accompanying video</a>. The video talks about the importance of cutting long-tail latency in massively parallel systems. The other key idea is the disaggregation of resources. Technologies such as GFS/HDFS already disaggregate disks because of high network bandwidth, but yet to see the same trend applying to DRAMs because that'd require low-latency networking.</p>
</li>
</ul>
<h2><a id="user-content--miscellaneous" class="anchor" href="#-miscellaneous" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a><a name="user-content-misc"> Miscellaneous</a></h2><a name="user-content-misc">
</a><ul><a name="user-content-misc">
</a><li><a name="user-content-misc">
</a><p><a name="user-content-misc"></a><a href="http://www.cs.berkeley.edu/%7Erxin/db-papers/TrustingTrust-Thompson.pdf">Reflections on Trusting Trust</a> (1984): Ken Thompson's Turing Award acceptance speech in 1984, describing black box backdoor issues and pointing out trust is not absolute.</p>
</li>
<li>
<p><a href="http://people.cs.umass.edu/%7Eyanlei/courses/CS691LL-f06/papers/SH05.pdf">What Goes Around Comes Around</a>: Michael Stonebraker and Joseph M. Hellerstein provide a summary of 35 years of data model proposals, grouped into 9 different eras. The paper discusses the proposals of each era, and show that there are only a few basic data modeling ideas, and most have been around a long time. Later proposals inevitably bear a strong resemblance to certain earlier proposals.</p>
</li>
</ul>
<h2><a id="user-content--external-reading-lists" class="anchor" href="#-external-reading-lists" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a><a name="user-content-external"> External Reading Lists</a></h2><a name="user-content-external">
<p>A number of schools have their own reading lists for graduate students in databases.</p>
</a><ul><a name="user-content-external">
</a><li><a name="user-content-external">Berkeley </a><a href="http://www.eecs.berkeley.edu/GradAffairs/CS/Prelims/db.html">PhD prelim exam reading list</a> and <a href="http://www.cs286.net/home/reading-list">CS286 grad database class reading list</a></li>
<li><a href="http://www.cs.brown.edu/courses/cs227/papers.html">Brown CSCI 2270 Advanced Topics in Database Management</a></li>
<li><a href="http://infolab.stanford.edu/db_pages/infoqual.html">Stanford PhD qualifying exam</a></li>
<li>MIT: <a href="http://db.csail.mit.edu/6.830/sched.html">Database Systems 6.830 year 2014</a> and <a href="http://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-830-database-systems-fall-2010/readings/">year 2010</a></li>
<li><a href="https://www.cs.wisc.edu/sites/default/files/pictures/Database%20systems%20qual_Summer%202014.pdf">Wisconsin Database Qualifying Exam Reading List (2014)</a></li>
<li><a href="http://15721.courses.cs.cmu.edu/spring2016/schedule.html">CMU 15-721 Database Systems Reading List (Spring 2016)</a></li>
</ul>
</article>
  </div>
