
# Understand-Again-Summarise


Polars was built from the ground up to be blazingly fast and can do common operations around 5–10 times faster than pandas.Polars is that it is written in Rust, a low-level language that is almost as fast as C and C++. In contrast, pandas is built on top of Python libraries, one of these being NumPy. While NumPy’s core is written in C, it is still hamstrung by inherent problems with the way Python handles certain types in memory, such as strings for categorical data, leading to poor performance when handling these types. Another factor that contributes to Polars’ impressive performance is Apache Arrow, a language-independent memory format. Arrow was actually co-created by Wes McKinney in response to many of the issues he saw with pandas as the size of data exploded. It is also the backend for pandas 2.0, a more performant version of pandas. One of the other cores of Polars’ performance is how it evaluates code. Pandas, by default, uses eager execution, carrying out operations in the order you’ve written them. In contrast, Polars has the ability to do both eager and lazy execution, where a query optimizer will evaluate all of the required operations and map out the most efficient way of executing the code.
https://wesmckinney.com/blog/apache-arrow-pandas-internals/
https://stackoverflow.com/questions/75680491/what-is-the-trade-off-between-lazy-and-strict-eager-evaluation

https://www.youtube.com/watch?v=lqz12s064RY - data lineage using openlineage
 
window function in pyspark

partition vs group by difference
pyspark - filter narrow transformation, groupby wide transformation
scalar and predicate subqueries.

https://blog.jetbrains.com/dataspell/2023/08/polars-vs-pandas-what-s-the-difference/

https://news.ycombinator.com/

https://sachidisanayaka98.medium.com/how-chrome-browser-use-process-threads-643dff8ad32c

https://www.linkedin.com/posts/hnaser_in-the-beginning-for-the-os-to-write-to-activity-7163388923916861441-t1vw?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_the-big-win-of-using-threads-instead-of-processes-activity-7161147178546069506-yehp?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_fragmentation-is-a-very-interesting-topic-activity-7156142414989037568-6C96?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_today-i-learned-how-the-linux-option-netipv4-activity-7150555792662740992-w8fL?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_i-just-learned-that-in-addition-to-the-mapping-activity-7148454941404110848-8m4D?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_i-am-fascinated-by-gos-compiler-escape-analysis-activity-7144747978224746496-z-YZ?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_glad-mongo-fixed-this-in-62-so-prior-to-activity-7135553971066175489-nwm7?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_why-does-it-take-time-for-dns-to-resolve-activity-7134793549526528001-xjL0?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_a-connection-pool-is-always-a-good-idea-especially-activity-7134109245909725184-qaUE?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_graphql-was-invented-by-facebook-mainly-because-activity-7127490321701056513-DSxX?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_the-recent-cloudflare-api-outage-on-november-activity-7126989541537677312-upGW?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_http3-is-taking-over-the-world-but-consider-activity-7116186211039285248-Bae7?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_i-got-asked-how-vpn-works-on-x-so-here-is-activity-7110641803984322560--ONA?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_fun-networking-fact-http-related-pglocks-activity-7108275178979160064-gAVu?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_its-fascinating-to-know-how-jit-just-in-activity-7101992901496229888-_777?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_postgres-has-weak-locks-those-are-table-activity-7078250396678303744-p6WU?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_normally-when-you-write-to-disk-the-writes-activity-7067253338395852800-r2JY?utm_source=share&utm_medium=member_desktop

https://bugs.mysql.com/bug.php?id=109595

https://www.youtube.com/watch?v=lCb5BkJOOVI&list=PLQnljOFTspQU0ICDe-cL1EwXC4GDSayKY&index=43

https://medium.com/@hnasr/the-journey-of-a-request-to-the-backend-c3de704de223

https://blog.jcole.us/2014/04/16/the-basics-of-the-innodb-undo-logging-and-history-system/

https://medium.com/@hnasr/how-slow-is-select-8d4308ca1f0c

https://medium.com/@hnasr/what-happens-when-databases-crash-74540fd97ea9

https://www.linkedin.com/pulse/how-troubleshoot-long-postgres-startup-nikolay-samokhvalov/

https://keefmck.blogspot.com/2023/04/why-ssds-lie-about-flush.html?m=1

https://tontinton.com/posts/scheduling-internals/

https://stackoverflow.com/questions/1518711/how-does-free-know-how-much-to-free

https://blog.allegro.tech/2024/03/kafka-performance-analysis.html

https://www.youtube.com/watch?v=d86ws7mQYIg

https://www.linkedin.com/pulse/builder-design-pattern-prateek-mishra


----------------------------------------------------------------------





















