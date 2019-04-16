---
title: NoSQL Databases
description: A comparison of various NoSQL databases
---

## Comparison

<table class="table table-bordered table-hover table-condensed" id="data">
        <thead>
          <tr>
            <th class="name">Name</th>
            <th class="cap-tradeoff"><abbr title="Consistency, Availablity, Partition Tolerance">CAP</abbr> Tradeoff</th>
            <th class="transactions">Transactions</th>
            <th class="indexes">Indexes</th>
            <th class="data-model">Data Model</th>
            <th class="license">License</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td class="name"><a href="http://www.mongodb.org/">MongoDB</a></td>
            <td class="cap-tradeoff">Consistency</td>
            <td class="transactions">Conditional Writes</td>
            <td class="indexes">Local Secondary</td>
            <td class="data-model">Document</td>
            <td class="license"><a href="https://www.gnu.org/licenses/agpl-3.0.html">AGPL v3.0</a></td>
          </tr>
          <tr>
            <td class="name"><a href="https://cassandra.apache.org/">Cassandra</a></td>
            <td class="cap-tradeoff">Availability</td>
            <td class="transactions"><abbr title="Conditional Writes are CP not AP">Conditional Writes</abbr></td>
            <td class="indexes">Local Secondary</td>
            <td class="data-model">Wide Column</td>
            <td class="license"><a href="https://www.apache.org/licenses/LICENSE-2.0.html">Apache v2.0</a></td>
          </tr>
          <tr>
            <td class="name"><a href="http://basho.com/riak/">Riak</a></td>
            <td class="cap-tradeoff">Availability</td>
            <td class="transactions"><abbr title="Check and Set operations are CP not AP">Check and Set</abbr></td>
            <td class="indexes">Local Secondary</td>
            <td class="data-model">Key Value</td>
            <td class="license"><a href="https://www.apache.org/licenses/LICENSE-2.0.html">Apache v2.0</a></td>
          </tr>
          <tr>
            <td class="name"><a href="https://hbase.apache.org/">HBase</a></td>
            <td class="cap-tradeoff">Consistency</td>
            <td class="transactions">Conditional Writes</td>
            <td class="indexes">Primary Only</td>
            <td class="data-model">Wide Column</td>
            <td class="license"><a href="https://www.apache.org/licenses/LICENSE-2.0.html">Apache v2.0</a></td>
          </tr>
          <tr>
            <td class="name"><a href="https://accumulo.apache.org/">Accumulo</a></td>
            <td class="cap-tradeoff">Consistency</td>
            <td class="transactions">Conditional Writes</td>
            <td class="indexes">Primary Only</td>
            <td class="data-model">Wide Column</td>
            <td class="license"><a href="https://www.apache.org/licenses/LICENSE-2.0.html">Apache v2.0</a></td>
          </tr>
          <tr>
            <td class="name"><a href="http://www.rethinkdb.com/">RethinkDB</a></td>
            <td class="cap-tradeoff">Consistency</td>
            <td class="transactions">Conditional Writes</td>
            <td class="indexes">Local Secondary</td>
            <td class="data-model">Document</td>
            <td class="license"><a href="https://www.gnu.org/licenses/agpl-3.0.html">AGPL v3.0</a></td>
          </tr>
          <tr>
            <td class="name"><a href="http://www.aerospike.com/">Aerospike</a></td>
            <td class="cap-tradeoff">Consistency</td>
            <td class="transactions">Check and Set</td>
            <td class="indexes">Local Secondary</td>
            <td class="data-model">Key Value</td>
            <td class="license"><a href="https://www.gnu.org/licenses/agpl-3.0.html">AGPL v3.0</a></td>
          </tr>
          <tr>
            <td class="name"><a href="http://redis.io/">Redis</a></td>
            <td class="cap-tradeoff"><abbr title="Using Redis Cluster">Consistency</abbr></td>
            <td class="transactions">Check and Set</td>
            <td class="indexes">Primary Only</abbr></td>
            <td class="data-model">Data Structures</td>
            <td class="license"><a href="http://opensource.org/licenses/BSD-3-Clause">BSD 3-Clause</a></td>
          </tr>
         <tr>
            <td class="name"><a href="http://couchdb.apache.org/">CouchDB</a></td>
            <td class="cap-tradeoff">Availability</td>
            <td class="transactions">Check and Set</td>
            <td class="indexes"><abbr title="Indexes are created using views">Local Secondary</abbr></td>
            <td class="data-model">Document</td>
            <td class="license"><a href="https://www.apache.org/licenses/LICENSE-2.0.html">Apache v2.0</a></td>
          </tr>
          <tr>
            <td class="name"><a href="https://pouchdb.com">PouchDB</a></td>
            <td class="cap-tradeoff">Availability</td>
            <td class="transactions">Check and Set</td>
            <td class="indexes"><abbr title="Indexes are created using views">Local Secondary</abbr></td>
            <td class="data-model">Document</td>
            <td class="license"><a href="https://www.apache.org/licenses/LICENSE-2.0.html">Apache v2.0</a></td>
          </tr>
          <tr>
            <td class="name"><a href="http://www.couchbase.com/">Couchbase</a></td>
            <td class="cap-tradeoff">Consistency</td>
            <td class="transactions">Check and Set</td>
            <td class="indexes"><abbr title="Indexes are created using views">Local Secondary</abbr></td>
            <td class="data-model">Document</td>
            <td class="license"><a href="https://www.apache.org/licenses/LICENSE-2.0.html">Apache v2.0</a></td>
          </tr>

        </tbody>
</table>


## References

http://nosqldbs.io/
