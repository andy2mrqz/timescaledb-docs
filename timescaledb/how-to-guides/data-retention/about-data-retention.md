# About data retention
In time-series applications, data often becomes less useful as it gets older. If
you don't need your historical data, you can delete it once it reaches a certain
age. TimescaleDB lets you set up
[automatic data retention policies][retention-policy] to discard old data. You
can also fine-tune data retention by [manually dropping chunks][manual-drop].

Often, you want to keep summaries of your historical data, but you don't need
the raw data. You can downsample your older data by
[combining data retention with continuous aggregates][retention-with-caggs].

## Drop data by chunk
TimescaleDB data retention works on chunks, not on rows. Deleting data
row-by-row, for example with the PostgreSQL `DELETE` command, can be slow. But
dropping data by the chunk is faster, because it deletes an entire file from
disk. It doesn't need garbage collection and defragmentation.

Whether you use a policy or manually drop chunks, TimescaleDB drops data by the
chunk. It only drops chunks where _all_ the data is wihin the specified time
range.

For example, consider the setup where you have 3 chunks containing data:
1.  More than 36 hours old
1.  Between 12 and 36 hours old
1.  From the last 12 hours

You manually drop chunks older than 24 hours. Only the oldest chunk is deleted.
The middle chunk is retained, because it contains some data newer than 24 hours.
No individual rows are deleted from that chunk.

[manual-drop]: /how-to-guides/data-retention/manually-drop-chunks/
[retention-policy]: /how-to-guides/data-retention/create-a-retention-policy/
[retention-with-caggs]: /how-to-guides/data-retention/data-retention-with-continuous-aggregates/
