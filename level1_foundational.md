# GENERATORS(yield)

### What??
 A generator is a special Python function that returns data chunk-by-chunk using the yield keyword instead of loading everything into a giant list at once.
 
### Why??
It completely stops Out-of-Memory (OOM) crashes. If an upstream system passes you a massive 20GB dataset, standard Python loops will try to load all 20GB into your computer's RAM, 
causing it to crash. A generator streams it line-by-line, keeping memory usage close to zero.

### Where??
- Reading Massive Files: Reading a 50 Gigabyte CSV log file from a server. A generator reads Line 1, gives it to you to process, deletes it from memory, and then reads Line 2. Your computer never crashes.
- Calling APIs with Pagination: If you pull data from the YouTube API, it won't give you 1 million records at once. It gives you Page 1 (100 rows). A generator handles Page 1, yields it to your system, and only fetches Page 2 when your system asks for more.
- Database Streaming: Pulling 100 million customer records from a production PostgreSQL database without slowing down the database or locking up your local machine.

### CODE??

```python
def stream_large_dataset(fake_database):
    """Streams data chunk-by-chunk using yield."""
    for row in fake_database:
        # yield pauses the function and hands over just one item
        yield row 

# --- How you actually use it ---
# Imagine this list has millions of items
massive_list = ["row_1", "row_2", "row_3", "row_4"]

# This creates the generator object (does NOT load data yet)
data_stream = stream_large_dataset(massive_list)

# We pull one item at a time into memory as we loop
for record in data_stream:
    print(f"Processing: {record}")

```

