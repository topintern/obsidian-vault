---
kind: "company-prep"
title: "Interview STAR Stories"
collection: "Acuity Kp"
topic: "Interview Prep"
imported: "2026-10-13"
source_files: ["Interview Prep company prep docs/Acuity Kp/Interview_STAR_Stories.html","Interview Prep company prep docs/Acuity Kp/Interview_STAR_Stories.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Interview STAR Stories

[[The Climb/Career Library/Career Library]]

> [!info] Source context
> Historical preparation or source notes. First-person stories and numeric outcomes remain source claims until confirmed; this import does not verify them.

# Acuity KP Interview Prep — Full STAR Technical Story Bank
> **Role**: Data Engineer | **Company**: Acuity KP  
> **Your Resume**: Epik Solutions → Samay Systems LLC → Zemoso Technologies  
> Every single bullet → deep STAR story + concept teardown + follow-up armor.  
> Read top to bottom. Each story builds vocabulary for the next.

---

## HOW TO USE THIS DOC
- **STAR Story** — lock in the narrative arc, memorize the flow
- **Concept Breakdown** — every technical term defined (so follow-ups can't touch you)
- **Natural Phrasing** — what to say out loud, in a human voice, in the room
- **Follow-ups** — pre-loaded answers for the questions that always come next


---

# PYTHON -- Deep Dive Stories & Concept Reference
> Acuity KP specifically wants strong Python. Five STAR stories drawn from your real work,
> each covering the Python design decisions, library choices, and architectural reasoning
> behind the code -- not the syntax, but the thinking.

---

## Python Story 1 -- OOP Framework Design for Reusable ELT Pipelines

> At Samay Systems you built a Python framework used across 15+ client pipelines.
> This directly answers the JD requirement: "develop reusable data engineering frameworks."

---

### STAR Story

**Situation**

At Samay I was building compliance ELT pipelines for 15 enterprise clients simultaneously.
Every client had a different source system -- some were REST APIs, some were SFTP flat file
drops, some were direct database connections. Without structure, each pipeline was a
standalone script with copy-pasted retry logic, logging, error handling, and validation.
When I found a bug in the retry mechanism, I had to fix it in 15 different files. That
maintenance overhead was unsustainable, and the risk of divergence was real -- one pipeline
getting a fix that five others never received.

**Task**

Design a Python framework where common infrastructure (logging, retries, connection
management, schema validation) lived once and was inherited automatically by every pipeline,
while each client-specific pipeline only implemented the unique extraction and transformation
logic for its particular source system.

**Action -- The design decisions**

The foundation was Python's Abstract Base Class system, using `ABC` from the built-in `abc`
module. I created a `BaseExtractor` class that inherited from `ABC` and marked the `extract`
method with `@abstractmethod`. The consequence of this decorator is that Python will raise a
`TypeError` at instantiation time if any subclass fails to implement `extract` -- it cannot
even be instantiated. This moves the "did you forget to implement this?" check from runtime
(buried inside a 4-hour pipeline run) to construction time (caught immediately when the
object is created).

The design pattern at work is the Template Method pattern. The `run` method on the base class
defines the algorithm skeleton -- log the start, call `extract`, handle errors, log
completion. Subclasses override only `extract`, never `run`. This means every pipeline
automatically inherits consistent logging and error handling without any subclass needing to
think about it. A new engineer building a 16th client pipeline cannot accidentally ship
without logging because the base class provides it unconditionally.

For the `extract` method I designed it as a Python generator -- it uses `yield` to produce
DataFrames in chunks rather than returning one giant collection. The critical insight here is
memory: if a source has 10 million rows, loading everything into a list and returning it means
10 million rows in RAM simultaneously. With a generator, only one chunk (say 10,000 rows) is
in memory at any moment. The caller consumes each chunk, processes it, discards it, and asks
for the next one. The base class's `run` method uses `yield from self.extract()` which
delegates to the subclass generator transparently -- the whole pipeline becomes a streaming
chain without any single component holding the full dataset.

Configuration across 15 clients meant 15 different sets of parameters -- API URLs, batch
sizes, schema names, retry counts. I used Python's `@dataclass` decorator for configuration
objects. The decorator auto-generates `__init__`, `__repr__`, and `__eq__` from the class
annotations, eliminating boilerplate. The important technical detail is `field(default_factory=list)`
for any list-type attribute. The naive approach -- writing `tags: list = []` as a default --
creates a single list object once when the class is defined and shares it across all instances.
This is the mutable default argument bug: mutate the list on one instance and every other
instance sees the mutation. `field(default_factory=list)` tells the dataclass machinery to
call `list()` fresh for each new instance. I also used `__post_init__` for validation --
the method runs automatically after `__init__` completes, so invalid configurations raise
`ValueError` at object construction rather than failing deep inside a pipeline run.

Resource management -- database connections, file handles -- used Python context managers
via the `@contextmanager` decorator from `contextlib`. A context manager separates the
resource acquisition from resource release using a `finally` block that always executes
regardless of whether an exception was raised inside the `with` block. Writing it as a
decorated generator function (rather than a class with `__enter__` and `__exit__`) is
simpler and reads more naturally. The downstream effect: no leaked Snowflake connections
even when a pipeline crashes halfway through.

For type safety across the framework I used Python type hints throughout -- `Iterator[pd.DataFrame]`
as the return type of `extract`, `str | None` for optional strings, `PipelineConfig` as the
parameter type for functions that accept configuration. These are not enforced at runtime by
default Python, but I ran `mypy` in CI as part of every pull request. Mypy is a static type
checker that reads the annotations and catches type mismatches before code ever runs --
a `None` dereference that would crash at 2 AM in a production pipeline gets caught as a CI
failure when the PR is raised.

I also used `Protocol` from `typing` for interfaces at the boundary between the framework
and callers. A `Protocol` is Python's structural typing mechanism -- any class that has the
right method signatures satisfies the Protocol, regardless of inheritance. This is different
from `ABC` which requires explicit inheritance. The distinction matters at architectural
boundaries: within the framework, `ABC` enforces implementation contracts at construction
time. At the framework's public API, `Protocol` allows callers to provide their own
implementations without inheriting from your base classes -- looser coupling, easier to test.

**Result**

One framework, 15 pipelines. A bug fix to retry logic required a single PR that propagated
to all clients automatically. Adding a new client integration meant creating one subclass,
implementing `extract`, and zero other code. The framework layer -- logging, retries,
connection management, schema validation -- never appeared in any client-specific file.
Onboarding time for a new pipeline dropped from two days to under half a day.

---

### Technical Concept Breakdown

| Concept | What It Is | Why It Matters in Your Context |
|---------|-----------|-------------------------------|
| **Abstract Base Class (ABC)** | A class with `@abstractmethod` methods that subclasses must implement. Python raises `TypeError` at instantiation if any abstract method is missing. | Moves "forgot to implement" bugs from runtime to construction time. At scale, this is the difference between a midnight prod failure and a caught bug before deployment. |
| **`@abstractmethod`** | Decorator that marks a method as required for all non-abstract subclasses. | Enforces the interface contract at the language level, not through documentation or convention. |
| **Template Method Pattern** | The base class defines an algorithm skeleton with fixed and variable steps. Subclasses override only the variable steps. | Shared infrastructure (logging, retries) lives once. Subclasses focus exclusively on their unique logic. No risk of infrastructure code being forgotten or diverging. |
| **Generator / `yield`** | A function that uses `yield` to produce values lazily, one at a time. Does not execute past the `yield` until the caller requests the next value. | Memory-efficient streaming. 10M row extracts stay flat in memory because only one chunk at a time is ever materialized. |
| **`yield from`** | Delegation syntax for generators. `yield from gen()` is equivalent to iterating through `gen()` and yielding each value, but without the overhead of an explicit loop. | Lets `run()` delegate to `extract()` transparently while keeping the streaming chain intact. |
| **`@dataclass`** | Class decorator that auto-generates `__init__`, `__repr__`, and `__eq__` from annotated fields. | Eliminates config class boilerplate. Derived fields and validation go in `__post_init__`. |
| **`field(default_factory=...)`** | Calls the factory function to create a fresh object for each dataclass instance. | Prevents the mutable default argument bug: `default=[]` shares one list object across ALL instances. `default_factory=list` creates a new list per instance. |
| **`__post_init__`** | Called by the dataclass machinery after `__init__` completes. Used for validation and derived field computation. | Validate at construction time -- wrong config raises immediately, not mid-pipeline. |
| **`@contextmanager`** | Decorator that turns a generator with a single `yield` into a context manager. The `finally` block after the `yield` always runs on exit. | Simpler than writing `__enter__`/`__exit__`. Guarantees resource cleanup even on exceptions. |
| **Type hints + mypy** | PEP-484 annotations (`str`, `int`, `Iterator[T]`) for function signatures. Mypy is the static type checker that enforces them at CI time. | Catches type errors before runtime. Makes function signatures self-documenting. Enables IDE autocomplete on complex types. |
| **`Protocol`** | Structural typing interface. A class satisfies a Protocol if it has the required method signatures -- no inheritance needed. | Looser coupling at API boundaries. Callers can pass in anything with the right methods; they don't need to inherit from your classes. Easier to mock in tests. |

---

### How to Say It in the Interview

"At Samay I had to solve a real maintenance problem -- 15 client pipelines that were
essentially the same script copy-pasted with different configs. I built a Python OOP
framework around the Abstract Base Class pattern. The base class used the Template Method
design pattern: `run()` defined the skeleton -- logging, retry, error handling -- and
subclasses only implemented `extract()`, which was a generator that yielded DataFrame chunks
for memory efficiency. The key enforcement mechanism was `@abstractmethod` -- Python itself
raised a `TypeError` if you tried to instantiate a subclass that hadn't implemented `extract`,
so you could never accidentally deploy an incomplete pipeline. Configuration was dataclasses
with `field(default_factory=list)` for mutable defaults -- avoiding the classic Python bug
where all instances share one list object. I also ran mypy in CI so type errors were caught
at PR time rather than at 2 AM in production."

---

### Likely Follow-up Questions

**"What is the mutable default argument bug?"**
The problem occurs when you write a function or class with a mutable object as a default
parameter value -- for example `def __init__(self, tags=[])`. Python creates that default
list once when the function definition is executed, and every call that uses the default
shares the same list object. If one caller appends to the list, the next caller sees that
mutation. The fix is to use `None` as the default and create the list inside the function
body, or in dataclasses, use `field(default_factory=list)` to create a fresh list for each
instance.

**"Difference between ABC and Protocol?"**
ABC is nominal typing -- a class must explicitly inherit from the ABC to satisfy it.
If a subclass fails to implement an abstract method, Python raises `TypeError` at
instantiation. Protocol is structural typing -- any class that has the right method
signatures satisfies the Protocol, regardless of inheritance. ABC is appropriate within a
framework where you control all implementations and want hard enforcement. Protocol is
appropriate at public API boundaries where you want to accept anything duck-typed-compatible
without forcing callers to inherit from your classes.

**"Why use a generator instead of returning a list?"**
A generator uses `yield` to produce values lazily -- it only runs until the next `yield`
when the caller requests the next value. Returning a list materializes everything in memory
at once. For a pipeline extracting 10 million compliance records, returning a list means
holding all 10 million rows in RAM simultaneously. A generator that yields 10,000-row
chunks means the maximum RAM usage at any point is one chunk. The downstream pipeline can
process, write, and discard each chunk before requesting the next. It also enables short
circuits -- if a downstream error occurs after the first three chunks, you never extracted
the remaining seven.

---

## Python Story 2 -- PySpark DataFrame API: Schemas, Pandas UDFs, Window Functions

> Every Databricks and PySpark bullet on your resume is Python. This story covers the
> Python-specific decisions that separate correct PySpark from fast, production-grade PySpark.

---

### STAR Story

**Situation**

At Epik, security event data arriving from Azure Event Hubs was raw JSON bytes with no
enforced schema. The Bronze-to-Silver transformation required parsing these bytes into a
strongly typed structure, running custom enrichment logic that plain Spark SQL could not
express (IP address classification, threat score normalization based on internal lookup
tables), and computing stateful rolling statistics -- event rate per source IP per tenant
over a sliding 5-minute window. These requirements pushed against the edges of what Spark
SQL handles naturally.

**Task**

Write PySpark transformations in Python that were: schema-enforced at ingestion, enriched
with custom Python logic at production speed, and augmented with rolling-window statistics.
The wrong Python choices here (inferred schemas, row-by-row UDFs) would have worked
functionally but been 10-50x slower at the event volumes we were processing.

**Action -- The design decisions**

For schema definition I always write explicit `StructType` objects with `StructField` entries
rather than relying on `inferSchema=True`. The `inferSchema` option reads the entire input
file or JSON body to guess types -- this is expensive, and for streaming from Event Hubs,
impossible (a stream has no end to sample from). More importantly, `inferSchema` makes
assumptions that are often wrong: a column that happens to contain only `"1234"` in the
sample data gets inferred as `LongType` when the business requirement is `StringType` because
it is a code, not a number. Explicit schemas also allow `nullable=False` on columns that
must never be null -- setting this means Spark will reject writes with null values in that
column if schema enforcement is enabled on the Delta table, turning data quality from a
convention into a constraint. For the semi-structured metadata field (arbitrary key-value
pairs per event type), I used `MapType(StringType(), StringType())` which represents a
dictionary column in Spark's type system -- queryable by key using bracket notation.

For custom enrichment logic, the decision between Python UDFs, Pandas UDFs, and Spark SQL
built-in functions is one of the most important performance choices in PySpark Python work.
The built-in Spark SQL functions (things like `from_json`, `regexp_extract`, `unix_timestamp`,
`to_date`) are the fastest option because they execute entirely inside the JVM without
crossing the language boundary at all. When business logic is too complex for built-ins, the
next choice is a Pandas UDF, also called a vectorized UDF. A Pandas UDF is decorated with
`@pandas_udf` and its function signature receives and returns a `pd.Series` -- an entire
column at once rather than one row at a time. The bridge between JVM and Python in a
Pandas UDF uses Apache Arrow, an in-memory columnar data format designed for zero-copy data
transfer. Zero-copy means the data is not serialized and deserialized -- the memory layout
that Spark uses internally is the same format Arrow uses, so transferring the entire column
to Python has near-zero overhead compared to serializing each row individually.

A regular Python UDF does the opposite: it serializes each row from the JVM to the Python
process using `pickle`, executes Python on that single row, serializes the result back via
pickle, then moves to the next row. This row-by-row ping-pong across the JVM-Python boundary
is the source of the 10-50x slowdown. The only time to use a regular Python UDF is when
the logic truly cannot be vectorized -- when it involves stateful Python objects that cannot
operate on a Pandas Series. In practice, IP address classification, URL parsing, custom
normalization logic, and most string processing can all be vectorized easily with Pandas
Series methods.

Window functions addressed the stateful rolling-statistics requirement. A window function
in Spark computes a value for each row using a defined "window" of related rows, without
collapsing the DataFrame the way `groupBy` and `agg` would. The window definition has three
components: `partitionBy` which resets the window for each group (equivalent to GROUP BY in
SQL), `orderBy` which defines row ordering within the partition, and a frame specification
that defines which rows are included in the window relative to the current row. For the
rolling 5-minute event count per tenant-IP pair, I used `rangeBetween(-300, 0)` on a Unix
timestamp column. The `rangeBetween` frame uses the ORDER column's numeric value -- so
`-300, 0` means "include all rows whose Unix timestamp is within 300 seconds before and
equal to the current row's timestamp." This is a time-range window. The alternative,
`rowsBetween(-N, 0)`, counts N preceding rows by position regardless of their timestamp
values -- this would give a rolling event count by count, not by time, which would be wrong
when event rates are variable.

The `lag` function computes the value from N rows behind the current row within the same
partition and ordering -- this is how I computed "seconds since last event from the same
source IP," which was the primary signal for detecting automated scanning patterns. A human
browsing a network will have irregular inter-event gaps. An automated scanner produces
events at a consistent machine-speed rate. `lag(unix_timestamp_col, 1)` gives the
previous row's timestamp, and subtracting gives the delta.

The most common PySpark Python mistakes I explicitly avoided: calling `collect()` which
pulls the entire DataFrame to the driver node (fine for summary statistics on small outputs,
catastrophic on raw event data); calling `count()` in a loop which triggers a full Spark job
per iteration; and creating Spark operations inside a UDF (UDFs must be pure Python functions
with no access to the Spark context).

**Result**

Schema-enforced, null-rejecting Bronze-to-Silver transformation in Python. IP classification
via Pandas UDFs ran at the same order of magnitude as pure SQL for our event volumes.
The rolling 5-minute event count enabled a rate-based alerting rule that caught three genuine
security incidents in the first month of operation -- incidents that the threshold-only rules
missed because they considered aggregate daily totals rather than instantaneous event rates.

---

### Technical Concept Breakdown

| Concept | What It Is | Why It Matters in Your Context |
|---------|-----------|-------------------------------|
| **`StructType` / `StructField`** | Explicit Spark schema definition. Each field has a name, type, and nullable flag. | Never use `inferSchema` in production. Explicit schemas catch type mismatches at write time, enable null enforcement, and are required for streaming. |
| **`nullable=False`** | Schema constraint that makes Spark reject writes with null values in that column when enforcement is on. | Data quality enforced at the storage layer. Bad data is rejected at the gate rather than silently propagating. |
| **`MapType`** | Spark column type for a dictionary (key-value map) with variable keys. | Models semi-structured data where not all rows have the same fields. Query via bracket notation on the column. |
| **Spark SQL built-in functions** | Functions like `from_json`, `unix_timestamp`, `regexp_extract` that execute in the JVM with no Python overhead. | Fastest option. Use whenever business logic can be expressed with them. |
| **Regular Python UDF** | A Python function registered with Spark via `udf()`. Serializes data row-by-row via pickle across the JVM-Python boundary. | Last resort -- row-by-row pickle serialization is 10-50x slower than vectorized alternatives. Use only when logic truly cannot be vectorized. |
| **Pandas UDF (vectorized UDF)** | A Python function decorated with `@pandas_udf` that receives and returns a `pd.Series`. Data transfers as a whole column via Apache Arrow. | The right way to add Python logic at scale. Arrow's zero-copy transfer eliminates per-row serialization overhead. 10-50x faster than regular UDFs. |
| **Apache Arrow** | In-memory columnar data format used for zero-copy JVM-to-Python data transfer in Pandas UDFs. | The technical reason Pandas UDFs are fast. Spark's internal memory format and Arrow's format are compatible -- no serialization needed. |
| **Window Function** | Computes a value for each row across a window of related rows without reducing the DataFrame. | Rolling aggregations, lag/lead values, rankings -- stateful calculations across related rows that are impossible with plain groupBy. |
| **`rangeBetween(start, end)`** | Window frame defined by ORDER column value range relative to the current row. `-300, 0` on a Unix timestamp = last 300 seconds. | Time-based sliding windows. Distinct from `rowsBetween` which counts by row position. Critical distinction when event rates are variable. |
| **`rowsBetween(start, end)`** | Window frame defined by row position -- N preceding rows regardless of ORDER column values. | Position-based rolling windows. Use for "last N events" semantics rather than "last N seconds." |
| **`lag(column, N)`** | Window function that returns the value from N rows behind the current row within the partition ordering. | Compute inter-event deltas: current timestamp minus previous timestamp gives time since last event. |

---

### How to Say It in the Interview

"For PySpark I always write explicit StructType schemas rather than inferring them. Schema
inference requires reading the full dataset to guess types, is unreliable for schemas like
compliance codes where numeric-looking strings should stay as strings, and is impossible in
streaming where there's no end to sample from. For custom enrichment logic I use Pandas
UDFs rather than regular Python UDFs -- the difference is how data crosses the JVM-Python
boundary. A regular UDF uses pickle per row, one row at a time. A Pandas UDF transfers the
entire column via Apache Arrow, which is a zero-copy operation because Spark and Arrow use
the same in-memory columnar format. For the rolling 5-minute event count per source IP I
used a window function with `rangeBetween(-300, 0)` on a Unix timestamp column -- that is a
time-range window, meaning it includes all rows whose timestamp falls within 300 seconds of
the current row's timestamp, not a fixed row count. The distinction matters when event rates
vary -- a machine scanner fires 100 events in 5 minutes, a human might fire 3."

---

### Likely Follow-up Questions

**"When do you use a Spark SQL built-in vs Pandas UDF vs Python UDF?"**
Priority order: first, use a Spark SQL built-in function if one exists for the logic -- these
run entirely in the JVM with zero Python overhead and are always fastest. Second, if you need
Python logic, use a Pandas UDF with `@pandas_udf` so data transfers as a whole column via
Arrow. Third and last resort only, use a regular Python UDF when the logic truly cannot be
vectorized into a Pandas Series operation.

**"What is the difference between `rangeBetween` and `rowsBetween`?"**
`rowsBetween(-3, 0)` means the 3 rows immediately preceding the current row by position in
the partition's ordering -- it counts by row number. `rangeBetween(-300, 0)` means rows
whose ORDER column value is within 300 of the current row's value -- when the ORDER column
is a Unix timestamp, this means the last 300 seconds. For time-based windows where event
rates are variable, `rangeBetween` on a timestamp is the correct approach. `rowsBetween`
would give you a rolling 3-event window regardless of whether those 3 events happened over
1 second or 1 hour.

**"What is the GIL and does it affect PySpark?"**
The Global Interpreter Lock prevents multiple Python threads from executing Python bytecode
simultaneously in one process. In PySpark, the JVM manages true parallelism across worker
nodes -- Python UDFs run in separate Python processes on each worker, not in threads, so the
GIL is not a bottleneck for distributed work. The GIL matters when you try to use Python
multi-threading for CPU-bound parallelism within a single process -- for that, you need
multiprocessing, not threading.

---

## Python Story 3 -- REST API Client: Pagination, Rate Limiting, Retry Backoff

> At Samay and Zemoso you built API integrations repeatedly. This is the production Python
> patterns story for robust API clients.

---

### STAR Story

**Situation**

At Samay, each client's compliance data was pulled from 4 to 6 external REST APIs --
regulatory feeds, HR systems, sanctions screening APIs, trade surveillance endpoints. Some
had strict rate limits of 100 requests per minute. Some had unreliable uptime, returning 500
errors unpredictably under load. Regulatory APIs returned millions of compliance records
across thousands of pages. The naive approach -- a bare `requests.get()` loop -- failed
constantly: rate limit 429 responses, timeout exceptions, and APIs that returned 500 errors
midway through a 2-hour extract job, killing the entire run with no resume capability.

**Task**

Write a reusable Python API client class that handled pagination transparently, throttled
request rate to stay within API limits, and retried transient failures with exponential
backoff -- all reusable across every client integration without modification.

**Action -- The design decisions**

For retry logic I used the `tenacity` library rather than hand-rolling a retry loop. Tenacity
lets you compose retry strategies as decorators on the method that makes the actual HTTP
call. The strategy I used was `wait_exponential` with `multiplier=1, min=2, max=60` -- this
means: wait 2 seconds before the first retry, double that to 4 seconds before the second,
8 before the third, 16 before the fourth, and cap at 60 seconds for any subsequent retries.
The exponential growth is important because it gives a struggling API server time to recover
rather than hammering it with retry requests every few seconds.

The `retry_if_exception_type` parameter is equally critical. I specified it to only retry on
`requests.Timeout` and `requests.ConnectionError` -- transient network conditions that are
worth retrying. If a `ValueError` occurs (programming error -- wrong field name), or a `KeyError`
(unexpected response structure), those are bugs in our code, not transient server conditions.
Retrying them just repeats the same failure five times. The tenacity `before_sleep_log`
parameter logs a warning before each retry attempt so engineers can see in the log stream
how many retries happened before success, which is useful for identifying intermittently
flaky APIs. The `reraise=True` setting means if all five attempts fail, the original
exception propagates to the caller rather than being wrapped in a tenacity exception type.

Rate limiting used a token bucket approach with `time.monotonic()` for elapsed time
measurement. The token bucket concept is: tokens accumulate at a constant rate (one token
per `1 / rate_limit_rps` seconds), and each request consumes one token. Before every HTTP
request, the client checks how much time has elapsed since the last request and sleeps for
the deficit if needed. I used `time.monotonic()` specifically rather than `time.time()`
because `time.time()` can go backwards when the system clock is adjusted by NTP
synchronization. `time.monotonic()` is a counter guaranteed never to decrease -- essential
for elapsed time measurement in timing-sensitive code.

For the HTTP session itself I used `requests.Session` rather than the top-level
`requests.get()` convenience function. A `Session` object maintains TCP connections via
HTTP keep-alive -- when you make a second request to the same host, it reuses the existing
TCP connection from a pool rather than performing a new TCP handshake. For an extract job
making hundreds of sequential API calls to the same host, this connection pooling provides
meaningful throughput improvement. The Session also persists headers across calls, so the
Authorization header is set once at initialization and sent on every request automatically.

Pagination was implemented as a Python generator method that yields one page of records at
a time. The caller never interacts with page numbers or cursors -- they iterate over the
generator and receive one list of records per iteration, stopping when the generator is
exhausted. Internally the method handles both offset-based pagination (where you pass
`?page=N`) and cursor-based pagination (where the API returns a `next_page_token` or
`next_cursor` value to include in the next request). Cursor-based pagination is preferable
when available because it is stable under concurrent inserts -- with offset pagination, if
records are inserted into the source database while you are paginating, some records shift
to a different page number and you get duplicates or gaps. A cursor points to a position in
an ordered sequence that remains stable regardless of inserts.

The generator pattern for pagination is elegant for a specific reason: memory usage stays
flat regardless of total record count. A client consuming the generator only holds one page
in memory at a time. If a downstream error occurs after fetching 200 pages, the generator
stops there -- it never fetched the remaining 800 pages it would have needed to had you
built a "fetch all then return" function.

**Result**

Zero manual restarts of API extract jobs due to transient network failures after deployment.
Rate-limited APIs were throttled transparently with no special handling by callers. Adding a
new API integration: configure the client with the base URL, API key, and rate limit, then
call `paginate()` in a for loop. The entire integration was one small subclass with
source-specific field mapping.

---

### Technical Concept Breakdown

| Concept | What It Is | Why It Matters in Your Context |
|---------|-----------|-------------------------------|
| **Exponential backoff** | After each failure, wait an exponentially increasing interval before retrying: 2s, 4s, 8s, 16s... capped at a maximum. | Gives a struggling API server time to recover. Avoids hammering it with rapid retries that make the overload worse. |
| **Jitter** | Adding randomness to backoff delays. | If 1000 clients all back off for exactly 2 seconds after a server overload, they all retry simultaneously -- the thundering herd problem. Jitter spreads retries across time. |
| **`tenacity`** | Python retry library with composable decorator-based retry strategies. | More expressive than hand-rolled loops. Handles logging, max attempts, wait strategies, exception type filtering cleanly. |
| **`retry_if_exception_type`** | Tenacity parameter specifying which exception types should trigger a retry. | Critical: only retry transient errors (Timeout, ConnectionError). Never retry programming errors (ValueError, KeyError) -- that just repeats the failure. |
| **`requests.Session`** | Maintains TCP connections, cookies, and headers across multiple requests to the same host. | HTTP keep-alive / connection pooling. Sequential API calls in a loop are significantly faster when connections are reused. |
| **Token bucket** | Rate limiting algorithm: tokens accumulate at a constant rate; each request consumes one token. Sleep if the bucket is empty. | Enforces average request rate while allowing short bursts up to the bucket capacity. Simple and effective for REST API throttling. |
| **`time.monotonic()`** | A monotonically increasing counter that never goes backwards. | Use for elapsed time measurement. `time.time()` can go backwards on NTP clock adjustments, which would break throttling logic. |
| **Cursor-based pagination** | API returns a cursor token pointing to the next page's position in an ordered sequence. | Stable under concurrent inserts. Offset pagination (`?page=3`) skips or duplicates records if rows are inserted between page fetches. |
| **Generator for pagination** | `yield`-based method that produces one page of records per iteration, lazily fetching pages on demand. | Memory stays flat regardless of total pages. Short circuits naturally if downstream processing stops early. |
| **`raise_for_status()`** | `requests` method that raises `HTTPError` for 4xx and 5xx status codes. | Forces explicit error handling. Without it, a 500 response silently returns a Response object and you process an error body as if it were valid data. |

---

### How to Say It in the Interview

"My API client at Samay used `tenacity` for retry -- exponential backoff starting at 2
seconds, capped at 60, and critically, only retrying on transient network exceptions:
`Timeout` and `ConnectionError`. I explicitly excluded retrying on `ValueError` or `KeyError`
because those are programming bugs, not transient server conditions -- retrying them just
repeats the failure five times. Rate limiting was a simple token bucket using
`time.monotonic()` -- I specifically used monotonic rather than `time.time()` because
monotonic cannot go backwards on NTP clock adjustments. Pagination is a generator method
that yields one page at a time -- the caller iterates over it in a for loop without ever
thinking about page tokens or cursors. I preferred cursor-based pagination over offset-based
wherever the API offered it because cursors are stable under concurrent inserts, whereas
offset pagination can give you duplicates or gaps if records are being inserted into the
source while you're paginating."

---

### Likely Follow-up Questions

**"What is the thundering herd problem?"**
When many clients all fail at the same time (because a server went down), they all back off
for the same fixed interval, then all retry simultaneously, which recreates the exact load
spike that caused the failure. Adding jitter -- a small random offset to each client's
backoff interval -- spreads retries across a time window instead of concentrating them at
a single moment. The server recovers gradually rather than being hit with another spike.

**"Why is cursor pagination better than offset pagination?"**
With offset pagination you say "give me records 200-300." If another process inserts 5 records
before record 200 while you're paginating, your next request for records 200-300 shifts and
you get duplicates or miss records. A cursor encodes a position in an ordered sequence -- the
API says "the next page starts after this specific record." Inserts before that position don't
affect the cursor's validity.

---

## Python Story 4 -- Testing Data Pipelines: pytest, Fixtures, Mocking

> The JD asks for automated testing frameworks. This is where you show you write testable,
> professionally structured Python -- not just scripts.

---

### STAR Story

**Situation**

At Samay, pipeline code had no automated tests. Bugs were discovered when analysts reported
wrong numbers in compliance dashboards, sometimes days after a bad change merged. In
financial compliance the cost is severe -- an incorrect aggregation in a trade surveillance
pipeline could mean incorrectly filed regulatory reports and potential fines. I needed to
build a testing culture and framework that made catching bugs the CI system's job before
any code reached production.

**Task**

Build a pytest-based testing framework that could meaningfully test: pure Python
transformation logic, PySpark DataFrames, API client behavior against mocked HTTP responses,
and database write correctness.

**Action -- The design decisions**

The testing framework was built on `pytest` rather than the standard library's `unittest`
because pytest's fixture system and parametrize decorator are significantly more ergonomic.
The central organization mechanism is `conftest.py` -- a special file that pytest
auto-discovers and uses to define shared fixtures available to all tests in the directory
tree below it.

The most expensive resource in PySpark tests is the SparkSession itself -- starting a
SparkSession locally takes 3 to 5 seconds. Using `@pytest.fixture(scope="session")` means
the fixture is created once for the entire test run and shared across all tests. If I had
used the default `scope="function"`, pytest would start and stop a new SparkSession for
every individual test -- a 100-test suite would spend 5 to 8 minutes just on SparkSession
startup. The session-scoped SparkSession is configured with `local[2]` as the master, which
runs Spark in-process using 2 local CPU threads -- no cluster needed, tests run in seconds.
The shuffle partitions are set to 2 rather than the default 200, which reduces unnecessary
overhead for the tiny test DataFrames.

For individual test DataFrames I used function scope (the default), meaning each test gets
a fresh DataFrame. This is test isolation -- tests that modify shared state can cause
order-dependent failures, where a test passes when run alone but fails when run after another
test that left shared state dirty. With function-scoped fixtures, there is no shared mutable
state between tests.

For testing API clients against HTTP responses, I used `unittest.mock.patch.object` to
replace the internal `_get` method with a mock that returns controlled responses. The
`side_effect` parameter accepts a list of values that the mock returns in sequence on
successive calls -- so I could simulate "first call returns page 1, second call returns page 2,
third call returns an empty page" without making any real HTTP requests. Tests are
deterministic (same inputs always produce same outputs), fast (no network round trips), and
cover exact edge cases including the empty-page termination condition. The `patch.object`
call is a context manager -- the mock is only active within the `with` block and the real
method is automatically restored when the block exits.

`pyspark.testing.assertDataFrameEqual` was the right tool for DataFrame assertions rather
than collecting rows and comparing manually. It handles two things that naive comparison
would miss: row ordering (Spark's distributed execution does not guarantee order without an
explicit `orderBy`) and floating-point precision (slight differences in floating-point
arithmetic should not fail tests). It also gives a readable diff when schemas or data
disagree.

`@pytest.mark.parametrize` was critical for the IP classification tests. I had one test
function with 8 input cases: a private IP, a public IP, a loopback address, a null input,
an empty string, an IP with an invalid octet, and two edge cases from the RFC ranges. Without
`parametrize` I would have written 8 nearly identical test functions. With `parametrize`
there is one function and a table of inputs and expected outputs. When a new edge case is
found in production, adding it to the parametrize list takes one line.

The most valuable test that came out of this process was a pagination edge case: the API
could return an empty-string `next_page_token` (`""`) when pagination was complete, rather
than `None`. In Python, an empty string is falsy -- `if not token: break` would correctly
stop on `None` but ALSO stop on `""`. However, `""` can also be a valid cursor value in some
APIs -- if the logic was `if token:` the empty string would not be treated as "end of
pagination." The parametrize test with an explicit `""` case caught this before it ever
hit a real API.

**Result**

Test suite caught 3 bugs before merge in its first two weeks: the null-handling crash in IP
classification, the empty-string pagination edge case, and an off-by-one in a date range
filter that was excluding the first day of each reporting period. All three were caught in
CI as failed PRs, none reached production.

---

### Technical Concept Breakdown

| Concept | What It Is | Why It Matters in Your Context |
|---------|-----------|-------------------------------|
| **`pytest`** | Python testing framework. Auto-discovers and runs `test_` prefixed functions. Fixture injection and parametrize are cleaner than `unittest`. | The standard for modern Python projects. Fixture system makes test setup composable and reusable. |
| **`@pytest.fixture`** | A function that sets up test dependencies and injects them into test functions by parameter name. | Reusable, scoped setup without inheritance hierarchies. Define once, use in any test that names it as a parameter. |
| **`scope="session"`** | Fixture created once per test run, shared across all tests. | For expensive resources (SparkSession, DB connections). Avoiding per-test startup is the difference between a 2-minute and 30-minute test suite. |
| **`scope="function"`** | Fixture recreated for each test (the default). | Test isolation. Prevents tests from sharing mutable state that causes order-dependent failures. |
| **`conftest.py`** | Special pytest file. Fixtures defined here are auto-discovered and available to all tests in the directory tree below. | Single place to define shared resources like SparkSession, DB connections, sample data factories. |
| **`pyspark.testing.assertDataFrameEqual`** | Checks schema and data equality between two DataFrames, handling row ordering and floating-point differences. | Spark does not guarantee row order in distributed execution. Naive comparison fails on correct output that happens to be in a different order. |
| **`unittest.mock.patch.object`** | Replaces a specific method on an object with a `MagicMock` for the duration of a `with` block. Restores the original on exit. | Isolate code from external dependencies (HTTP, database, file system). Tests are fast, deterministic, and don't require live infrastructure. |
| **`side_effect=[list]`** | Mock parameter: each successive call to the mock returns the next value from the list. | Simulate sequences of API responses without a real server. "Page 1 returns X, page 2 returns Y, page 3 returns empty." |
| **`@pytest.mark.parametrize`** | Runs one test function with multiple input/expected pairs as separate test cases. | One function covers all edge cases. Adding a new edge case requires one line in the parameter table, not a new test function. |
| **Test isolation** | Each test starts from a clean, independent state with no shared mutable objects. | Order-dependent test failures (tests that pass alone but fail when run after other tests) are the hardest category of test bugs to diagnose. Isolation prevents them. |

---

### How to Say It in the Interview

"For testing PySpark I used a session-scoped SparkSession fixture -- Spark takes 3 to 5
seconds to start, so you create it once per test run and share it. If you use function scope
you'd spend most of your test run on SparkSession startup overhead. For API client tests I
used `patch.object` with `side_effect` -- I give the mock a list of responses in sequence,
so I can simulate 'page 1, page 2, empty page' without any real HTTP calls. The test that
found the most valuable bug used `parametrize` to test IP classification across 8 cases --
private IP, public IP, null, empty string, invalid octet. The empty-string case caught a
real bug: `if not token: break` stops on empty string as well as None. For a pagination
guard, stopping early on `""` would truncate a legitimate multi-page extract silently."

---

### Likely Follow-up Questions

**"What is test isolation and why does it matter?"**
Test isolation means each test has its own independent state -- no test depends on the side
effects of a test that ran before it. Without isolation you get order-dependent failures:
the test passes when run alone but fails when run as part of the suite because a previous
test left shared state modified. These are the most difficult test failures to diagnose
because the bug appears in test B but the cause is in test A. Pytest's fixture system with
function scope enforces isolation by creating fresh state for each test.

**"What is a mock and when would you use it?"**
A mock is an object that replaces a real dependency with a controlled fake that records how
it was called and returns configurable values. Use mocks for: external dependencies that
would make tests slow (HTTP APIs, databases), non-deterministic dependencies (clocks, random
number generators), and dependencies that have side effects you don't want in tests (sending
emails, writing to production databases). The rule of thumb is to mock at the boundary of
your system -- replace the things your code calls, not the internals of your code itself.

---

## Python Story 5 -- Dagster Python: Assets, Resources, Sensors

> Dagster is Python-native. Assets, resources, schedules, and sensors are all Python
> functions. This shows you understand the programming model, not just the UI.

---

### STAR Story

**Situation**

At Epik the pipeline needed to be more than a cron job running a script. It needed: declarative
dependency tracking between data assets so Dagster could visualize and enforce lineage,
injectable resources so the same pipeline code could run against real Snowflake in
production and an in-memory fake in tests, proactive freshness monitoring with automatic
alerting when a Silver asset violated its 15-minute SLA, and event-driven triggering when
new files arrived in the ADLS Bronze container rather than fixed-schedule polling.

**Task**

Implement the medallion pipeline orchestration in Dagster using software-defined assets,
configurable resources, asset checks for data quality gating, and event-driven sensors.

**Action -- The design decisions**

Dagster's software-defined asset model is a direct implementation of Dependency Injection as
a first-class framework concept. A Dagster asset is a Python function decorated with `@asset`.
Its function parameters declare its dependencies -- both on data (upstream assets, injected as
their output types) and on infrastructure (resources, declared as `ResourceParam[T]` type
annotations). Dagster resolves these dependencies at runtime: it determines which upstream
assets to materialize first, then passes their outputs and the configured resource instances
into the function. The function itself contains pure business logic -- it does not manage
connections, does not handle retry, does not know which environment it is running in.

The `ConfigurableResource` base class from Dagster is a Pydantic model with an additional
method protocol for resource behavior. Declaring a resource as a `ConfigurableResource`
subclass means Dagster validates its configuration at launch time -- a missing required field
like `account` or `database` raises a validation error immediately when the pipeline starts,
not when the first asset function tries to use the resource mid-run. The production deployment
configuration file provides real Snowflake credentials. The test configuration provides a
mock resource with identical method signatures but no real connections -- it captures writes
into an in-memory dictionary that tests can assert against.

This is the practical power of Dependency Injection in the context of data pipelines: the
`silver_security_events` asset function is identical in production and test. The environment
changes via configuration, not via code branches. No `if os.environ['ENV'] == 'test'`
conditionals scattered through business logic.

Asset checks address a recurring problem in data engineering: transformation logic that
successfully runs but produces incorrect output. A pipeline might complete without raising
any exception while silently writing a DataFrame where 20% of `event_id` values are null
because of an upstream join issue. Without a check, this bad data propagates through to Gold
and into dashboards. An `@asset_check` is a Python function that receives the asset's output
and returns an `AssetCheckResult` with a `passed` boolean and optional metadata. The
`blocking=True` parameter is the critical configuration: when set, a failed check prevents
any downstream assets from materializing. The bad data is contained at the failing asset --
it cannot propagate downstream automatically.

Sensors implement event-driven pipeline triggering. A `@sensor` is a Python function that
Dagster calls on a configurable polling interval. It can yield `RunRequest` objects to
trigger pipeline runs, or yield nothing if there is no new work to do. The `run_key`
parameter on `RunRequest` is the idempotency mechanism -- Dagster maintains a record of
which `run_key` values have already triggered runs, and will not submit a duplicate run for
the same `run_key`. This means the sensor can poll every 60 seconds checking for new files
in ADLS, and even if it detects the same file multiple times across successive polls, it will
only trigger one pipeline run for that file. The sensor uses `context.cursor` to track where
the last successful check ended -- typically the timestamp of the most recently processed
file -- and updates the cursor after yielding all new run requests.

`FreshnessPolicy` is declared directly on an asset and specifies the maximum acceptable lag
between when the asset should have been materialized and when it actually was. Dagster
computes this continuously and surfaces violations in the UI and can push them to alerting
systems. This is proactive monitoring -- rather than waiting for an analyst to notice a stale
dashboard at 9 AM and file a ticket, the system alerts the data engineering team at 3 AM
when the lag first exceeds 15 minutes.

**Result**

Pipeline orchestration expressed entirely as Python functions with explicit dependency
declarations, testable via resource substitution, with data quality gates that automatically
blocked downstream materialization on bad data. The sensor-driven architecture reduced the
average latency from file landing in Bronze to Silver completion from 45 minutes (fixed
Databricks cluster startup + schedule wait) to under 10 minutes (serverless + event trigger).

---

### Technical Concept Breakdown

| Concept | What It Is | Why It Matters in Your Context |
|---------|-----------|-------------------------------|
| **Dependency Injection** | Passing dependencies (DB connections, API clients) into functions via parameters rather than constructing them inside. | Core software engineering principle enabling testability. Swap real dependencies for test fakes via configuration, not code changes. |
| **`@asset` decorator** | Marks a Python function as a Dagster software-defined asset. The function's return value is the asset's materialization. Parameters declare dependencies. | Declarative DAG construction. Dagster builds the dependency graph from function signatures rather than requiring explicit wiring code. |
| **`ConfigurableResource`** | Dagster base class (a Pydantic model) for injectable, type-safe resources with configuration schema. | Pydantic validation at launch time. Swappable via configuration between environments. |
| **`ResourceParam[T]`** | Type annotation on an asset function parameter telling Dagster to inject a resource of type T. | Zero-boilerplate resource injection. Dagster resolves and provides the right configured instance. |
| **`@asset_check`** | Decorator marking a function as a data quality check for a specific asset. Returns `AssetCheckResult`. | First-class data quality in the Dagster asset graph. Visible in UI, alertable, and optionally blocking. |
| **`blocking=True`** | Asset check option: a failed check prevents all downstream assets from materializing. | Hard data quality gate. Bad data is contained at the failing asset rather than propagating automatically through the pipeline. |
| **`@sensor`** | Python function polled by Dagster on a configurable interval. Yields `RunRequest` objects to trigger runs. | Event-driven orchestration. Trigger runs based on file arrivals, API events, or any arbitrary Python condition. |
| **`run_key`** | Unique idempotency token for a `RunRequest`. Dagster will not submit duplicate runs with the same `run_key`. | Sensors can poll frequently without launching duplicate pipeline runs for the same input file. |
| **`FreshnessPolicy`** | Policy on an asset declaring maximum acceptable lag before Dagster flags the asset as stale. | Proactive SLA monitoring. System alerts when data freshness is violated, before analysts report stale dashboards. |
| **`context.cursor`** | Sensor context field for storing the sensor's last-processed position between polls. | State persistence across sensor polls. Enables "check for files newer than the last run's timestamp." |

---

### How to Say It in the Interview

"In Dagster, the key Python design insight is that assets are pure functions: their
parameters declare their dependencies -- both upstream asset outputs and injectable resources
-- and Dagster resolves everything at runtime. The function itself contains only business
logic. This makes every asset function unit-testable by providing mock resources in the test
configuration without changing any code in the function. The `blocking=True` on asset checks
was important for us -- without it a check failure is just a warning in the UI. With it,
downstream assets literally cannot materialize if the upstream check fails. For event-driven
triggering I wrote a sensor with `run_key` set to the file path -- `run_key` is the
idempotency token, so even if the sensor polls the same file multiple times across successive
60-second intervals, Dagster only submits one run for it."

---

### Likely Follow-up Questions

**"What is dependency injection and why does it help with testing?"**
Dependency injection means that a function or class receives its dependencies as parameters
rather than constructing them internally. A function that constructs its own database
connection internally is hard to test because you can't control what connection it gets. A
function that receives a connection as a parameter can be tested by passing a fake connection
that records what was written to it. In Dagster, the resource system implements dependency
injection at the framework level -- you never write `conn = Snowflake.connect()` inside an
asset function, so tests can provide `InMemoryWriter` and production provides the real
`SnowflakeWriter` via configuration.

**"What is the difference between a sensor and a schedule in Dagster?"**
A schedule triggers runs at fixed time intervals -- every hour, every day at midnight.
A sensor triggers runs based on a condition -- a file arriving, an API returning new data,
an upstream asset completing with a specific metadata value. Sensors are event-driven;
schedules are time-driven. For our use case, a schedule would mean waiting up to 60 minutes
for the next scheduled run after a file landed. A sensor detected the file and triggered
within 60 seconds of landing.

---

## Python Concepts Quick Reference
> Fundamentals that come up in follow-up questions -- be ready to discuss any of these fluently.

---

### Core Patterns

**Decorators**
A decorator is a function that takes a function as input and returns a modified function.
The `@decorator` syntax is shorthand for `func = decorator(func)`. Common use cases in
data engineering: `@retry` for automatic retry logic, `@lru_cache` for memoization,
`@pytest.fixture` for test setup, `@asset` for Dagster asset declaration.

**Generators and `yield`**
A generator function uses `yield` to produce values lazily. When the caller requests the
next value, execution resumes from the `yield` statement. Memory usage stays flat because
the generator only holds the current item in memory. The `yield from` syntax delegates to a
sub-generator, chaining lazy sequences without materializing intermediate collections.

**Context Managers and `with`**
The `with` statement ensures cleanup code always runs by calling `__exit__` (or the
`@contextmanager` function's `finally` block) when the block exits, whether normally or via
exception. Use for any resource that needs cleanup: database connections, file handles,
temporary directories, transaction blocks.

**`functools.lru_cache`**
`@lru_cache(maxsize=128)` memoizes a function's return values indexed by its arguments.
On repeated calls with the same arguments, it returns the cached result without re-executing
the function. LRU = Least Recently Used eviction when the cache is full. Use for: expensive
database lookups called repeatedly with the same tenant or dimension keys.

**Custom exceptions**
Define a base exception class for your domain (`class PipelineError(Exception)`) with
specific subclasses (`ExtractionError`, `ValidationError`). This lets callers write
`except ExtractionError` to handle extraction failures specifically while letting other
exceptions propagate. Avoid catching broad `Exception` -- it swallows bugs silently.

**`asyncio` for I/O concurrency**
`async def` functions are coroutines. `await` suspends the coroutine while waiting for I/O,
allowing the event loop to run other coroutines. `asyncio.gather()` runs multiple coroutines
concurrently. For 15 parallel API calls: sequential = 15 x 2s = 30s. Async concurrent = ~2s
total. The GIL is not a problem here because `await` yields the thread voluntarily -- there
is no CPU contention, just I/O waiting.

---

### Python Fundamentals Answer Bank

| Question | Precise Answer |
|----------|---------------|
| **What is the GIL?** | Global Interpreter Lock. Prevents multiple Python threads from executing bytecode simultaneously. Not a bottleneck for I/O-bound work (threads yield at I/O). Bottleneck for CPU-bound parallelism -- use multiprocessing instead. |
| **`is` vs `==`** | `is` checks object identity (same memory address). `==` checks value equality. `x is None` is correct; `x == None` works but is not idiomatic -- None is a singleton so identity check is appropriate. |
| **Mutable default bug** | `def f(tags=[])` creates one list object at function definition time, shared across all calls. Fix: `def f(tags=None): tags = tags or []`. In dataclasses: `field(default_factory=list)`. |
| **Shallow vs deep copy** | `copy.copy()` copies the container but shares references to nested objects. `copy.deepcopy()` recursively copies everything. Matters when nested mutable objects (lists of lists, dicts of dicts) need to be independent copies. |
| **`*args` and `**kwargs`** | `*args` captures extra positional arguments as a tuple. `**kwargs` captures extra keyword arguments as a dict. Use in wrapper functions that need to forward arbitrary arguments to the wrapped function. |
| **`zip(strict=True)`** | Raises `ValueError` if the two iterables have different lengths. Without `strict=True`, `zip` silently truncates to the shorter iterable -- this can silently lose data when pairing two lists that should have the same length. |
| **`__repr__` vs `__str__`** | `__repr__` is the unambiguous developer representation -- ideally `eval(repr(obj)) == obj`. `__str__` is the human-readable representation. `print(obj)` calls `str`. If only one is defined, `repr` is used as fallback. |
| **`@property`** | Makes a method callable without parentheses. Used for computed attributes and to add validation to attribute access via getters and setters without changing the calling interface. |
| **`collections.defaultdict`** | `defaultdict(list)` automatically creates an empty list on first access of any missing key. Eliminates `if key not in d: d[key] = []` boilerplate in grouping logic. |
| **`itertools.chain`** | `chain(list_a, list_b)` iterates over both sequences as one without concatenating them into a new list. Memory-efficient for chaining large iterables. |
| **Pickling** | Python's object serialization protocol (`pickle.dumps`/`pickle.loads`). Used by `multiprocessing` for inter-process communication and by PySpark for row-by-row UDF serialization. The reason regular Python UDFs in Spark are slow. |
| **`__slots__`** | Replacing the per-instance `__dict__` with a fixed-size attribute array. Memory benefit: 30-50% reduction for classes with millions of instances. Tradeoff: can no longer add arbitrary attributes dynamically. |

---

### Pandas Optimization Quick Reference

| Pattern | Why It Helps |
|---------|-------------|
| `df["col"].astype("category")` | Low-cardinality string columns (status codes, event types) stored as integer indices. 5-10x memory reduction. |
| `pd.read_csv(path, chunksize=N)` | Process CSV files larger than RAM by iterating N-row chunks. Never loads the full file. |
| `df.query("severity > 5 and tenant == @tid")` | Readable boolean filtering. The `@var` syntax references Python local variables inside the query string. |
| `df.eval("roi = (revenue - cost) / cost")` | Vectorized multi-column expression evaluated in one pass. Avoids creating intermediate Python objects for each operation. |
| Avoid `df.iterrows()` | Row-by-row Python iteration over a DataFrame is 100 to 1000x slower than vectorized column operations. Use `.apply()`, `.map()`, or direct column arithmetic. |
| `pd.to_datetime(col, utc=True)` | Always normalize timestamps to UTC on ingest. Timezone-naive timestamps silently produce wrong results in time-based window calculations. |

---

# CHALLENGES, FAILURES & DEBUGGING STORIES
> These are the questions that separate senior engineers from junior ones: "Tell me about
> a time you failed," "What's the hardest production bug you've debugged?", "Tell me about
> a mistake that had business impact." Answer these with specificity and ownership.
> The formula: what broke, why it was hard to find, what you changed, what you learned.

---

## Failure 1 -- Silent Data Multiplication from a PySpark Join (Epik Solutions)

> Type: Silent data corruption / wrong join semantics
> Impact: Security event counts inflated 3x in compliance dashboards for 6 days before detection

---

### What Happened

The Bronze-to-Silver pipeline at Epik joined raw security events against a tenant metadata
table to enrich each event with its tenant's compliance tier and regulatory region. This join
had been running in production for two weeks without any obvious error. No exceptions, no
failed pipeline runs, clean Dagster materialization history. The pipeline looked healthy.

Six days in, an analyst raised a ticket: event counts in the Acuity compliance dashboards
were approximately three times higher than the counts the client's own SIEM system showed
for the same time windows. The discrepancy was noticed only because the client had a
cross-system sanity check in their weekly review process.

### Why It Was Hard to Find

The pipeline's monitoring only checked for job completion and schema compliance -- it did not
verify that output row counts were in the expected range relative to input row counts. A
successful pipeline run with no schema violations and no exceptions looked identical to a
correct one. The inflation was not 2x or 10x (which would have been obvious) but roughly
3x, which matched the fact that three different data delivery methods had been configured
per tenant in the metadata table -- three rows in the metadata table per tenant, one per
delivery channel.

The join I had written was on `tenant_id` alone. Since the metadata table had three rows per
tenant (one for each channel), every event for that tenant joined to all three, tripling the
count. This is a classic join fan-out from an undetected one-to-many relationship. The
correct join key was the composite `(tenant_id, primary_channel)` -- only one row per tenant
per primary channel. I had looked at the metadata table's documented schema and assumed
`tenant_id` was unique, which it was in the original version but was no longer true after a
schema change two weeks before the pipeline launched.

### What I Did

The debugging process had three stages. First I verified the symptom by comparing the Silver
table row count for a specific tenant and date window against the raw event count from the
Bronze table -- 3.1x ratio confirmed for every tenant. Second I ran the same join logic
manually against a 1-day sample and computed the `GROUP BY tenant_id, COUNT(*)` on the
result versus the same aggregation on the Bronze input. The ratio appeared in the first
query. Third I examined the metadata table and found three rows per tenant where I had
assumed one.

The immediate fix was to correct the join predicate to include the composite key and backfill
the affected Silver partitions by reprocessing the prior six days through Databricks.

The preventive fix was adding a `@asset_check` with `blocking=True` that computed the ratio
of Silver row count to Bronze row count for the same event date and failed the check if the
ratio exceeded 1.1 (a 10% tolerance for legitimate deduplication). This check would have
caught the issue on the first pipeline run.

### What I Learned

Row count monitoring at each pipeline stage is not optional for production data pipelines.
Schema validation (is the schema correct?) is table stakes. Count validation (is the output
count in an expected range relative to the input?) is what actually catches semantic errors
like fan-out joins. The most dangerous failures are the ones that produce no exceptions and
look healthy in all the places you are monitoring.

For join correctness specifically: never assume uniqueness of a join key without
explicitly verifying it with a `COUNT(DISTINCT key) = COUNT(*)` check, or by reading the
source system's data dictionary rather than inferring from the schema. Schema change
notifications should trigger a review of all joins on that table.

---

### How to Say It in the Interview

"We had a silent data multiplication bug in production at Epik that inflated security event
counts by 3x for six days before an analyst caught it. The pipeline ran without errors,
passed schema validation, and had clean job completion history -- there was nothing in our
monitoring that would flag it. The root cause was a join fan-out: I joined events to a
tenant metadata table on tenant_id alone, assuming it was unique, but a schema change two
weeks earlier had added three rows per tenant for different delivery channels. Every event
was joining to all three rows. The fix was correcting the join key to the composite and
backfilling six days. The preventive fix was an asset check that compared Silver-to-Bronze
row count ratios and blocked materialization if the ratio exceeded 1.1. The lesson for me
was that count validation is as important as schema validation -- a pipeline that runs
successfully but produces wrong counts is worse than a pipeline that fails, because you
don't know the data is wrong."

---

### Likely Follow-up Questions

**"How would you design a monitoring system to prevent this class of issue?"**
Three layers: First, row count ratio checks at each pipeline stage -- Silver count should be
within an expected range of Bronze count. An asset check or Great Expectations expectation
that asserts `output_count between 0.9 * input_count and 1.1 * input_count` catches fan-out
and silent deduplication. Second, business-level metric monitoring -- the end metric (total
events per tenant per day) should be within expected bounds based on historical distributions.
Statistical anomaly detection on these metrics catches issues that count-ratio checks miss.
Third, cross-system reconciliation for high-stakes pipelines: compare counts between your
pipeline's output and the source system's own counts for the same time window.

---

## Failure 2 -- Pagination Truncation Caused Missing Compliance Records (Samay Systems)

> Type: Silent data loss / subtle Python truthiness bug
> Impact: 11 days of incomplete trade records for two clients -- caught during internal audit

---

### What Happened

At Samay, one of the regulatory API clients returned a `next_page_token` field in its
pagination response. When there were no more pages, the API was documented to return an
empty string for `next_page_token`. My pagination logic checked `if not token: break` to
stop pagination. In Python, an empty string is falsy -- `not ""` evaluates to `True` -- so
this condition correctly stopped on an empty string.

The problem emerged when the API was updated (without a changelog announcement) to return
`next_page_token` as a value of `"0"` rather than `""` to indicate end of pagination. The
string `"0"` is truthy in Python. My code now treated `"0"` as a valid cursor and passed it
in the next request's parameters. The API, receiving `next_page_token="0"` as if starting
fresh, returned the first page again. The pagination looped on the last two pages indefinitely
until the pipeline hit its configured timeout, then terminated gracefully with the last
successful write -- which was partial.

### Why It Was Hard to Find

The pipeline ran to completion with no errors. It hit the timeout and exited cleanly because
the timeout handling wrote whatever had been extracted to Snowflake and returned success.
The extracted count was lower than expected but there was no alerting on absolute record
counts -- only on pipeline success or failure. The issue was discovered during an internal
audit comparing the Snowflake staging table against a re-extract from the source API.

The 11-day window meant there were 11 days of trade records that had been partially
extracted -- the first N pages of trades per day existed in Snowflake, the remaining pages
did not. Because the API returns trades in reverse chronological order, the missing records
were the oldest trades within each day, which were less likely to appear in recent queries.

### What I Did

The audit finding showed count discrepancies by day. I reproduced the issue by re-running
the extractor against a specific day's data with verbose logging enabled -- the log showed
the page token cycling: page 1 response contained token `"0"`, the client sent page 2 with
`cursor="0"`, the API returned page 1 again. The loop was visible in the logs immediately.

The fix was changing the termination condition from the falsy check to an explicit `None`
check: `if token is None: break`. This stops on `None` only and treats any other value --
including empty string or `"0"` -- as a valid cursor, letting the API's actual end-of-data
signal drive termination (the empty `data` array in the response body) rather than the token
value.

The backfill required identifying the affected date ranges per client, re-extracting from
the API for those dates, and using a merge strategy (not an overwrite) to fill in the missing
records without disturbing the records that had been correctly extracted.

The preventive fix was adding a configurable maximum page count to the extractor, after which
it would log a warning and raise an exception rather than continuing silently. An 11,000-page
extract would be so far outside the historical norm for these APIs that an exception would
have been the right response, triggering manual investigation rather than a timed-out partial
write.

### What I Learned

Explicit `None` checks (`if token is None`) are always safer than falsy checks (`if not token`)
for sentinel values in protocol behavior. An empty string and `None` are both falsy in
Python but mean semantically different things -- `None` usually means "absent/not provided"
while `""` means "explicitly empty string." The distinction matters when you are handling
API response fields where the API contract can change the sentinel value format.

The broader lesson is about silent success: a job that completes within its timeout and
writes some data looks successful in every operational metric. Count validation against
source-side record counts is the only way to detect partial extracts.

---

### How to Say It in the Interview

"We had a pagination bug at Samay that caused 11 days of incomplete compliance data for two
clients. The root cause was a Python truthiness issue: my pagination loop used `if not token:
break` to stop when the API indicated end of pages. The API returned an empty string for
end-of-pagination, which is falsy, so it worked correctly. Then the API updated its contract
to return the string `'0'` instead of empty string -- `'0'` is truthy in Python, so my code
treated it as a valid cursor and looped forever until the timeout. The pipeline completed
cleanly every time, just with partial data, because the timeout handler wrote whatever it had.
The fix was changing to `if token is None: break` -- explicit None check instead of a falsy
check. The lesson that stuck with me was the difference between `not token` and `token is None`:
they look similar but behave differently for any falsy non-None value like empty string,
zero, or False. For sentinel values in protocol contracts, always use explicit identity
checks."

---

## Failure 3 -- dbt Incremental Model Missing Soft-Deleted Records (Samay Systems)

> Type: Architectural design error / incremental strategy mismatch
> Impact: Stale data in Silver for 3 months -- compliance records that had been revoked at
> source continued appearing as active in Snowflake

---

### What Happened

At Samay, a dbt incremental model loaded compliance records from a staging Snowflake table
into the Silver layer. The incremental strategy used an `updated_at` timestamp filter: on
each run, the model queried for records where `updated_at` was greater than the last run's
maximum `updated_at` and merged them into the Silver table. This is a standard incremental
pattern and it worked correctly for new records and updates.

What it did not handle was soft deletes. The source compliance system marked records as
deleted by setting a `is_deleted` flag to `True` -- but it did NOT update the `updated_at`
timestamp when doing so. From the incremental model's perspective, a soft-deleted record
was indistinguishable from a record that simply had not changed. It was never included in
the incremental load because its `updated_at` was old. The Silver table continued to show
these records as active compliance records.

### Why It Was Hard to Find

The issue had no observable failure. Pipeline ran daily, completed successfully, produced
no schema errors. The compliance records in question were valid records at the time they
were first loaded, so they passed all business validation rules. The only way to detect the
issue was to cross-reference Snowflake's Silver table count against the source system's
"active records" count -- and the source system had no obvious reporting interface that made
this comparison easy.

The issue surfaced three months in when a client noticed that two contractors who had been
removed from their compliance portal weeks earlier were still appearing in the Samay
compliance reporting dashboard. Manual investigation traced the discrepancy from the
dashboard to the Gold model to the Silver model to the incremental logic.

### What I Did

The first step was quantifying the damage: I compared the full set of `record_id` values
in the Silver table against the source system's active record list. The count showed 847
records in Silver that the source system considered deleted or inactive.

The fix required re-evaluating the incremental strategy. The `updated_at`-based approach
was fundamentally wrong for this source because the source system's soft-delete mechanism
didn't touch `updated_at`. I had two options: either request that the source system fix
its soft-delete logic to update `updated_at` (rejected -- would require changes to a
production compliance system we didn't own), or switch the dbt incremental model to a full
re-scan strategy with a merge predicate.

I switched the model from `strategy: incremental` to a daily full merge. The model now
reads all records from the staging table, compares them against the Silver table on `record_id`,
and applies the full change set: insert new records, update changed records, and mark any
records in Silver that are absent from the source scan as `is_deleted=True` with a deletion
timestamp. This is more expensive than an incremental load (a daily full scan of the staging
table rather than a filtered query) but guaranteed correctness for all change types.

The backfill deleted the 847 stale records from Silver with a `deleted_at` timestamp
matching the best estimate of when they were removed from source.

### What I Learned

The right incremental strategy depends entirely on how the source system signals changes.
The standard `updated_at` incremental approach assumes the source system is well-behaved:
every change -- including deletions -- updates the `updated_at` field. Many production
systems are not well-behaved. Before choosing an incremental strategy, the right question
is: "Does this source system update its modification timestamp for ALL types of changes,
including soft deletes?" If the answer is "I don't know," the safer default is a full merge
strategy with tombstone handling, even if it is more expensive.

The other lesson was about the gap between "pipeline succeeds" and "data is correct." A
pipeline that runs daily with no errors for three months can silently accumulate a growing
delta of wrong data if the incremental logic has a blind spot. Business-level reconciliation
checks -- total active record counts compared against source -- are the only reliable
detection for this class of issue.

---

### How to Say It in the Interview

"The hardest data correctness bug I dealt with at Samay was a dbt incremental model that was
silently missing soft-deleted compliance records for three months. The incremental strategy
used an `updated_at` filter to identify changed records -- completely standard. But the source
system's soft-delete process set an `is_deleted` flag without updating `updated_at`. From
the incremental model's perspective, those deleted records were unchanged and were never
re-processed. They stayed active in Snowflake while the source showed them as deleted. The
only reason we caught it was a client noticed two removed contractors still appearing in
our dashboards. The fix was switching from an `updated_at` incremental to a full daily
merge with tombstone handling -- more expensive, but the only correct approach for a source
system that doesn't update modification timestamps on soft deletes. The lesson: always
validate the source system's change-signaling behavior before choosing an incremental
strategy. Don't assume `updated_at` covers all change types."

---

## Failure 4 -- PySpark Data Skew OOM Failure on Large Tenant (Epik Solutions)

> Type: Infrastructure failure / data distribution problem
> Impact: Security event pipeline OOM-crashing for largest client, blocking Silver
> materialization for 14 hours

---

### What Happened

At Epik, the Silver-to-Gold pipeline aggregated security events by `tenant_id` and `event_type`
to compute daily summary statistics. This pipeline ran without issues for three months while
clients were in onboarding. When the largest enterprise client (a financial services firm
with roughly 150x the event volume of any other client) reached full production traffic,
the Spark job started failing with executor OOM errors consistently.

The error message was `ExecutorLostFailure (executor 3 exited caused by one of the running
tasks)` followed by `java.lang.OutOfMemoryError: GC overhead limit exceeded`. The job would
fail at the same stage every time: the window function computing rolling statistics within
each `tenant_id` partition.

### Why It Was Hard to Find

OOM errors in Spark are often misdiagnosed as infrastructure issues -- "we need bigger executors"
is the first instinct. I had initially gone down that path: submitted a request to increase
executor memory from 8GB to 16GB. The job still OOM'd, just slightly later. Doubling memory
again would have been expensive and still wrong.

The Spark UI told the real story. The "Tasks" tab for the failing stage showed 199 tasks
completing in under 2 seconds each, and one task running for 40 minutes with an input size
of 82GB. That one task was holding all of the largest client's event data because the
`partitionBy("tenant_id")` in the window function had placed all of their events in a single
Spark partition -- and that partition was assigned to one executor.

This is data skew: when your partition key has a highly unequal distribution (one tenant has
150x the rows of any other), partitioning by that key creates one enormous partition and
hundreds of tiny ones. The large partition overwhelms the executor handling it while the
others sit idle. Adding more executor memory treats the symptom but does not fix the problem.

### What I Did

The diagnostic was comparing task execution times and input sizes across the failing stage
in the Spark UI. Once data skew was confirmed as the cause, the fix was a salting strategy
on the partition key.

Salting works by appending a random number (the "salt") to the partition key, transforming
a skewed single-tenant partition into N evenly distributed partitions. For a `COUNT` or
`SUM` aggregation, you can safely salt, compute partial aggregations per salt bucket, and
then merge the partial results. For a window function that requires seeing all of a tenant's
events ordered by timestamp (as our rolling event rate calculation did), salting is
incompatible with a single window -- you cannot split a time-ordered window computation
across multiple partitions.

The right fix for the window function case was a two-phase approach: compute the initial
salted aggregations at a sub-tenant level (by `tenant_id` plus `event_source_region`, which
distributed the large tenant's data across 12 partitions), then compute the cross-region
totals in a second aggregation pass. This restructuring required separating the "per-region
rate" and "total-tenant rate" statistics into two models, but the data was actually more
granular and useful at the regional level for security analysis purposes.

### What I Learned

Increasing executor memory is the wrong first response to a Spark OOM in a data aggregation
pipeline. The right first step is examining the Spark UI for task time and input size
distribution across the failing stage. A task that takes 50x longer than its siblings or
processes 100x more data than its siblings is the diagnostic signature of data skew, and no
amount of additional memory fixes a distribution problem.

The broader lesson is about cardinality assumptions: a partition key that is balanced today
may become severely skewed when a single large customer onboards. Pipeline design should
include analysis of the worst-case key distribution, not just the average case.

---

### How to Say It in the Interview

"At Epik, our Silver-to-Gold pipeline started OOM-crashing after the largest enterprise
client went to full production. Initial instinct was to increase executor memory -- which
didn't fix it. The Spark UI told the real story: the Tasks view showed 199 tasks finishing
in 2 seconds each and one task running for 40 minutes with 82GB of input. Classic data skew:
`partitionBy('tenant_id')` put all of this client's events in one partition on one executor.
The fix was restructuring the window computation to partition by a more granular key --
`tenant_id` plus `event_source_region` -- which distributed the large tenant's data across
12 partitions instead of 1. The statistics became more granular (per-region rather than
per-tenant only) but also more useful for security analysis. The lesson: Spark OOM with a
skewed task time distribution is a data skew problem, not a memory problem. Look at task
input sizes in the Spark UI before touching any memory configuration."

---

### Likely Follow-up Questions

**"How do you detect data skew before it causes failures?"**
Three approaches: First, analyze key cardinality and distribution in the source data before
building the pipeline. A simple `GROUP BY partition_key, COUNT(*)` showing the top 10
groups by count reveals skew. Second, monitor Spark stage metrics in production -- the ratio
of max task duration to median task duration within a stage is the skew indicator. A ratio
above 5x warrants investigation. Third, instrument your pipeline with partition size logging:
compute the partition size distribution before any wide transformation and alert if the
max-to-median ratio exceeds a threshold.

---

## Failure 5 -- Terraform State Drift Caused 6-Hour Pipeline Outage (Epik Solutions)

> Type: Infrastructure management failure / IaC drift
> Impact: All Epik pipelines failing with cryptic permission errors for 6 hours on a Monday

---

### What Happened

At Epik, Azure infrastructure was managed with Terraform: Key Vault for secrets, Event Hubs
namespaces, Databricks workspaces, Storage accounts, and their associated RBAC and access
policy configurations. A Monday morning deployment ran successfully through CI/CD, and then
every pipeline started failing within minutes. The error messages were cryptic Azure SDK
exceptions about secret retrieval failures -- something along the lines of "The user, group,
or application does not have secrets get permission on key vault."

The pipelines had been working perfectly the previous Friday. No code changes had merged
over the weekend. The deployment that morning had not touched Key Vault configuration.

### Why It Was Hard to Find

The immediate suspicion was the Monday deployment -- but reviewing the Terraform plan that
had been applied showed no Key Vault changes. The plan had only touched Event Hubs consumer
group settings. This was correct and expected.

The problem was that a developer on the team had manually added their personal service
principal to the Key Vault access policy on Friday afternoon to debug a separate issue. They
forgot to remove it when they were done. Because Terraform's state file did not know about
this manual addition, when Terraform applied on Monday it compared its desired state
(no manual service principal in the access policy) against the live state (access policy
with both the correct managed identity AND the manual service principal), determined that
the difference was in scope, and removed the manual service principal as an "untracked
resource."

The problem was that in doing so, Terraform also reset the access policy block format, which
in an older version of the `azurerm` Terraform provider reset all access policies for the
vault to only those explicitly listed in the Terraform configuration -- and our Terraform
configuration was missing the Databricks managed identity that the pipelines used for secret
retrieval. The managed identity had been added to the Key Vault via the Azure portal six
months earlier (before Terraform managed this resource) and had never been codified into
the Terraform configuration.

### What I Did

The immediate fix was identifying the failing secret retrieval, locating the correct managed
identity for the Databricks pipeline service principal, and manually adding it back to the
Key Vault access policy via the Azure portal. Pipelines recovered within 10 minutes once
the permission was restored.

The root cause fix was a two-day effort to audit every manually-created Azure resource
against the Terraform state file and codify the discrepancies. The Key Vault access policy
was the obvious one, but the audit found three other resources that existed in Azure but not
in Terraform state -- a Network Security Group rule, a storage account lifecycle policy, and
a diagnostic settings configuration. All four were imported into the Terraform state using
`terraform import` and their corresponding resource blocks added to the configuration.

The process control fix was establishing a team rule: no manual portal changes to
Terraform-managed infrastructure. Any change that needs to be made in production must go
through a Terraform PR. For debugging scenarios requiring temporary access, changes must be
documented and either reverted immediately or codified in a PR within 24 hours.

We also added a `terraform plan` job to the CI pipeline that ran on a nightly schedule
against the live production environment and alerted if any non-empty plan was detected.
A non-empty plan against a production environment where no changes are expected means drift
has occurred -- either a manual change in Azure or a missing resource in Terraform state.

### What I Learned

IaC drift is an insidious class of problem because it accumulates silently. Individual manual
changes seem harmless in the moment -- adding temporary debug permissions, tweaking a
resource setting directly in the portal for speed. But each change widens the gap between
what Terraform thinks the infrastructure looks like and what it actually looks like. The next
Terraform apply becomes unpredictable because it reconciles the delta against what it
believes to be the desired state, and that reconciliation may remove or modify things you
didn't intend to touch.

The specific lesson about Terraform access policies: when Terraform manages a resource block
that has a list attribute (like access policies), it enforces the full list on apply -- any
member of the list not in the Terraform configuration is removed. This is not a bug, it is
correct idempotent behavior. The failure was our configuration not being complete.

---

### How to Say It in the Interview

"We had a 6-hour pipeline outage at Epik on a Monday morning caused by Terraform state
drift. The root chain was: a developer manually added a temporary service principal to a
Key Vault access policy on Friday for debugging and forgot to remove it. Monday's Terraform
apply saw the drift and reconciled it -- but the reconciliation reset the full access policy
list to only what was in Terraform state, which was missing the Databricks managed identity
that all our pipelines used for secret retrieval. The managed identity had been added via
the portal six months before Terraform managed that resource and had never been codified.
Everything failed with cryptic permission errors within minutes of the deploy. The fix was
re-adding the managed identity, then spending two days doing a full Terraform state audit
and importing all the manually-created resources. The process fix was adding a nightly
`terraform plan` against production: if the plan is non-empty when no changes are expected,
drift has occurred and someone gets paged. Manual portal changes to Terraform-managed
infrastructure became a team policy violation."

---

### Likely Follow-up Questions

**"What is Terraform state drift and how do you prevent it?"**
Terraform state drift occurs when the actual infrastructure diverges from what Terraform's
state file records -- typically from manual changes made outside of Terraform. On the next
`apply`, Terraform reconciles the delta between desired state (in configuration) and
recorded state (in the state file), which can result in unexpected modifications or
deletions of resources that exist in reality but not in state. Prevention: establish a
"Terraform-managed means hands off" policy for production resources, add nightly drift
detection plans in CI, use `terraform import` to codify existing resources before Terraform
takes ownership of them, and use resource locks in Azure to prevent accidental manual
modifications to critical infrastructure.

---

## Failure 6 -- Debugging a Memory Leak in a Long-Running Python Ingestion Process (Zemoso)

> Type: Performance / resource management failure in production Python
> Impact: Ingestion service restarting every 4-6 hours due to OOM, dropping events

---

### What Happened

At Zemoso, the LabOps platform ran a Python-based ingestion service that continuously
polled laboratory instrument APIs every 30 seconds to collect measurement data. The service
was deployed as a container. Within a week of deployment, the on-call team noticed the
container was restarting roughly every 4 to 6 hours -- the OOM killer was terminating it
when memory usage exceeded the container's limit.

The service was not doing anything that should accumulate memory. Each polling loop fetched
data from an API, transformed it into a DataFrame, wrote to PostgreSQL, and discarded the
DataFrame. At least, that was the design.

### Why It Was Hard to Find

The first thing I checked was the obvious: the DataFrames themselves. The polling loop was
using Pandas, and each cycle created a new DataFrame. I verified that the DataFrame reference
went out of scope at the end of each loop iteration and assumed Python's garbage collector
would reclaim the memory. This was correct -- DataFrames were not the leak.

The actual leak was in the logging configuration. The service used Python's standard
`logging` module. During initialization, a custom log handler had been added that stored
log records in an in-memory list (intended for a future "retrieve last N log messages via
API" feature that had never been implemented). This handler was appended to the root logger
with no maximum size on the in-memory list. Every log message from every library in the
process -- not just application logs but also library debug logs from `requests`, `sqlalchemy`,
and the PostgreSQL driver -- was being stored in this growing list. Over 4-6 hours of
30-second polling with verbose library logging, the list accumulated hundreds of thousands
of log records.

The logger handler was invisible in the normal code path -- it was configured in the
application startup code and then never referenced again, but it held a reference to every
log record created, preventing garbage collection.

### What I Did

I added memory profiling to the container using the `tracemalloc` module from Python's
standard library, which tracks memory allocations and can report the top N allocation sites
by size. I attached it to the running service by adding a debug endpoint that returned the
`tracemalloc` snapshot in JSON format. After running for 2 hours, the snapshot showed the
in-memory log handler's list as the dominant allocation -- thousands of `logging.LogRecord`
objects.

The immediate fix was removing the in-memory log handler (the feature it was built for was
never going to be implemented anyway). The proper fix if we had kept it would have been
bounding the list to the last 1000 records using a `collections.deque(maxlen=1000)` -- a
double-ended queue with a maximum length automatically discards the oldest item when the
limit is reached.

I also added a memory metrics endpoint to the service that the monitoring system polled
every minute, logging the process RSS memory size. This made memory growth visible on a
dashboard rather than discoverable only when the container restarted.

### What I Learned

Memory leaks in Python are less common than in C/C++ because of garbage collection, but they
do occur. The common sources are: objects stored in containers that are never cleared
(logging handlers, caches without eviction, global registries), circular references that
prevent reference-count-based collection (Python's cyclic GC handles these but with delay),
and large objects stored in global scope or class variables rather than local scope.

The `tracemalloc` module is underused for Python memory debugging. It is part of the standard
library, has no dependencies, and can be enabled in production with a feature flag for
debugging sessions. The key function is `tracemalloc.take_snapshot()` followed by comparing
two snapshots over time -- the difference shows what allocations are growing.

The `collections.deque(maxlen=N)` pattern is the right way to implement any in-memory
bounded buffer -- a recent-events store, a log tail, a sliding window of metrics. It is more
memory-safe than a list with a periodic `del list[:-N]` trim because it enforces the bound
atomically on every append.

---

### How to Say It in the Interview

"At Zemoso I debugged a Python service that was OOM-crashing every 4 to 6 hours in
production. My first suspicion was Pandas DataFrames not being released, but I verified
those were going out of scope correctly. The actual leak was a custom logging handler added
at startup that stored every log record in an unbounded Python list -- including verbose
debug logs from third-party libraries. After 4 hours of 30-second polling with library debug
logging enabled, the list had hundreds of thousands of LogRecord objects. I found it using
`tracemalloc`, Python's standard library memory profiler, by comparing two snapshots taken
an hour apart -- the growing allocation was clearly the log record list. The fix was removing
the unused handler. The right pattern if you need an in-memory log buffer is
`collections.deque(maxlen=1000)` -- a deque with a max length automatically discards the
oldest element on each append, so it is memory-bounded by design."

---

### Lessons Learned Summary

| Story | Root Cause Category | Prevention Pattern |
|-------|--------------------|--------------------|
| Silent join fan-out | Wrong join key assumption + no count monitoring | Asset check asserting Silver/Bronze row ratio; verify join key uniqueness before use |
| Pagination truncation | Python truthiness vs explicit None check | Always use `is None` for sentinel checks on protocol values |
| dbt incremental blind spot | Incremental strategy mismatch with source change behavior | Validate source soft-delete behavior before choosing incremental strategy; prefer full merge for uncertain sources |
| PySpark data skew OOM | Partition key cardinality assumption failed at scale | Analyze key distribution before building aggregation pipeline; monitor max/median task duration ratio |
| Terraform state drift | IaC drift from manual portal changes + incomplete state | Nightly drift detection in CI; codify all manually-created resources; enforce no-manual-changes policy |
| Python memory leak | Unbounded in-memory container in global scope | Prefer bounded collections (`deque(maxlen=N)`) for any in-memory buffer; use `tracemalloc` for memory debugging |

---

# EPIK SOLUTIONS — Senior Data Engineer (Jul 2025 – Present)
### *Enterprise Security Data Platform*

---

## Bullet 1 — Azure Databricks Medallion Lakehouse + Delta Live Tables

> *"Architected Azure Databricks medallion lakehouse (Bronze/Silver/Gold) using Delta Live Tables and PySpark, ingesting 50M+ daily security events with schema enforcement and full lineage tracking via Unity Catalog."*

---

### STAR Story

**Situation**  
Epik Solutions was building an enterprise security analytics platform for large clients — think security operations centers that needed to detect threats across millions of firewall logs, endpoint events, and cloud audit trails. Their existing setup was a flat blob of raw files dumped into Azure Storage with no organization, no quality guarantees, and no way to trace where data came from. Analysts were writing fragile SQL against raw files with no idea if the data was valid or stale.

**Task**  
Design the foundational data architecture — the system that everything else would sit on top of. My responsibility was to build a structured, reliable, traceable data platform that could handle 50 million+ events per day and still guarantee data quality at every stage.

**Action — Step by step**

1. **What a Medallion Lakehouse is and why it matters**:  
   Instead of one chaotic raw data layer, I designed three distinct layers in ADLS Gen2:  
   - **Bronze**: Raw, append-only data. Exactly as it arrived from the source. No transformations. If something breaks downstream, you always have the original.  
   - **Silver**: Cleaned, typed, deduplicated, schema-enforced. Bad records filtered out or quarantined, timestamps normalized to UTC, columns cast to correct types.  
   - **Gold**: Business-ready, pre-aggregated tables. What analysts and dashboards actually query. Optimized for read performance.  
   This is called the **Medallion Architecture** — coined by Databricks. It gives you both a historical raw record AND a clean query layer simultaneously.

2. **Delta Live Tables (DLT)**:  
   Instead of writing individual PySpark jobs and chaining them manually, I used **Delta Live Tables** — Databricks' declarative pipeline framework. You define each table as a Python function decorated with `@dlt.table` and declare its upstream dependencies. DLT handles:  
   - Dependency resolution (runs upstream tables before downstream ones automatically)  
   - **Auto-recovery**: if a job fails mid-run, it knows exactly which tables succeeded and which to re-run  
   - **Data quality constraints**: you annotate each table with `@dlt.expect_or_drop("valid_ip", "src_ip IS NOT NULL")` — rows violating the constraint are either dropped, quarantined, or cause the pipeline to fail depending on severity  
   - **Pipeline monitoring**: a built-in UI showing table-by-table run status, row counts, expectation pass/fail rates  

3. **PySpark transformations**:  
   Between Bronze and Silver I wrote PySpark jobs that:  
   - **Deduplicated** events using `dropDuplicates(['event_id'])` with a window to keep the latest version of any re-sent event  
   - **Parsed nested JSON** in the `raw_payload` column using `from_json(col('raw_payload'), schema)` — Spark can deserialize JSON into typed structs in one pass  
   - **Applied schema enforcement** using a predefined `StructType` schema — any column type mismatch surfaces as an error before bad data proceeds

4. **Unity Catalog for lineage**:  
   Unity Catalog is Databricks' unified governance layer. Every table I created was registered in the catalog with its owner, tags, and full **column-level lineage** — so you can click any column in any Gold table and trace exactly which raw source column it came from, through every transformation step. This is critical for compliance: when an auditor asks "where did this field come from?", you have a visual proof.

**Result**  
50M+ daily events processed reliably across the three layers. Schema violations caught at the Silver layer before they could corrupt Gold analytics. Lineage tracking satisfied the security compliance team's audit requirements. The architecture became the pattern every subsequent client deployment at Epik followed.

---

### 🔬 Technical Concept Breakdown

| Term | What It Is | Why It Matters |
|------|-----------|----------------|
| **Medallion Architecture** | Bronze (raw) → Silver (clean) → Gold (business-ready) data organization pattern. | Gives you raw replay ability AND clean analytics in one system. Industry standard for lakehouses. |
| **Delta Live Tables (DLT)** | Databricks' declarative pipeline framework. Define tables as functions; DLT handles orchestration, recovery, quality checks. | Less operational overhead than writing Spark jobs + Airflow DAGs. Built-in quality constraints. |
| **Delta Lake** | Open-source storage layer adding ACID transactions and a transaction log to Parquet files. | Makes cloud storage (ADLS/S3) reliable like a database. Enables upserts, deletes, time travel. |
| **ADLS Gen2** | Azure Data Lake Storage Gen2 — Microsoft's cloud object storage optimized for analytics. Hierarchical namespace + RBAC. | The storage backbone for Azure-based data platforms. Cheaper than databases, infinitely scalable. |
| **PySpark** | Python API for Apache Spark — distributed data processing across a cluster. | Process data too large for a single machine. Parallelized across many cores/nodes automatically. |
| **Unity Catalog** | Databricks' centralized governance layer: tables, schemas, access policies, column-level lineage in one place. | Fine-grained access control + automatic data lineage across all Databricks workspaces. |
| **Column-Level Lineage** | Ability to trace any column in any table back to its original source column through all transformation steps. | Compliance & debugging superpower. "Where did this number come from?" answered visually. |
| **Schema Enforcement** | Rejecting writes that don't match the expected table schema (column names, types). | Prevents silent schema drift from breaking downstream pipelines. The first line of data quality defense. |
| **DLT `@dlt.expect_or_drop`** | A data quality annotation: rows failing the condition are dropped (or quarantine/fail depending on severity). | Inline data quality without writing separate validation code. Results tracked in DLT Event Log. |

---

### 💬 How to Say It in the Interview

*"At Epik we were ingesting 50 million security events a day and the original setup was just raw files dumped into blob storage — no structure, no quality guarantees. I designed the full medallion architecture: Bronze for raw append-only storage, Silver for cleaned and schema-enforced data, Gold for analytics-ready tables. I implemented it using Delta Live Tables, which is Databricks' declarative pipeline framework — you define each table as a Python function, annotate data quality expectations inline, and DLT handles dependency resolution, failure recovery, and monitoring automatically. Everything was registered in Unity Catalog so we had column-level lineage from Gold all the way back to the raw source — that's what the security compliance team needed for their audit trail."*

---

### ❓ Likely Follow-up Questions

- *"What's the difference between Delta Lake and a regular data lake?"*  
  → A regular data lake is just files on object storage — no transactions, no ACID, no history. Delta Lake adds a transaction log (`_delta_log`) that records every operation. This enables ACID guarantees (writes are atomic), time travel (query old versions with `VERSION AS OF`), and schema enforcement. Without Delta, your data lake becomes a data swamp over time.

- *"Why use DLT instead of regular Spark jobs with Airflow?"*  
  → Regular Spark + Airflow requires you to write the orchestration, failure handling, and quality check logic yourself. DLT gives you auto-retry on partial failures, built-in quality constraint tracking with row-level metrics, and a visual pipeline graph with no extra code. The tradeoff is DLT is more opinionated — it works best for the medallion pattern.

- *"What is Unity Catalog and how does it differ from the legacy Hive Metastore?"*  
  → The Hive Metastore in Databricks was workspace-scoped — each workspace had its own catalog with no cross-workspace visibility. Unity Catalog is account-level — one governance layer for all workspaces. It also adds column-level security (masking policies), row-level security, and automated data lineage that the Hive Metastore never had.

---

## Bullet 2 — Snowflake + dbt for Enterprise Security Analytics

> *"Built Snowflake data warehouse models with dbt for enterprise security analytics, applying incremental materializations, clustering keys, and Snowpipe auto-ingest to reduce query latency by 45% downstream."*

---

### STAR Story

**Situation**  
After the medallion lakehouse was built in Databricks, the Gold layer data needed to flow into Snowflake — the warehouse that downstream BI tools and analysts queried directly. Security analysts needed to run queries like "show me all high-severity alerts from the last 30 days grouped by tenant and threat type." Without proper modeling these queries scanned hundreds of millions of rows and took 3+ minutes. Unusable in a live SOC environment.

**Task**  
Build the Snowflake transformation layer using dbt — turning the raw-ish data from Databricks into clean, optimized, analyst-friendly models. Reduce query latency to under 10 seconds for standard analyst queries.

**Action — Step by step**

1. **What dbt is (and what it is not)**:  
   dbt (data build tool) is a transformation framework. It does NOT extract or load data — it only transforms data that's already in your warehouse. You write SQL `SELECT` statements, dbt wraps them in `CREATE TABLE AS` or `CREATE VIEW AS` statements, and runs them in the right dependency order. The magic is: dbt makes SQL a proper software engineering artifact — with version control, tests, documentation, and lineage.

2. **dbt model layers**:  
   I organized the dbt project into three layers mirroring the medallion architecture:  
   - **Staging models** (`stg_*`): One-to-one with source tables. Just renaming columns, casting types, filtering out test data. No business logic. Materialized as **views** (no storage cost, always fresh).  
   - **Intermediate models** (`int_*`): Joining staging tables together, applying business logic (e.g., enriching alerts with tenant metadata). Materialized as **ephemeral** models (CTEs, not stored) or **tables** for heavy joins.  
   - **Mart models** (`mart_*`): The final analytics-ready tables. Fact and dimension tables following star schema. Materialized as **incremental tables**.

3. **Incremental materialization** — this is where the 45% latency reduction came from:  
   For the `mart_security_alerts` table (the main fact table), I used dbt's `materialized = 'incremental'` with an `is_incremental()` filter:  
   ```sql
   {{ config(materialized='incremental', unique_key='alert_id') }}
   SELECT * FROM {{ ref('int_alerts_enriched') }}
   {% if is_incremental() %}
     WHERE event_time > (SELECT MAX(event_time) FROM {{ this }})
   {% endif %}
   ```  
   On the first run: full table build. On every subsequent run: only processes rows newer than the latest record already in the table. This turned a 20-minute full refresh into a 90-second incremental run.

4. **Clustering keys**:  
   Snowflake's query optimizer benefits enormously from clustering keys on high-cardinality filter columns. I added `cluster_by = ['event_date', 'tenant_id']` on the main fact table. Snowflake reorganizes micro-partitions so queries filtering on those columns scan a tiny fraction of the data. 90% of analyst queries filter on date range + tenant — this single change cut scan volume drastically.

5. **Snowpipe auto-ingest**:  
   Data from Databricks landed in ADLS Gen2 as Parquet files. Instead of running a scheduled COPY INTO job every hour, I configured **Snowpipe** — Snowflake's continuous micro-batch ingestion. An Azure Event Grid notification triggers Snowpipe whenever a new file lands in the storage path. Snowpipe loads it within 1-2 minutes automatically, with no scheduled job to maintain.

6. **dbt tests**:  
   Every model had automated tests defined in `schema.yml`:  
   - `not_null` on primary key columns  
   - `unique` on `alert_id`  
   - `accepted_values` on `severity` column: `[low, medium, high, critical]`  
   - `relationships` — every `tenant_id` in the fact table must exist in `dim_tenant`  
   These run as part of CI/CD — a PR that breaks a test doesn't get merged.

**Result**  
Query latency on standard analyst queries dropped 45%. Incremental runs cut transform time from 20 minutes to 90 seconds. Snowpipe meant data was in Snowflake within 2 minutes of landing in storage. Analysts went from "I'll get you that report tomorrow" to "let me pull it up right now."

---

### 🔬 Technical Concept Breakdown

| Term | What It Is | Why It Matters |
|------|-----------|----------------|
| **dbt (data build tool)** | SQL-based transformation framework. Write SELECT statements; dbt handles building, testing, and documentation. | Brings software engineering practices (tests, version control, docs, lineage) to SQL transformations. |
| **dbt Materialization** | How dbt persists a model: view (no storage), table (full rebuild every run), incremental (only new rows), ephemeral (CTE). | Choosing the right materialization is 90% of dbt performance tuning. |
| **Incremental Materialization** | On the first run, build the full table. On subsequent runs, only process rows newer than the current max. | Turns a 20-minute full rebuild into a 2-minute delta load. Essential for large fact tables. |
| **`is_incremental()` block** | dbt Jinja macro that evaluates to `true` only on non-full-refresh runs. Used to add a WHERE filter. | Tells dbt "when I'm doing an incremental run, only look at new data." |
| **Snowflake Clustering Key** | Metadata that physically co-locates micro-partitions with the same key values. Equivalent to partitioning. | Drastically reduces scan volume for queries filtering on the cluster key. Best on date + high-cardinality dimension. |
| **Micro-partition** | Snowflake's internal storage unit: 50–500MB of compressed, columnar data. | Snowflake's query optimizer skips micro-partitions whose min/max range doesn't overlap the query filter. |
| **Snowpipe** | Snowflake's continuous micro-batch ingestion. Triggers on new file arrival via cloud storage notifications. | Near-real-time data availability without polling or scheduled COPY INTO jobs. 1-2 minute SLA. |
| **dbt `schema.yml` tests** | Data quality tests defined declaratively in YAML: `not_null`, `unique`, `accepted_values`, `relationships`. | Automated data contract enforcement. Run in CI/CD to prevent breaking changes from merging. |
| **Staging / Intermediate / Mart** | dbt layer convention: staging = raw source cleanup, intermediate = business logic joins, mart = analytics-ready final tables. | Separation of concerns. Easier debugging, reuse, and onboarding for new engineers. |

---

### 💬 How to Say It in the Interview

*"Snowflake was the analyst-facing warehouse — everything Databricks produced flowed there. I built the transformation layer in dbt, organized into staging, intermediate, and mart layers. The biggest win was incremental materialization on the main alerts fact table — instead of rebuilding 200 million rows every run, I added an is_incremental block that only processes rows newer than the current max event time. That took transform time from 20 minutes to 90 seconds. For query performance I added clustering keys on event_date and tenant_id, which is Snowflake's way of co-locating micro-partitions — queries filtering on those columns went from scanning the whole table to scanning maybe 5% of it. Data freshness I solved with Snowpipe: files landing in ADLS triggered automatic micro-batch loads in under 2 minutes, so analysts were always querying data that was at most 2 minutes old."*

---

### ❓ Likely Follow-up Questions

- *"What's the difference between dbt Core and dbt Cloud?"*  
  → dbt Core is the open-source CLI tool — free, runs anywhere, no UI. dbt Cloud is the hosted version — adds a scheduler, a web IDE, CI/CD integration, observability dashboards, and the dbt Explorer for visual lineage. We used dbt Core with Azure DevOps for CI/CD.

- *"How does dbt handle slowly changing dimensions?"*  
  → dbt has a `snapshot` feature — it tracks row-level history using a `dbt snapshot` command with a `strategy` (timestamp or check). It adds `dbt_valid_from` and `dbt_valid_to` columns to create a Type 2 SCD automatically.

- *"What is Elementary and how does it relate to dbt testing?"*  
  → Elementary is a dbt package that stores dbt test results as data in your warehouse over time. Instead of just pass/fail on each run, you get historical trending — "this column's null rate was 0.1% last week and is 3% today." It adds observability to dbt tests. Acuity KP specifically listed it — it sits on top of your existing dbt tests and adds time-series tracking and alerting.

---

## Bullet 3 — Azure Event Hubs + Databricks Structured Streaming

> *"Designed Azure Event Hubs streaming ingestion pipelines feeding Databricks Structured Streaming jobs into Delta Lake, achieving sub-5-minute data freshness SLA for real-time security alerting workflows."*

---

### STAR Story

**Situation**  
Some security events couldn't wait for a batch pipeline. A lateral movement attack — where a compromised account accesses multiple systems in sequence — might complete in under 10 minutes. If your data pipeline had a 1-hour batch window, the detection would always come too late. The security alerting team needed event data available for their detection rules within 5 minutes of the event occurring.

**Task**  
Design a streaming ingestion pipeline that continuously moved security events from source systems into Delta Lake with a guaranteed sub-5-minute freshness SLA.

**Action — Step by step**

1. **Azure Event Hubs**:  
   Event Hubs is Azure's managed message streaming service — think of it as Azure's equivalent of Apache Kafka. Source systems (endpoint agents, cloud audit log forwarders, network taps) published events as JSON messages to Event Hubs topics called **namespaces/event hubs**. Event Hubs retains messages for up to 7 days, so if the Databricks consumer falls behind or crashes, it can replay from its last position.  
   
   Key Event Hubs concepts:  
   - **Partitions**: Each event hub is split into N partitions for parallelism. Messages with the same partition key go to the same partition (preserving per-source ordering).  
   - **Consumer Groups**: Each reader (Databricks in this case) has its own consumer group with independent offset tracking.  
   - **Capture**: Event Hubs can auto-archive messages to ADLS Gen2 as Avro files — this gave us the Bronze layer for free.

2. **Databricks Structured Streaming**:  
   Structured Streaming is Spark's streaming execution engine. Unlike micro-batch systems, it models a data stream as an **unbounded DataFrame** — you write the same transformation code as for batch, and Spark handles the continuous processing.  
   
   My streaming job:  
   ```python
   df = (spark.readStream
     .format("eventhubs")
     .options(**ehConf)
     .load())
   
   parsed = df.select(
     from_json(col("body").cast("string"), event_schema).alias("data"),
     col("enqueuedTime").alias("ingestion_time")
   ).select("data.*", "ingestion_time")
   
   query = (parsed.writeStream
     .format("delta")
     .option("checkpointLocation", checkpoint_path)
     .trigger(processingTime="30 seconds")
     .toTable("silver.security_events"))
   ```  
   The `.trigger(processingTime="30 seconds")` means: process whatever arrived in the last 30 seconds every 30 seconds. This gives ~1-minute end-to-end latency from event emission to Delta table availability.

3. **Checkpointing**:  
   The `checkpointLocation` is a folder in ADLS Gen2 where Spark persists the stream's progress — which Event Hubs offsets have been processed. If the streaming job crashes and restarts, it resumes exactly from where it left off. No data lost, no duplicates.

4. **Exactly-once semantics with Delta Lake**:  
   Delta Lake + Structured Streaming together provide **exactly-once processing** — each event is written to Delta exactly once, even if a job fails midway and is restarted. This is because Delta's transaction log records which offsets were committed, and Structured Streaming checks this before writing.

5. **Meeting the 5-minute SLA**:  
   - Event emitted by source → Event Hubs: ~1-5 seconds  
   - Event Hubs → Databricks trigger: 30-second trigger interval  
   - Databricks transformation + Delta write: ~20-30 seconds  
   - Total: well under 2 minutes in normal operation. SLA of 5 minutes was met with 3x headroom.

**Result**  
Sub-5-minute data freshness SLA achieved and maintained. Security alerting rules that previously ran on 1-hour-old data now ran on data that was 1-2 minutes old. Lateral movement detection accuracy improved significantly because correlated events arrived in the same analysis window.

---

### 🔬 Technical Concept Breakdown

| Term | What It Is | Why It Matters |
|------|-----------|----------------|
| **Azure Event Hubs** | Azure's managed event streaming service. Compatible with Apache Kafka protocol. | Decouples event producers from consumers. Durable, scalable, 7-day retention for replay. |
| **Event Hubs Partition** | An ordered log within an event hub. Messages with the same partition key are ordered within a partition. | More partitions = more parallel consumers. Per-key ordering guaranteed within a partition. |
| **Consumer Group** | An independent view into an event hub. Each consumer group tracks its own offset. | Multiple downstream systems can read the same event hub independently at their own pace. |
| **Databricks Structured Streaming** | Spark's streaming engine. Treats a stream as an unbounded DataFrame. Write batch-style code; runs continuously. | Same API as batch Spark. Simplifies code — no separate streaming framework to learn. |
| **`.trigger(processingTime=...)`** | How often Spark wakes up to process accumulated messages. 30s = micro-batch every 30 seconds. | Controls latency vs throughput tradeoff. Shorter = lower latency, higher overhead. |
| **Checkpoint Location** | A folder in cloud storage where Spark writes stream progress (last committed offset). | Enables fault-tolerant, exactly-once restarts. If job crashes, it resumes from last checkpoint. |
| **Exactly-once Semantics** | Each message is processed and written to the output exactly once, even on failure + restart. | Data integrity guarantee. Without it, retries cause duplicates or missed records. |
| **Event Hubs Capture** | Event Hubs' built-in auto-archival to ADLS Gen2 as Avro files at configurable intervals. | Free Bronze layer. Raw event archive without any pipeline code. |
| **`from_json()`** | Spark SQL function to parse a JSON string column into a typed struct using a provided schema. | Needed because Event Hubs delivers message body as bytes — you deserialize it in Spark. |

---

### 💬 How to Say It in the Interview

*"For real-time security alerting we needed data in Delta Lake within 5 minutes of an event happening — batch pipelines couldn't satisfy that. I built the streaming layer using Azure Event Hubs as the ingestion buffer — source agents pushed events there — and Databricks Structured Streaming as the consumer. The streaming job read from Event Hubs, parsed the JSON body, transformed it to the Silver schema, and wrote to Delta with a 30-second trigger. The checkpoint location in ADLS ensured exactly-once delivery — if the job crashed and restarted, no duplicates, no gaps. End-to-end latency was consistently under 2 minutes, well within the 5-minute SLA. I also turned on Event Hubs Capture to get a free Bronze archive — Avro files in ADLS automatically, zero code."*

---

### ❓ Likely Follow-up Questions

- *"How does Structured Streaming handle late-arriving data?"*  
  → Spark has a `withWatermark()` API: `df.withWatermark("event_time", "10 minutes")` tells Spark to wait up to 10 minutes for late events before finalizing a window. Events arriving after the watermark are dropped. Without watermarking, Spark holds state indefinitely for all possible late events — memory leak.

- *"Event Hubs vs Kafka — when would you use one vs the other?"*  
  → Event Hubs is fully managed on Azure with zero operational overhead — no cluster to run. Kafka gives you more control: custom configurations, more connector ecosystem, works outside Azure. Event Hubs actually implements the Kafka protocol, so you can use Kafka clients against Event Hubs. If you're all-in on Azure and don't need Kafka-specific features, Event Hubs is simpler to operate.

---

## Bullet 4 — Azure Infrastructure + Terraform + Azure DevOps CI/CD

> *"Provisioned end-to-end data infrastructure on Azure (ADLS Gen2, Databricks, Event Hubs, Key Vault) using Terraform IaC, reducing environment setup time from days to under 2 hours via Azure DevOps CI/CD."*

---

### STAR Story

**Situation**  
Every new client onboarding at Epik required a new isolated Azure environment — a separate Databricks workspace, ADLS storage accounts, Event Hubs namespace, and Key Vault. The original process involved manually clicking through the Azure Portal, which took 2-3 days of DevOps time, was error-prone (someone always forgot a firewall rule), and produced environments that were slightly different from each other in ways that caused subtle bugs.

**Task**  
Eliminate manual infrastructure provisioning. Codify the entire environment in Terraform so a new client environment could be stood up in under 2 hours with a single pipeline run.

**Action — Step by step**

1. **What Terraform is**:  
   Terraform is Infrastructure as Code — you describe your desired infrastructure in `.tf` files (HCL language), run `terraform plan` to see what will change, then `terraform apply` to make it happen. Terraform talks to Azure (and every other cloud) via **providers**. The key insight: infrastructure becomes code — version-controllable, reviewable, testable, reproducible.

2. **What I provisioned in Terraform**:  
   - **ADLS Gen2** storage account with hierarchical namespace, Bronze/Silver/Gold containers, and lifecycle management policies (auto-archive files older than 90 days to cool tier)  
   - **Azure Databricks** workspace with Unity Catalog enabled, cluster policies, and auto-scaling compute configurations  
   - **Azure Event Hubs** namespace with client-specific event hubs, consumer groups, and Capture to ADLS enabled  
   - **Azure Key Vault** for all secrets (storage access keys, API credentials, Snowflake passwords) — nothing stored in code or config files  
   - **Azure AD** service principal with minimum required RBAC roles (not Owner — exactly what was needed)

3. **Azure Key Vault for secrets management**:  
   No secret ever touches code or a config file. All credentials are stored in Key Vault and retrieved at runtime:  
   - Databricks jobs retrieve secrets via `dbutils.secrets.get(scope='kv-scope', key='snowflake-password')`  
   - Python pipelines use the Azure SDK: `SecretClient(vault_url, DefaultAzureCredential()).get_secret("snowflake-password").value`  
   - Key Vault itself is provisioned and configured by Terraform including access policies

4. **Azure DevOps CI/CD pipeline**:  
   I built a two-stage Azure Pipeline:  
   - **PR stage**: `terraform validate` + `terraform plan` — the plan output is posted as a PR comment so reviewers can see exactly what infrastructure will change  
   - **Merge to main**: `terraform apply -auto-approve` — deploys the change to the target environment  
   - **Environment isolation**: separate Terraform state files per environment (dev/staging/prod) stored in Azure Blob backend with state locking  

5. **State management**:  
   Terraform tracks what it has deployed in a **state file** — a JSON file mapping Terraform resources to real Azure resource IDs. I stored state in Azure Blob Storage with state locking via a lease mechanism — prevents two pipeline runs from applying simultaneously and corrupting state.

**Result**  
New client environment setup: 2 hours end-to-end (pipeline run time). Previously: 2-3 days of manual work. Zero configuration drift between environments — dev, staging, and prod were identical because they all deployed from the same Terraform code.

---

### 🔬 Technical Concept Breakdown

| Term | What It Is | Why It Matters |
|------|-----------|----------------|
| **Terraform** | Open-source Infrastructure as Code tool. Declares desired infrastructure state in HCL; applies it against cloud APIs. | Reproducible, version-controlled infrastructure. The industry standard for cloud IaC. |
| **HCL (HashiCorp Config Language)** | Terraform's declarative configuration language. | Human-readable syntax for defining resources: `resource "azurerm_storage_account" "bronze" { ... }`. |
| **`terraform plan`** | Dry-run: shows exactly what Terraform will create, modify, or destroy before applying. | Safety check. Review the plan before touching real infrastructure. |
| **Terraform State** | A JSON file mapping Terraform config to real cloud resources. Terraform reads it to know what's deployed. | Without state, Terraform can't know what already exists. Stored remotely for team collaboration. |
| **Remote State Backend** | Storing Terraform state in Azure Blob / S3 / GCS instead of locally. | Enables team collaboration. Prevents "works on my machine" with different local states. |
| **State Locking** | Preventing concurrent Terraform applies via a lease/lock on the remote state. | Without locking, two simultaneous `apply` runs corrupt the state file. |
| **Azure Key Vault** | Azure's secrets management service. Store, rotate, and audit access to secrets, certificates, and keys. | Never hardcode credentials. Key Vault is the Azure equivalent of AWS Secrets Manager. |
| **RBAC (Azure)** | Role-Based Access Control on Azure resources. Built-in roles: Owner, Contributor, Reader, plus custom roles. | Least-privilege access. Service principals get only the IAM permissions they actually need. |
| **Azure DevOps Pipelines** | Microsoft's CI/CD platform. YAML-defined pipelines for build, test, and deploy workflows. | Automates `terraform apply` on merge, gates deployment behind PR review. |
| **Service Principal** | An Azure AD identity for applications/pipelines (not humans). Used for automated authentication. | Pipelines authenticate as a service principal, not as a human account. Auditable, revocable. |

---

### 💬 How to Say It in the Interview

*"Manual infrastructure provisioning at Epik took 2-3 days per new client — Azure Portal clicking, always slightly inconsistent between environments. I codified the entire stack in Terraform: ADLS storage accounts with lifecycle policies, Databricks workspace with Unity Catalog, Event Hubs, Key Vault — all of it. Every secret went into Key Vault at provision time; code retrieves secrets at runtime via the Azure SDK, nothing is ever in a config file. The Azure DevOps pipeline runs terraform plan on every PR so reviewers see the exact infrastructure diff before merging, then terraform apply on merge to main. New client environment: under 2 hours. Dev, staging, and prod are identical because they all deploy from the same Terraform code — no more 'it works in dev but not prod' mystery."*

---

### ❓ Likely Follow-up Questions

- *"How do you manage secrets in a data pipeline — what's wrong with environment variables?"*  
  → Environment variables are better than hardcoded strings, but they're still plaintext in memory, visible in process listings, and hard to rotate across many machines. Key Vault (or AWS Secrets Manager) adds: encryption at rest and in transit, fine-grained access policies (which service principal can read which secret), automatic rotation, and audit logs of every access. Databricks secret scopes backed by Key Vault integrate seamlessly.

- *"What's the difference between Terraform and Azure ARM templates / Bicep?"*  
  → ARM templates and Bicep are Azure-native — they only work with Azure. Terraform is cloud-agnostic — same workflow for Azure, AWS, GCP. If your infrastructure spans multiple clouds or you want to avoid vendor lock-in on your IaC tooling, Terraform wins. Bicep is more ergonomic than ARM JSON but still Azure-only.

---

## Bullet 5 — Dagster Orchestration + Great Expectations Data Quality

> *"Implemented Dagster-orchestrated pipeline monitoring with Great Expectations (GX) data quality checks across all medallion layers, catching schema drift and anomalies before they reached production analytics layers."*

---

### STAR Story

**Situation**  
We had a running medallion pipeline and streaming ingestion, but no systematic way to know if the data moving through those layers was actually good. Data quality issues were discovered reactively — an analyst would notice a weird number in a dashboard, trace it back, and find that a source system changed a field format three days ago. By then, three days of Gold data was corrupted.

**Task**  
Build proactive, automated data quality monitoring that caught issues at each layer boundary before they propagated downstream. Orchestrate the quality checks in a way that pipelines automatically paused on failure rather than silently continuing with bad data.

**Action — Step by step**

1. **Why Dagster (not Airflow)**:  
   Airflow models workflows as **task DAGs** — the unit is a task (a unit of work). Dagster models workflows as **software-defined assets** — the unit is a data asset (a table, a file, a model). This distinction matters:  
   - In Airflow: "run task X at 2 AM"  
   - In Dagster: "materialize the `silver_security_events` asset, which depends on `bronze_raw_events` and `dim_threat_intel`"  
   
   Dagster shows you the **asset graph** — a visual map of all your data assets and their dependencies. When an asset fails, Dagster highlights exactly which downstream assets are now stale. It also integrates natively with dbt — you can see your dbt models AS assets in the same graph as your Python pipelines.

2. **Dagster asset definitions**:  
   Each data layer (Bronze, Silver, Gold, dbt models) was defined as a Dagster `@asset`:  
   ```python
   @asset(
     group_name="silver",
     freshness_policy=FreshnessPolicy(maximum_lag_minutes=10)
   )
   def silver_security_events(bronze_raw_events):
       # transformation logic
       return transformed_df
   ```  
   The `freshness_policy` tells Dagster: if this asset hasn't been materialized in the last 10 minutes, flag it as stale on the dashboard. Monitors alert on staleness.

3. **Great Expectations (GX) integration**:  
   Great Expectations is a Python data quality framework. You define **Expectations** — assertions about your data:  
   - `expect_column_to_not_be_null("event_id")`  
   - `expect_column_values_to_be_between("severity_score", 0, 100)`  
   - `expect_table_row_count_to_be_between(min_value=10000, max_value=5000000)` — if row count drops below 10K something upstream broke  
   - `expect_column_values_to_match_regex("src_ip", r"^\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}$")`  
   
   I organized expectations into **Expectation Suites** per layer — a Bronze suite (minimal: schema and completeness), a Silver suite (stricter: type correctness, value ranges, referential integrity), a Gold suite (business rules: no negative revenue, valid tenant IDs only).

4. **Dagster + GX integration**:  
   Used the `dagster-ge` integration library. Each Dagster asset had a GX validation step as an `AssetObservation` — it ran the expectation suite against the asset output and reported results back to Dagster's event log. If expectations failed, the asset was marked as failed in the asset graph, and Dagster blocked downstream asset materializations automatically.

5. **Schema drift detection**:  
   One of the most valuable GX expectations: `expect_table_columns_to_match_ordered_list(columns)`. If a source system added, removed, or renamed a column, this expectation failed immediately at the Bronze → Silver transition, before any transformation logic tried to reference the missing column and caused a cryptic KeyError 3 layers deep.

**Result**  
Schema drift and data quality issues caught at the Bronze/Silver boundary, not in production dashboards. Mean time to detection for data quality issues dropped from "analyst notices something wrong 2 days later" to "Dagster alert fires within 10 minutes of the first bad batch."

---

### 🔬 Technical Concept Breakdown

| Term | What It Is | Why It Matters |
|------|-----------|----------------|
| **Dagster** | Asset-centric data orchestration platform. Builds, schedules, and monitors software-defined data assets. | Models your pipeline as a graph of data assets with dependencies, lineage, and freshness policies. |
| **Software-Defined Asset (SDA)** | A Dagster `@asset` — a Python function that produces a persistent data artifact (table, file, model). | The fundamental unit in Dagster. Replaces Airflow's task abstraction with a data-centric one. |
| **Asset Graph** | Dagster's visual map of all assets and their upstream/downstream dependencies. | At a glance: what's healthy, what's stale, what's broken, and what's affected downstream. |
| **Dagster `FreshnessPolicy`** | Policy on an asset declaring the maximum acceptable staleness (e.g., materialized within last 10 minutes). | Proactive staleness monitoring. Alert before an analyst notices stale data in a dashboard. |
| **Great Expectations (GX)** | Python framework for defining, documenting, and validating data quality expectations. | `expect_column_to_not_be_null`, `expect_values_to_be_between`, etc. Assertion-based quality checks. |
| **Expectation Suite** | A named collection of GX expectations for a specific dataset/layer. | Group related checks together. Bronze suite = basic checks; Gold suite = strict business rule checks. |
| **Validation Result** | GX's output after running an expectation suite: pass/fail per expectation + row-level details on failures. | The evidence of data quality. Stored for historical trending and audit. |
| **Schema Drift** | When a source system changes its schema (adds/removes/renames columns) without notifying downstream consumers. | One of the top causes of silent pipeline failures. Early detection is everything. |
| **Elementary** | dbt package that stores dbt test results over time in your warehouse. Adds anomaly detection and alerting on top. | Acuity KP's listed tool. Extends dbt tests with time-series trending — "null rate went from 0.1% to 3%." |
| **Dagster + dbt integration** | Dagster can import a dbt project and represent all dbt models as Dagster assets. | One unified asset graph showing both Python pipeline assets and dbt SQL model assets together. |

---

### 💬 How to Say It in the Interview

*"We were discovering data quality issues reactively — an analyst would notice something wrong in a dashboard two days after the source system had silently changed a field format. I fixed that with Dagster and Great Expectations. Dagster is asset-centric — instead of thinking about tasks, you think about data assets and their dependencies. Every layer in the medallion architecture was a Dagster asset with a freshness policy. I attached Great Expectations validation suites to each asset — Bronze suite checked schema and completeness, Silver suite added type correctness and value ranges, Gold suite added business rules. Dagster blocked downstream materializations automatically when GX expectations failed. Schema drift was caught at the Bronze-Silver boundary within 10 minutes of the first bad batch instead of days later."*

---

### ❓ Likely Follow-up Questions

- *"Dagster vs Airflow — which would you recommend for a new project?"*  
  → Dagster for greenfield. The asset-centric model is a better mental model for data engineering — you reason about your data, not your tasks. Dagster's integration with dbt is first-class, the UI shows you what data is fresh vs stale, and it has better software engineering ergonomics (testability, type hints, resource injection). Airflow has a larger ecosystem and more operational familiarity but the task DAG abstraction doesn't naturally model data lineage.

- *"What is Elementary and how does it complement Great Expectations?"*  
  → Great Expectations is a validation framework — you assert things about data and get pass/fail. Elementary is a dbt observability tool — it stores dbt test results as data in your warehouse over time and adds anomaly detection on top (e.g., if column null rate doubles vs its 7-day average, alert). GX is better for rich, custom validations. Elementary is better for trend-based anomaly detection on top of your existing dbt tests. They're complementary.

---

## Bullet 6 — Team Tech Leadership, dbt Style Guides, Delta Partitioning Standards

> *"Led data modeling reviews and pipeline design sessions across a 5-engineer team, establishing dbt style guides and Delta Lake partitioning standards adopted as team-wide conventions."*

---

### STAR Story

**Situation**  
As the team at Epik grew to 5 engineers, each one had slightly different dbt conventions — some named staging models `stg_`, others `stage_`, some used incremental materialization everywhere, others used tables everywhere regardless of size. Delta tables had inconsistent partitioning: one engineer partitioned by `event_date`, another by `year_month`, another didn't partition at all. This inconsistency made code reviews slow, made debugging painful ("which convention does this repo use?"), and made it hard for new engineers to onboard.

**Task**  
Establish team-wide conventions for dbt project structure and Delta Lake partitioning, and run design review sessions that prevented bad patterns from reaching main before they became technical debt.

**Action — Step by step**

1. **dbt Style Guide** (what I documented and enforced):  
   - **Naming**: `stg_<source>__<entity>` (double underscore separates source from entity), `int_<verb>_<entity>`, `mart_<domain>__<entity>`. Example: `stg_eventhubs__security_events`, `int_enrich_alerts`, `mart_security__alert_summary`  
   - **Materialization rules**: Views for staging (cheap, always fresh), incremental for large fact tables (>10M rows), table for dimension tables and intermediates (small, frequently joined)  
   - **Test requirements**: Every staging model must have `not_null` + `unique` on primary key. Every fact table must have `relationships` tests on all foreign keys.  
   - **Documentation**: Every model must have a description in `schema.yml`. Every column that's not obviously named must have an inline description.  
   - **CTEs over subqueries**: All multi-step SQL written as a series of named CTEs, not nested subqueries. `final` CTE at the bottom is what gets selected.

2. **Delta Lake partitioning standards**:  
   - Partition **only on columns used in frequent WHERE filters**. Never partition on high-cardinality columns (e.g., user_id — creates millions of tiny files, the "small file problem").  
   - Standard: partition by `event_date` (date, not datetime) for time-series data. If query patterns also filter on `tenant_id`, add it as a secondary cluster key.  
   - **Z-Ordering**: For columns that aren't the partition key but are frequently filtered, use Databricks' `OPTIMIZE table ZORDER BY (column)` to physically co-locate related data within partitions.

3. **Design review process**:  
   I ran bi-weekly 30-minute "data design reviews" where any engineer working on a new pipeline or model would present their proposed approach before coding. The format: (1) what are the source tables, (2) what is the target schema, (3) what materialization strategy and why, (4) what data quality checks. This prevented significant rework — catching "you're using a table materialization on a 500M row model that rebuilds every 20 minutes" before it's already in production.

**Result**  
Code reviews became faster because reviewers could check against documented standards rather than debating conventions in every PR. Onboarding a new engineer went from "figure it out from existing code" to "read the style guide, then read two existing models as examples." Delta partitioning inconsistencies were eliminated across the codebase.

---

### 🔬 Technical Concept Breakdown

| Term | What It Is | Why It Matters |
|------|-----------|----------------|
| **Small File Problem** | When Delta/Parquet tables accumulate thousands of tiny files, query performance degrades due to per-file overhead. | Over-partitioning (partitioning on high-cardinality columns) creates millions of files. `OPTIMIZE` compacts them. |
| **Delta `OPTIMIZE`** | Databricks command that compacts small Delta files into larger, more efficient ones. | Fixes small file problem. Run periodically on high-write tables. |
| **Z-Ordering** | Delta Lake feature: `OPTIMIZE table ZORDER BY (col)` co-locates rows with similar values in the same files. | For columns frequently filtered that aren't the partition key. Multi-dimensional data skipping. |
| **dbt Naming Conventions** | `stg_` for staging, `int_` for intermediate, `mart_` for final analytics models. | Consistent naming = instant context. You know the purpose and layer of any model from its name. |
| **CTE Pattern** | Write SQL as a series of named `WITH` blocks, final `SELECT` at the bottom from a `final` CTE. | Readability. Debugging. Each step is independently inspectable. No nested subquery hell. |
| **Tech Lead Role** | Setting technical standards, conducting design reviews, unblocking team members on architecture decisions. | Beyond individual contribution — scaling your knowledge across the team through documentation and process. |

---

---

# SAMAY SYSTEMS LLC — Data Engineer (Jul 2022 – Jun 2025)
### *Financial Compliance SaaS Platform*

---

## Bullet 7 — Azure Data Factory ELT Pipelines (10+ Sources, Multi-Tenant)

> *"Built Azure Data Factory ELT pipelines ingesting structured and semi-structured data from 10+ REST APIs and flat-file sources into ADLS Gen2, processing 10K+ compliance records daily across 15+ enterprise tenants."*

---

### STAR Story

**Situation**  
Samay Systems built a compliance tracking SaaS platform for financial services firms. Each client (tenant) had their own data: compliance reports from regulatory APIs (FINRA, SEC feeds), transaction records from flat files dropped via SFTP, trade surveillance data from REST APIs, employee training records from HR systems. 15 clients, each with 4-6 data sources = 60+ individual data feeds that needed to flow into the platform daily.

**Task**  
Build the data ingestion layer that pulled from all these heterogeneous sources and landed the data in ADLS Gen2, with proper tenant isolation so one client's data never mixed with another's.

**Action — Step by step**

1. **What Azure Data Factory is**:  
   ADF is Azure's cloud ETL/ELT orchestration service. It has three core concepts:  
   - **Linked Services**: Connection configurations to data sources (REST APIs, SFTP servers, SQL Server, ADLS, Snowflake). Think of them as ODBC connection strings managed in the UI.  
   - **Datasets**: A named reference to a specific data location within a Linked Service (a specific SFTP path, a specific REST endpoint URL).  
   - **Pipelines**: The actual workflow — activities (Copy Data, Execute Script, Call REST API, etc.) connected with dependencies and control flow.

2. **Parameterized pipelines for multi-tenancy**:  
   Instead of building one pipeline per tenant (60+ pipelines), I built **parameterized pipeline templates** with parameters like `tenant_id`, `source_endpoint_url`, `target_adls_container`. A single "ingest_rest_api" pipeline template served all REST API sources across all tenants — you just pass different parameters. ADF's **ForEach** activity iterated over a JSON config of tenant-source configurations and spawned parallel pipeline runs.

3. **REST API ingestion with pagination**:  
   Most regulatory APIs returned paginated results (e.g., 1000 records per page). I built a pipeline with a **Until** loop activity that:  
   - Called the API with a page token  
   - Appended results to a staging file in ADLS  
   - Checked the response for a `next_page_token` field  
   - Looped until no more pages  
   
   This is the standard pagination pattern for REST APIs in ADF.

4. **SFTP flat-file ingestion**:  
   For clients that dropped CSV/Excel files on SFTP servers, ADF's **SFTP Linked Service** watched for new files using a **tumbling window trigger** (fires for every fixed-length time window, one run per window). Files were copied to ADLS Bronze with the tenant ID and ingestion timestamp embedded in the folder path: `bronze/tenant_{id}/year={y}/month={m}/day={d}/`.

5. **Tenant isolation**:  
   Every file landed in a tenant-specific ADLS container with Azure AD RBAC scoped to that container. No ADF pipeline for tenant A could read or write to tenant B's container — enforced at the storage layer, not just in application code.

**Result**  
60+ data feeds ingested daily across 15 enterprise tenants from a handful of parameterized ADF pipeline templates. Tenant isolation enforced at the storage RBAC layer. New tenant onboarding: add their config to the JSON parameter file, no new pipeline code needed.

---

### 🔬 Technical Concept Breakdown

| Term | What It Is | Why It Matters |
|------|-----------|----------------|
| **Azure Data Factory (ADF)** | Azure's managed ETL/ELT orchestration service. Build data pipelines visually or via JSON definition. | The Azure equivalent of AWS Glue or Apache NiFi. Good for cloud-to-cloud data movement. |
| **Linked Service** | ADF's connection configuration to a data source (credentials, endpoint, auth method). | The "connector" abstraction. Configure once, reuse across multiple datasets and pipelines. |
| **Parameterized Pipeline** | An ADF pipeline with parameter placeholders (`@pipeline().parameters.tenant_id`). | One template, many executions with different configs. Eliminates copy-paste pipelines. |
| **ForEach Activity** | ADF activity that iterates over an array and spawns parallel (or sequential) inner pipeline runs. | Drive multi-tenant or multi-source pipelines from a config array. |
| **Until Activity** | ADF activity that loops until a condition is true. Used for API pagination. | "Keep calling the API until there are no more pages." |
| **Tumbling Window Trigger** | ADF trigger that fires for every fixed-length time window (e.g., every hour), one run per window, no overlap. | Good for batch loads that need to process each time window exactly once. |
| **Multi-tenant Architecture** | A single platform instance serving multiple clients (tenants) with strict data isolation between them. | SaaS fundamental. Each tenant's data must be logically and physically isolated. |

---

## Bullet 8 — SQL Server → Snowflake Migration + Dagster Asset Pipelines

> *"Migrated on-premise SQL Server compliance warehouse to Snowflake, designing star-schema dimensional models and orchestrating historical loads via Dagster asset pipelines, reducing analyst query latency 60%."*

---

### STAR Story

**Situation**  
Samay's compliance warehouse lived on an on-premise SQL Server. As the client base grew to 15 tenants and data volume hit hundreds of millions of compliance records, SQL Server was struggling — queries took 10-15 minutes, indexes were ballooning, storage was a constant operational headache. The business decision was made to migrate to Snowflake. My job was to execute that migration without losing any historical data or breaking analyst workflows.

**Task**  
Design the Snowflake target schema, execute the historical data migration from SQL Server, and cut over live production traffic — all without downtime and without data loss.

**Action — Step by step**

1. **Schema redesign**:  
   SQL Server schema was a normalized OLTP design — 3rd Normal Form with many lookup tables and foreign key constraints. This is good for transactional writes but terrible for analytical queries (lots of joins). I redesigned it as a **Star Schema** for Snowflake:  
   - `fact_compliance_events`: One row per compliance event, all foreign keys to dimensions  
   - `dim_tenant`, `dim_regulation`, `dim_employee`, `dim_date`  
   - Deliberately denormalized — some redundancy is fine in a warehouse to avoid joins  
   
   This single change was responsible for most of the 60% latency improvement.

2. **Dagster asset pipelines for migration**:  
   I used Dagster's **software-defined assets** to model the migration in phases:  
   - Asset 1: `sql_server_extract_compliance_events` — exported data from SQL Server as Parquet to ADLS (in chunks, by date range, to avoid memory issues)  
   - Asset 2: `transform_to_snowflake_schema` — PySpark job that remapped old SQL Server columns to new star schema column names, resolved lookup table foreign keys to denormalized values  
   - Asset 3: `snowflake_historical_load` — used Snowflake's COPY INTO from ADLS staging  
   - Asset 4: `validate_migration_counts` — GX expectation: row counts in Snowflake must match SQL Server source within 0.01% tolerance  
   
   Each asset ran independently and could be re-run if it failed — idempotent writes (MERGE, not INSERT) ensured no duplicates on retry.

3. **Incremental cutover**:  
   Historical load (5 years of data) ran over a weekend. For the cutover, I ran SQL Server and Snowflake in parallel for 2 weeks — both pipelines populated simultaneously. Analysts tested their Snowflake queries against SQL Server baseline before cutting over. This is called a **parallel run** — reduces risk because you have a fallback.

4. **Dagster for ongoing orchestration**:  
   After migration, Dagster orchestrated the ongoing ELT — ADF loaded raw data to ADLS, Dagster assets materialized the star schema layers in Snowflake in the right order, with data quality checks gating each layer.

**Result**  
Zero data loss on migration (validated by count reconciliation). Analyst query latency dropped 60% — from 10-15 minutes on SQL Server to under 4 minutes on Snowflake star schema. Ongoing pipeline reliability improved because Dagster gave the team visibility into which assets were fresh vs stale.

---

### 🔬 Technical Concept Breakdown

| Term | What It Is | Why It Matters |
|------|-----------|----------------|
| **3NF (Third Normal Form)** | OLTP normalization: every non-key attribute depends only on the primary key. No redundancy. | Optimal for transactional writes. Terrible for analytics — requires many joins for simple aggregations. |
| **Star Schema** | Fact table + denormalized dimension tables. Optimized for analytical read queries. | Fewer joins, faster aggregation, simpler SQL. The Kimball methodology standard for data warehouses. |
| **Snowflake COPY INTO** | Bulk-load command: reads files from cloud storage and loads into a table in parallel. | Orders of magnitude faster than INSERT statements for large-scale data loads. |
| **Parallel Run** | Running old and new systems simultaneously during a migration, comparing outputs before cutting over. | The safest migration strategy. You can roll back if Snowflake produces different results. |
| **Count Reconciliation** | Asserting that row counts between source and destination match within an acceptable tolerance. | The most basic migration validation. If counts don't match, data was lost or duplicated. |
| **Idempotent Write** | A write operation that produces the same result no matter how many times you run it (no duplicates). | Critical for reliable pipelines. MERGE/upsert is idempotent; blind INSERT is not. |
| **Dagster Asset Pipeline** | A Dagster workflow where each step is a software-defined asset, run in dependency order. | Models the migration as data artifacts with lineage, not just a sequence of tasks. |

---

## Bullet 9 — PySpark ELT on Databricks (Replacing ADF Transformations)

> *"Adopted Azure Databricks and Delta Lake to replace brittle ADF transformation logic, building PySpark-based ELT jobs with idempotent writes, watermarking, and schema evolution handling across all compliance datasets."*

---

### STAR Story

**Situation**  
ADF's transformation capabilities (Data Flow activities) were initially used for the T in ELT — cleaning and transforming data after ingestion. Over time, these ADF Data Flows became increasingly complex, hard to test, and impossible to debug when they failed. ADF Data Flows are essentially a drag-and-drop GUI tool — they're fine for simple column renames, but not for complex conditional logic, multi-step business rule application, or anything requiring Python. We kept hitting the ceiling of what the GUI tool could do.

**Task**  
Move all complex transformation logic from ADF Data Flows into PySpark jobs on Databricks, making the transformations testable, version-controllable, and maintainable.

**Action — Step by step**

1. **Idempotent writes with Delta MERGE**:  
   The key requirement: if a job runs twice (failure + restart), no duplicate data. I implemented every write as a Delta `MERGE` (upsert):  
   ```python
   delta_table.alias("target").merge(
     source_df.alias("source"),
     "target.compliance_event_id = source.compliance_event_id"
   ).whenMatchedUpdateAll().whenNotMatchedInsertAll().execute()
   ```  
   This inserts new records and updates existing ones. Running the same job twice: second run updates the same rows to the same values. No new rows created. Idempotent.

2. **Watermarking for incremental loads**:  
   Instead of processing the full compliance dataset on every run, I tracked a **high watermark** (the maximum `event_timestamp` value of records already processed) in a `_pipeline_state` Delta table. Each job run:  
   - Read the current watermark  
   - Queried source only for records newer than the watermark  
   - Processed and wrote those records  
   - Updated the watermark to the new maximum  
   
   This is the **bookmark/watermark pattern** — fundamental to incremental ELT.

3. **Schema evolution handling**:  
   Source compliance data came from APIs that occasionally added new fields. In a traditional setup, a new source column would fail the write because the target schema didn't have it. I enabled Delta's **schema evolution** (`mergeSchema=True` option on write):  
   ```python
   df.write.format("delta").option("mergeSchema", "true").mode("append").save(path)
   ```  
   New columns in the source are automatically added to the Delta table schema. Existing columns are unchanged. No pipeline failure, no manual schema migration script needed.

4. **Testing PySpark transformations**:  
   Unlike ADF GUI flows, PySpark code is testable. I wrote unit tests using `pyspark.testing.assertDataFrameEqual` — created a small in-memory test DataFrame, ran the transformation function, asserted the output matched expected results. Tests ran in the Azure DevOps CI pipeline on every PR.

**Result**  
Complex ADF Data Flows retired. All transformation logic now lived in version-controlled PySpark files with unit tests. Schema changes from source APIs no longer caused pipeline failures. Debugging a failed job went from "open ADF Studio and click through 50 connected boxes" to "read the Python stack trace."

---

### 🔬 Technical Concept Breakdown

| Term | What It Is | Why It Matters |
|------|-----------|----------------|
| **Delta MERGE (Upsert)** | SQL/PySpark operation: insert if key doesn't exist, update if it does. | Idempotent writes. Run the same job twice, same result, no duplicates. |
| **Watermark / High Watermark** | A saved value (usually max timestamp or ID) marking the furthest-processed record. | Resume from where you left off. Don't reprocess the entire dataset on every run. |
| **`_pipeline_state` table** | A small Delta table tracking pipeline metadata (last run watermark, row counts, etc.). | Persistent state for incremental jobs. Survives job restarts. |
| **Schema Evolution** | Ability to automatically add new columns to a table when new source columns appear. | Prevents pipeline failures when upstream schemas change. Delta supports this natively. |
| **`mergeSchema=True`** | Delta write option that allows new source columns to be added to the target schema automatically. | Enable schema evolution for append/overwrite operations. |
| **ADF Data Flows** | ADF's visual ETL transformation tool. Drag-and-drop UI for column transformations. | Good for simple transformations. Breaks down for complex business logic. Hard to test. |

---

## Bullet 10 — Power BI + DAX for Financial Compliance KPIs

> *"Developed Power BI dashboards with DAX measures for compliance KPI reporting, connecting to Snowflake via DirectQuery to deliver real-time financial insights for 15+ enterprise tenants."*

---

### STAR Story

**Situation**  
Compliance officers at each of Samay's 15 client firms needed to track KPIs like: % of trades reviewed on time, open regulatory findings by severity, employee training completion rates, and days since last audit. These weren't nice-to-have dashboards — in financial services, a compliance officer who can't prove oversight in real-time has a regulatory problem. They needed live numbers, not yesterday's Excel export.

**Task**  
Build Power BI dashboards for compliance KPIs that (1) reflected real-time data, (2) were scoped per tenant so each firm saw only their own data, and (3) had DAX measures that correctly implemented financial compliance business logic.

**Action — Step by step**

1. **DirectQuery vs Import**:  
   I chose **DirectQuery** mode — queries go directly to Snowflake at report-open time. The alternative, Import mode, would cache data in Power BI and refresh on a schedule (fastest queries, but always stale by the refresh interval). For compliance reporting where officers needed live numbers before a regulatory call, stale data wasn't acceptable.

2. **Key DAX measures** I built:  
   
   **Trade review timeliness** (% of trades reviewed within required window):  
   ```dax
   On-Time Review % = 
   DIVIDE(
     CALCULATE(COUNTROWS(fact_trades), fact_trades[reviewed_within_sla] = TRUE),
     COUNTROWS(fact_trades),
     0
   )
   ```  
   
   **Rolling 30-day compliance score** (requires date intelligence):  
   ```dax
   30-Day Compliance Score = 
   CALCULATE(
     [Compliance Score],
     DATESINPERIOD(dim_date[date], LASTDATE(dim_date[date]), -30, DAY)
   )
   ```  
   `DATESINPERIOD` is a DAX time intelligence function — it returns a table of dates within a relative period from an anchor date. This pattern works because Power BI's date table enables the time-relative calculation to respect whatever date filter is active on the report.
   
   **YTD findings** (year-to-date regardless of current date filter):  
   ```dax
   YTD Findings = TOTALYTD(COUNTROWS(fact_findings), dim_date[date])
   ```

3. **Row Level Security for multi-tenancy**:  
   A single Power BI dataset served all 15 clients, but each compliance officer could only see their own firm's data. I implemented **Row Level Security (RLS)**:  
   - Created a role `TenantUser` with the DAX filter: `[tenant_id] = USERPRINCIPALNAME()`  
   - Each user's Azure AD UPN was mapped to their tenant ID in a `dim_user_tenant` table  
   - When a compliance officer logs into Power BI Service, their UPN is passed to the RLS filter, which restricts all visuals to their tenant's data automatically  

4. **Snowflake + DirectQuery performance**:  
   DirectQuery sends native SQL to Snowflake on every visual interaction. For this to be fast, the Snowflake models (built in dbt) needed to be pre-optimized: clustering keys on `event_date` and `tenant_id` (the most common filter combination), materialized aggregates for expensive KPIs, and query result caching enabled in Snowflake.

**Result**  
15 compliance teams got live, self-service dashboards replacing daily email reports. RLS ensured complete tenant isolation in one shared Power BI dataset. Compliance officers went from "I need to call the data team to pull this number" to "I can pull it up before my regulatory call in 30 seconds."

---

### 🔬 Technical Concept Breakdown

| Term | What It Is | Why It Matters |
|------|-----------|----------------|
| **DAX (Data Analysis Expressions)** | Formula language for Power BI and Excel Analysis Services. Used for measures and calculated columns. | The calculation engine of Power BI. You need it to go beyond basic aggregations. |
| **DAX Measure** | A formula evaluated dynamically in the current filter context. Not stored physically. | The right way to build KPIs. Always calculated fresh for whatever slicers are active. |
| **Filter Context** | The set of active filters (slicers, rows, columns) that constrain a DAX evaluation. | Everything in Power BI is evaluated relative to the current filter context. The core DAX concept. |
| **`CALCULATE()`** | Evaluates an expression in a modified filter context. The most powerful DAX function. | Override, add, or remove filters for a specific calculation. `CALCULATE(measure, filter)`. |
| **`DATESINPERIOD()`** | DAX time intelligence: returns a table of dates in a relative period from an anchor date. | Rolling N-day calculations. `DATESINPERIOD(date_col, anchor, -30, DAY)` = last 30 days. |
| **`TOTALYTD()`** | DAX shortcut for year-to-date calculation. Wraps `CALCULATE` with `DATESYTD`. | YTD metrics that respect the current date filter context. |
| **Power BI DirectQuery** | Power BI sends queries to Snowflake at report-render time. Always live, no cache. | Real-time data. Latency depends on Snowflake query performance. Needs good clustering/indexing. |
| **Row Level Security (RLS)** | Power BI security: DAX filter rules restricting which rows each user role sees. | Multi-tenant dashboards. One dataset, each user sees only their data. Enforced server-side. |
| **`USERPRINCIPALNAME()`** | DAX function returning the logged-in user's email/UPN. Used in RLS to filter by user. | Dynamic RLS — each user gets their own filtered view based on their identity. |

---

## Bullet 11 — dbt Transformation Layer with Tests and Documentation

> *"Implemented dbt transformation layer over Snowflake with modular SQL models, tests, and documentation, reducing ad hoc analyst SQL requests by 40% and improving data discoverability across the B2B platform."*

---

### STAR Story

**Situation**  
Before dbt, analysts at Samay's client firms submitted tickets to the data team for every custom report — "I need compliance events filtered by regulation type X, joined with employee table, grouped by department." The data team spent 40% of their time writing one-off SQL queries for analysts. There was also no central documentation of what tables existed or what columns meant — analysts didn't know what data was available, so they kept asking.

**Task**  
Build a dbt project that (1) standardized the transformation logic into reusable, well-documented models, (2) generated browsable documentation analysts could explore self-service, and (3) provided data quality tests so analysts could trust what they queried.

**Action — Step by step**

1. **dbt docs**:  
   dbt auto-generates a browsable documentation site from `schema.yml` descriptions. I wrote descriptions for every model and every column:  
   ```yaml
   models:
     - name: mart_compliance__trade_reviews
       description: "One row per trade requiring compliance review. Updated incrementally every 2 hours."
       columns:
         - name: trade_id
           description: "Unique identifier for a trade. Foreign key to dim_trade."
           tests:
             - not_null
             - unique
         - name: review_sla_breached
           description: "True if the trade was not reviewed within the regulatory 24-hour window."
   ```  
   Running `dbt docs generate` + `dbt docs serve` produced a searchable HTML site with table descriptions, column definitions, lineage graphs, and test results.

2. **dbt lineage graph**:  
   dbt's docs site includes a **DAG visualization** — you can see which sources feed which staging models, which staging feeds which intermediate models, and which intermediates feed which marts. An analyst looking for "where does trade review data come from?" could navigate the lineage graph visually.

3. **Modular SQL models**:  
   I built **semantic models** in the mart layer that analysts could query directly with no additional joins:  
   - `mart_compliance__trade_reviews`: Pre-joined trade + employee + regulation data with all derived metrics  
   - `mart_compliance__findings_summary`: Pre-aggregated findings by tenant, regulation, and severity  
   - `mart_compliance__training_completion`: Pre-joined training records with employee and training requirement tables  
   
   These covered 90% of analyst query patterns. Instead of writing complex SQL, analysts ran: `SELECT * FROM mart_compliance__trade_reviews WHERE tenant_id = '...' AND review_date >= '2024-01-01'`.

4. **Reducing ad-hoc requests**:  
   The 40% reduction came from two things: (1) analysts could now query pre-joined marts instead of asking the data team to build custom joins, and (2) the self-service dbt docs let analysts discover what tables existed and what columns meant without emailing anyone.

**Result**  
Data team's ad-hoc analyst request load dropped 40%. New analyst onboarding: "read the dbt docs, query the mart layer." Analysts went from black-box data consumers to self-sufficient query writers.

---

## Bullet 12 — Unity Catalog RBAC + Column Security + Audit Lineage

> *"Enforced data governance using Unity Catalog RBAC policies, column-level security, and audit lineage across Databricks workspaces, achieving compliance with enterprise data access control requirements for 15+ clients."*

---

### STAR Story

**Situation**  
Financial compliance data is extremely sensitive — one client's trade data must be completely invisible to another client's users. Within a client, junior compliance analysts should see aggregated reports but not raw PII (Social Security numbers, account numbers in trade records). Senior analysts and compliance officers needed full access. Regulators required audit trails proving who accessed what data and when.

**Task**  
Implement a data access control system in Databricks Unity Catalog that enforced multi-tenant isolation, column-level PII masking, and produced audit logs for regulatory review.

**Action — Step by step**

1. **Unity Catalog RBAC hierarchy**:  
   Unity Catalog organizes data as: **Catalog → Schema → Table**. RBAC is applied at any level:  
   - `GRANT USE CATALOG ON CATALOG tenant_acme TO GROUP acme_analysts` — gives Acme analysts access to Acme's catalog only  
   - `GRANT SELECT ON TABLE tenant_acme.silver.compliance_events TO GROUP acme_analysts`  
   - No Acme analyst can even see the existence of tenant_bcorp's catalog — not just access denied, completely invisible  

2. **Column masking policies**:  
   For PII columns (employee SSN, account numbers), I created **Dynamic Data Masking** policies:  
   ```sql
   CREATE OR REPLACE FUNCTION mask_ssn(ssn STRING)
   RETURNS STRING
   RETURN CASE WHEN IS_MEMBER('compliance_officers') THEN ssn
               ELSE CONCAT('XXX-XX-', RIGHT(ssn, 4))
          END;
   
   ALTER TABLE silver.employee_records
   ALTER COLUMN ssn SET MASK mask_ssn;
   ```  
   A compliance officer sees `123-45-6789`. A junior analyst sees `XXX-XX-6789`. Same query, same table, different result based on group membership. Zero application code changes needed.

3. **Audit lineage**:  
   Unity Catalog's **System Tables** (enabled in account settings) record every data access event in tables like `system.access.audit` — who ran what query, what tables and columns were accessed, at what time, from which IP and cluster. I set up a Dagster job that periodically queried these audit tables and produced a weekly "data access report" per tenant showing all access events for their data. This was the deliverable regulators required.

4. **Row filters**:  
   In addition to column masking, I added **row filter policies** on multi-tenant tables: even if a user somehow accessed a shared table (which they shouldn't under catalog-level RBAC), a row filter ensured they'd only see rows where `tenant_id = current_user_tenant()`.

**Result**  
All 15 clients' data governance requirements met. Audit reports produced automatically from Unity Catalog system tables. Zero cross-tenant data leakage incidents. Compliance team could demonstrate to regulators exactly which users accessed which data during any time period.

---

### 🔬 Technical Concept Breakdown

| Term | What It Is | Why It Matters |
|------|-----------|----------------|
| **Unity Catalog RBAC** | `GRANT`/`REVOKE` on Catalog/Schema/Table/Column level. Users inherit permissions from groups. | Fine-grained, auditable access control across all Databricks workspaces. |
| **Dynamic Data Masking** | A column-level policy function that returns masked values to unauthorized users but real values to authorized ones. | Same query, different results by role. PII visible to authorized users only, no app changes needed. |
| **Row Filter Policy** | A policy that automatically appends a WHERE clause to queries on a table based on the user's identity. | Tenant isolation at the row level. Even if the wrong user queries a shared table, they only see their rows. |
| **Unity Catalog System Tables** | Databricks-managed tables in `system.*` schemas recording audit logs, lineage, and usage. | `system.access.audit` = every data access event. The backbone of compliance audit reporting. |
| **Data Lineage** | Tracking the origin, movement, and transformation of data from source to final table. | Compliance requirement: "show us where this data came from and who touched it." |

---

## Bullet 13 — Terraform + Azure DevOps CI/CD (Multi-Tenant)

> *"Provisioned Azure data infrastructure (ADLS Gen2, ADF, Databricks, Synapse) with Terraform and Azure DevOps CI/CD pipelines, reducing manual deployment errors by 40% across multi-tenant environments."*

---

### STAR Story

**Situation**  
Each of Samay's 15 client environments had its own isolated Azure infrastructure — separate ADLS accounts, ADF instances, Databricks workspaces, and Synapse Analytics. Changes to the shared platform (like adding a new pipeline type, updating a Databricks runtime version) had to be rolled out to 15 environments. Manual deployment scripts had a 40% error rate because someone always forgot to update one of the 15 environments, or applied a config change to prod but not staging.

**Task**  
Codify the entire per-tenant Azure infrastructure in Terraform with a CI/CD pipeline that deployed consistently to all environments.

**Action — Step by step**

1. **Terraform modules for reuse**:  
   I built Terraform **modules** — reusable infrastructure packages. The `tenant_environment` module provisioned the full stack for one tenant (ADLS + ADF + Databricks + Synapse + Key Vault + RBAC). To add a new tenant, you called the module with tenant-specific variables:  
   ```hcl
   module "tenant_acme" {
     source = "./modules/tenant_environment"
     tenant_id = "acme"
     environment = "prod"
     region = "eastus2"
     compliance_tier = "financial"
   }
   ```

2. **Azure DevOps CI/CD flow**:  
   - **PR pipeline**: `terraform fmt` check (enforces consistent formatting), `terraform validate`, `terraform plan` for each environment. Plan output posted as PR comment.  
   - **Merge to main**: `terraform apply` sequentially for dev → staging → prod, with a manual approval gate between staging and prod.  
   - **Drift detection**: A nightly job ran `terraform plan` against each environment and alerted if there was any drift (manual changes made in the Azure Portal that aren't in Terraform).

3. **Azure Synapse integration**:  
   Azure Synapse Analytics was used by some clients as a dedicated SQL pool for heavy analytical queries that benefited from Synapse's MPP (Massively Parallel Processing) architecture — queries that needed to scan and aggregate billions of rows interactively. I provisioned Synapse dedicated SQL pools via Terraform and built ADF pipelines that loaded data from ADLS into Synapse using PolyBase (Synapse's high-throughput bulk load mechanism).

**Result**  
Deployment error rate dropped 40% because every change went through code review and automated validation before touching any environment. Rolling out a platform update to 15 environments: one PR, one merge, one automated pipeline run.

---

### 🔬 Technical Concept Breakdown

| Term | What It Is | Why It Matters |
|------|-----------|----------------|
| **Terraform Module** | A reusable, parameterized Terraform configuration package. Called like a function with variables. | Write once, deploy many times with different inputs. The DRY principle applied to IaC. |
| **Azure Synapse Analytics** | Azure's unified analytics service: on-demand serverless SQL, dedicated SQL pools (MPP), and Spark. | Dedicated SQL pools = Massively Parallel Processing for very large interactive queries. |
| **MPP (Massively Parallel Processing)** | Database architecture that distributes query processing across many nodes in parallel. | Synapse/Redshift use this. Very fast for large scans and aggregations on petabyte-scale data. |
| **Drift Detection** | Identifying when real infrastructure differs from Terraform's desired state (due to manual Portal changes). | Prevents config drift. Manual Portal changes that aren't in Terraform will be overwritten on next apply. |
| **Manual Approval Gate** | A CI/CD pipeline stage that pauses and requires a human to approve before continuing to prod. | Safety. Never automatically deploy to production without human sign-off. |
| **`terraform fmt`** | Formats Terraform files to the canonical style. Used in CI to enforce consistent formatting. | Code style consistency for HCL files. Like `black` for Python or `prettier` for JavaScript. |

---

---

# ZEMOSO TECHNOLOGIES — Associate Data Engineer (Jul 2020 – Aug 2022)
### *LabOps Platform*

---

## Bullet 14 — Python ETL with Pandas + PySpark into PostgreSQL

> *"Built Python ETL pipelines with Pandas and PySpark to ingest, clean, and transform scientific experiment datasets from lab instruments and REST APIs into a PostgreSQL analytical database for 500+ scientists."*

---

### STAR Story

**Situation**  
Zemoso built a LabOps platform for scientific research institutions. Lab instruments (centrifuges, spectrophotometers, PCR machines) generated experiment data in proprietary formats (CSV exports, instrument-specific JSON) and uploaded it to shared network drives. Scientists needed this data queryable in a centralized database for analysis and cross-experiment comparisons. The challenge: 500+ scientists, each with their own instrument and data format quirks.

**Task**  
Build Python-based ETL pipelines that ingested data from lab instruments and REST APIs, cleaned it, and loaded it into a PostgreSQL analytical database in a consistent, queryable schema.

**Action — Step by step**

1. **Pandas for small-to-medium datasets**:  
   For most instrument data (typically <1M rows per experiment), I used Pandas:  
   - `pd.read_csv()` / `pd.read_json()` to ingest  
   - `.dropna(subset=['experiment_id', 'measurement_value'])` — drop rows missing critical fields  
   - `.astype({'measurement_value': 'float64', 'recorded_at': 'datetime64[ns]'})` — type coercion  
   - `.drop_duplicates(subset=['reading_id'])` — deduplication  
   - Then write to PostgreSQL via `df.to_sql(table_name, engine, if_exists='append', index=False)`

2. **PySpark for large genomics datasets**:  
   Some genomics experiments produced datasets too large for a single machine's memory (10GB+ CSV files). For these I used PySpark on a small Databricks cluster — same logic, distributed across workers. The transformation code was nearly identical to Pandas thanks to the API similarity.

3. **REST API ingestion**:  
   Some instruments had REST API interfaces. I wrote a Python client with retry logic:  
   ```python
   def fetch_with_retry(url, max_retries=3):
       for attempt in range(max_retries):
           try:
               response = requests.get(url, timeout=30)
               response.raise_for_status()
               return response.json()
           except requests.RequestException as e:
               if attempt == max_retries - 1:
                   raise
               time.sleep(2 ** attempt)  # exponential backoff
   ```  
   Exponential backoff: wait 1s, then 2s, then 4s between retries. Prevents hammering a struggling API.

4. **PostgreSQL schema design**:  
   I designed the target schema with proper normalization for the write side but with analytical indexes for the read side:  
   - Primary tables: `experiments`, `readings`, `instruments`, `scientists`  
   - Composite indexes on `(experiment_id, recorded_at)` for the most common query pattern  
   - `JSONB` column for instrument-specific metadata (PostgreSQL's native semi-structured type — queryable with `->` operators)

**Result**  
500+ scientists had a single queryable database for all experiment data across all instrument types. Cross-experiment comparisons that previously required manual data assembly became single SQL queries.

---

## Bullet 15 — PostgreSQL Schema Design + Query Optimization

> *"Designed normalized PostgreSQL schemas and optimized SQL queries for LabOps experiment tracking workflows, improving data retrieval performance by 30% and data integrity across 500+ experiment datasets."*

---

### STAR Story

**Situation**  
Early in the project, the PostgreSQL database had grown organically — tables were added as needed, indexes were an afterthought, and queries that had been fast on small datasets were now taking 30+ seconds on the full 3-year data history. Scientists were complaining about the dashboard being unusable during busy lab periods.

**Task**  
Profile the slow queries, redesign the schema where needed, and add proper indexes to bring query times to acceptable levels.

**Action — Step by step**

1. **Query profiling**:  
   Used `EXPLAIN ANALYZE` in PostgreSQL (the gold-standard for query performance analysis). This shows:  
   - **Seq Scan** = bad (reading the whole table). **Index Scan** = good (using an index for efficient lookup).  
   - Actual rows scanned vs estimated rows — large discrepancy means stale statistics, fixed with `ANALYZE table`  
   - Where the most time was spent (Sort operations, Hash Join operations, nested loops)

2. **Index additions**:  
   The single biggest win: a `readings` query filtered on `experiment_id AND reading_type` but the index only covered `experiment_id`. Added a composite index `CREATE INDEX ON readings (experiment_id, reading_type)` — PostgreSQL could now satisfy both filter conditions from the index alone (index-only scan). Query time: 28 seconds → 3 seconds.

3. **Partial indexes** for selective queries:  
   Many queries only cared about `status = 'completed'` experiments. A full index on `status` is inefficient because there are only a handful of distinct values (low cardinality). Instead: `CREATE INDEX ON experiments (created_at) WHERE status = 'completed'` — a partial index that only indexes completed experiments. Smaller index, faster query for that specific filter.

4. **Schema normalization for data integrity**:  
   Found a data integrity issue: `instrument_type` was stored as a free-text column in `readings` — same instrument appeared as "PCR", "PCR Machine", "pcr machine" depending on who uploaded data. I added a `instruments` dimension table, made `instrument_id` a foreign key in `readings` with a `NOT NULL` constraint, and wrote a one-time migration to normalize existing values.

**Result**  
30% aggregate performance improvement across all tracked queries. The slowest dashboard query dropped from 28 seconds to 3 seconds. Data integrity issues on instrument type eliminated.

---

### 🔬 Technical Concept Breakdown

| Term | What It Is | Why It Matters |
|------|-----------|----------------|
| **`EXPLAIN ANALYZE`** | PostgreSQL command that executes a query and shows the actual execution plan with real row counts and timings. | The essential tool for query optimization. Shows you exactly where time is being spent. |
| **Sequential Scan (Seq Scan)** | Reading every row in a table. Fine for small tables or when you need most of the rows. | For large tables with selective filters, a Seq Scan means you're missing an index. |
| **Index Scan** | Using a B-tree (or other) index to find rows directly by key value. | Much faster than Seq Scan for selective queries. The goal of most query optimization. |
| **Composite Index** | An index on two or more columns: `CREATE INDEX ON table (col_a, col_b)`. | Most effective when queries filter on the leading columns in order. `(a, b)` helps `WHERE a=X AND b=Y`. |
| **Partial Index** | An index with a WHERE clause: only indexes rows matching the condition. | Smaller and faster than a full index for selective queries. `WHERE status = 'active'` on an active-records query. |
| **JSONB** | PostgreSQL's binary JSON column type. Indexable, queryable with operators like `->` and `->>`. | Store semi-structured data in PostgreSQL without losing queryability. Can add GIN indexes for JSONB key searches. |
| **Foreign Key Constraint** | A column-level constraint ensuring every value exists in the referenced table's primary key. | Referential integrity enforcement at the database level. Can't have a reading for a non-existent experiment. |

---

## Bullet 16 — Apache Airflow DAGs for Lab Data Workflows

> *"Orchestrated batch data workflows using Apache Airflow DAGs with retry logic, SLA alerting, and dependency management, reducing manual pipeline intervention by 35% across 10+ lab data products."*

---

### STAR Story

**Situation**  
By the time we had 10+ lab data pipelines running (one per instrument type, plus several cross-experiment aggregation jobs), there was no coordination — someone manually checked whether each one had run, and a failure in one job cascaded silently into downstream jobs producing stale reports without anyone noticing.

**Task**  
Implement Airflow orchestration that ran all 10+ pipelines in the right order, retried failures automatically, alerted on SLA breaches, and gave the team a central monitoring view.

**Action — Step by step**

1. **DAG design**:  
   The main nightly pipeline DAG:  
   ```
   ingest_instrument_a ──┐
   ingest_instrument_b ──┤──► clean_readings ──► compute_experiment_stats ──► refresh_dashboard
   ingest_instrument_c ──┘
   ```  
   The three ingest jobs ran in parallel (no dependency on each other). `clean_readings` waited for ALL ingest jobs with `trigger_rule='all_success'`. If any ingest failed, the cleaning step and everything downstream was automatically skipped — no stale data processed.

2. **Retry logic**:  
   Every task configured with:  
   ```python
   default_args = {
     'retries': 3,
     'retry_delay': timedelta(minutes=5),
     'retry_exponential_backoff': True,
   }
   ```  
   Exponential backoff on retries: waits 5 min, then 10 min, then 20 min. Handles transient network/API failures without hammering a struggling source.

3. **SLA alerting**:  
   Defined an SLA on the `refresh_dashboard` task: `sla=timedelta(hours=2)`. If the entire pipeline hadn't completed within 2 hours of the scheduled start, Airflow fired an SLA miss alert to the team's Slack channel. Scientists knew their morning reports would be fresh by 8 AM or they'd be notified if something was wrong.

4. **XComs for inter-task data**:  
   The ingest tasks pushed row counts to XCom: `context['ti'].xcom_push(key='rows_ingested', value=len(df))`. The `clean_readings` task pulled these counts and asserted the total was above a minimum threshold before proceeding — a lightweight sanity check that the ingest step actually produced data.

5. **vs Dagster** (since Acuity KP uses Dagster):  
   I built this on Airflow in 2020-2022, which was the industry standard at the time. The equivalent in Dagster would be defining each pipeline step as a `@asset`, using `AutoMaterializePolicy.eager()` so downstream assets auto-materialize when upstream ones are updated, and using `FreshnessPolicy` instead of SLA alerts. Same concepts, better ergonomics in Dagster.

**Result**  
35% reduction in manual intervention — previously 2-3 pipeline failures per week required a human to manually re-run jobs in the right order. Now Airflow handled retries and dependency management automatically. SLA alerts meant the team knew about problems before scientists complained.

---

## Bullet 17 — AWS Lambda + S3 Event-Triggered Ingestion

> *"Built AWS Lambda and S3-event-triggered ingestion jobs for automated raw data landing and archival, reducing manual upload overhead by 40%."*

---

### STAR Story

**Situation**  
Some lab instruments could only export data by pushing files to an S3 bucket (a common integration pattern). When a scientist finished an experiment, the instrument's export software uploaded the results file to S3. But then nothing happened — someone had to notice the file was there, manually trigger the ingestion pipeline, and verify it loaded. Scientists were running their own informal "did it load?" checks.

**Task**  
Make S3 file uploads trigger automatic ingestion — zero manual steps from "file arrives in S3" to "data available in PostgreSQL."

**Action — Step by step**

1. **S3 Event Notifications**:  
   S3 can publish events when objects are created, deleted, etc. I configured an **S3 Event Notification** on the `lab-raw-uploads` bucket: `ObjectCreated:Put` events trigger a target. The target was an AWS Lambda function.

2. **Lambda function**:  
   The Lambda received an event payload containing the S3 bucket name and object key of the uploaded file:  
   ```python
   def lambda_handler(event, context):
       bucket = event['Records'][0]['s3']['bucket']['name']
       key = event['Records'][0]['s3']['object']['key']
       
       # download file from S3
       obj = s3.get_object(Bucket=bucket, Key=key)
       df = pd.read_csv(obj['Body'])
       
       # validate and transform
       df = validate_and_clean(df)
       
       # write to PostgreSQL
       df.to_sql('raw_readings', engine, if_exists='append', index=False)
       
       # archive: move to processed/ prefix
       s3.copy_object(Bucket=bucket, CopySource=f"{bucket}/{key}", Key=f"processed/{key}")
       s3.delete_object(Bucket=bucket, Key=key)
   ```

3. **Why Lambda**:  
   Lambda is **serverless** — there's no server running permanently waiting for files. Lambda wakes up on-demand, processes the file, and shuts down. Cost: pay only for the execution time (usually milliseconds to seconds). For a workload like "process a file when it arrives, maybe 50 times a day," Lambda is far cheaper than running a dedicated EC2 instance.

4. **Archival**:  
   After successful processing, the Lambda moved the file from the `uploads/` prefix to `processed/` — a permanent archival location. This meant: (1) raw data was always preserved, (2) the `uploads/` folder only contained unprocessed files (easy to see what's pending), (3) reprocessing was possible (re-run Lambda against a `processed/` file if needed).

**Result**  
File upload → data in PostgreSQL: fully automated, under 3 minutes. Scientists no longer had a manual step in their workflow. The 40% overhead reduction came from eliminating the entire manual notification/trigger/verify loop.

---

### 🔬 Technical Concept Breakdown

| Term | What It Is | Why It Matters |
|------|-----------|----------------|
| **AWS Lambda** | Serverless function execution. Run code on-demand without managing servers. Pay per execution. | Event-driven compute. Perfect for "do X when Y happens" patterns with infrequent, bursty workloads. |
| **Serverless** | Infrastructure model where the cloud provider manages server provisioning and scaling. You write functions. | No idle server costs. Auto-scales. Zero ops. The tradeoff: cold starts, max execution time limits. |
| **S3 Event Notification** | S3 triggers a notification (to Lambda, SQS, SNS) when a specified event occurs (object created, deleted). | The primitive for S3-triggered automation. File arrives → Lambda fires immediately. |
| **S3 Object Key** | The full path of an object within a bucket: `uploads/tenant_acme/2024/01/data.csv`. | Think of it as the file path in S3. Includes "folders" (which are just key prefixes in S3). |
| **Cold Start** | The latency when Lambda initializes a new execution container (imports, connection setup). Usually 1-5 seconds. | For latency-sensitive workloads, keep Lambda warm with provisioned concurrency. For batch ingest, cold start is fine. |
| **Lambda Execution Role** | An IAM role assigned to the Lambda function defining what AWS services it can access. | Least-privilege: Lambda should only have `s3:GetObject`, `s3:PutObject`, `s3:DeleteObject` on the specific bucket it needs. |

---

## Bullet 18 — Full-Stack: React.js + Spring Boot + PostgreSQL

> *"Delivered full-stack experiment tracking features integrating React.js front-ends with Spring Boot REST APIs and PostgreSQL, providing accurate data entry and retrieval across 10+ regulated scientific workflows."*

---

### STAR Story

**Situation**  
Beyond building the data pipelines, scientists also needed a web UI to manually enter experiment metadata, search for past experiments, and download reports. The platform needed a front-end connected to a proper REST API — not just a BI dashboard.

**Task**  
Build full-stack features end-to-end: React.js UI for data entry and search, Spring Boot REST API for business logic, PostgreSQL for persistence.

**Action — Step by step**

1. **Spring Boot REST API**:  
   Built CRUD endpoints for experiment management:  
   - `POST /api/experiments` — creates a new experiment record with validation (`@Valid`, `@NotNull` annotations)  
   - `GET /api/experiments/{id}/readings` — paginated retrieval of readings for an experiment using Spring Data JPA with `Pageable`  
   - `GET /api/experiments/search?scientist=X&dateFrom=Y&dateTo=Z` — parameterized search using Spring Data JPA `@Query` with JPQL  
   
   Data persistence via Spring Data JPA (Hibernate) — no raw SQL for CRUD operations, JPA generates it. For complex analytical queries (aggregations, window functions), I used native SQL via `@Query(nativeQuery=true)`.

2. **React.js front-end**:  
   Used React functional components with hooks:  
   - `useState` for form state management  
   - `useEffect` for fetching experiment data on component mount and on filter changes  
   - `useCallback` to avoid unnecessary API calls on re-renders  
   
   Search results table with client-side pagination (React `useState` tracking current page, fetching next page on scroll).

3. **Data entry validation**:  
   Validated at three layers:  
   - Front-end: HTML5 constraint validation + React custom validation hooks (immediate feedback)  
   - API layer: `@Valid` + Bean Validation annotations (`@NotNull`, `@Size`, `@Pattern` for required format)  
   - Database layer: `NOT NULL`, `CHECK`, and `UNIQUE` constraints in PostgreSQL  
   
   Defense in depth — a bad value rejected at the front-end is UX; rejected at the database is the last line of data integrity.

**Result**  
Scientists could enter experiment metadata, search historical experiments, and export reports entirely through the web UI — no database access or data team involvement. 10+ regulated workflows supported with proper validation at every layer.

---

---

# QUICK REFERENCE — 30-Second Pre-Interview Mental Warm-Up

| Concept | One-liner to recall |
|---------|---------------------|
| **Medallion Architecture** | Bronze (raw) → Silver (clean) → Gold (analytics). Every layer boundary has quality gates. |
| **Delta Live Tables** | Declarative Databricks pipeline framework. Define tables as functions. Auto-handles retries, quality, lineage. |
| **Delta Lake** | Parquet + transaction log = ACID + time travel + schema enforcement. Makes storage reliable like a DB. |
| **dbt** | SQL-only transformation framework. `SELECT` statements become tables/views. Tests + docs built in. |
| **dbt Incremental** | On first run: full build. On subsequent runs: only new rows (watermark filter). 90s vs 20min. |
| **Snowpipe** | Snowflake's continuous micro-batch ingest triggered by new file in ADLS/S3. 1-2 min SLA. |
| **Snowflake Clustering Key** | Co-locates micro-partitions by key value. Queries on that column scan 5% of data instead of 100%. |
| **Dagster vs Airflow** | Dagster = asset-centric (what data). Airflow = task-centric (what work). Dagster is the modern choice. |
| **Dagster Asset** | `@asset` function = a unit of data in the asset graph. Has dependencies, freshness policy, observability. |
| **Great Expectations** | Assertion-based data quality. `expect_column_not_null`, `expect_row_count_between`, etc. |
| **Elementary** | dbt package: stores test results as data over time. Trending + anomaly detection on dbt tests. |
| **ADF** | Azure's managed ELT orchestration. Linked Services → Datasets → Pipelines. Good for cloud data movement. |
| **Event Hubs** | Azure Kafka equivalent. Partitioned, durable, Consumer Groups for independent readers. |
| **Structured Streaming** | Spark's streaming engine. Treat stream as unbounded DataFrame. 30s trigger = micro-batch. |
| **Checkpoint** | Spark persists stream progress in ADLS. Crash + restart = resume from last checkpoint, no duplicates. |
| **Terraform** | IaC: declare desired infra in HCL, `plan` to preview, `apply` to deploy. Reproducible, version-controlled. |
| **Key Vault** | Azure secrets management. Never hardcode credentials. Runtime retrieval via SDK or Databricks `dbutils.secrets`. |
| **Unity Catalog** | Databricks governance: Catalog → Schema → Table hierarchy. Column masking, row filters, audit lineage. |
| **RBAC (Least Privilege)** | Every user/role has exactly the minimum permissions needed. Nothing more. Limits blast radius. |
| **DAX CALCULATE** | Evaluates a measure in a modified filter context. The most important DAX function. |
| **DAX DirectQuery** | Power BI queries Snowflake live at render time. Always fresh. Needs Snowflake clustering to be fast. |
| **Power BI RLS** | DAX filter by role. Same dataset, each user sees their own tenant's rows. `USERPRINCIPALNAME()`. |
| **Schema Evolution** | `mergeSchema=True` on Delta write: new source columns auto-added to table. No pipeline failure. |
| **Watermark Pattern** | Save max(timestamp) as state. Next run: only process rows newer than watermark. Incremental ELT foundation. |
| **Idempotent Write** | Run the same job twice, same result, no duplicates. MERGE/upsert = idempotent. INSERT = not. |
| **Z-Ordering** | `OPTIMIZE ZORDER BY col` — co-locates data with similar values for faster queries on non-partition columns. |
| **EXPLAIN ANALYZE (PG)** | Shows actual query execution plan with timings. Seq Scan = missing index. Index Scan = good. |

---

*Last updated: 2026-07-06 | Acuity KP — Senior Data Engineer Interview*




> [!example]- Alternate source version (html)
> ## Acuity KP Interview Prep — Full STAR Technical Story Bank 
>
>   
>
> Role: Data Engineer | Company: Acuity KP
>  Your Resume: Epik Solutions → Samay Systems LLC → Zemoso Technologies
>  Every single bullet → deep STAR story + concept teardown + follow-up armor.
>  Read top to bottom. Each story builds vocabulary for the next.
>
>    
>
> ### HOW TO USE THIS DOC 
>
>   
> - STAR Story — lock in the narrative arc, memorize the flow 
> - Concept Breakdown — every technical term defined (so follow-ups can't touch you) 
> - Natural Phrasing — what to say out loud, in a human voice, in the room 
> - Follow-ups — pre-loaded answers for the questions that always come next   
>
> ## PYTHON -- Deep Dive Stories & Concept Reference 
>
>   
>
> Acuity KP specifically wants strong Python. Five STAR stories drawn from your real work,
>  each covering the Python design decisions, library choices, and architectural reasoning
>  behind the code -- not the syntax, but the thinking.
>
>    
>
> ### Python Story 1 -- OOP Framework Design for Reusable ELT Pipelines 
>
>   
>
> At Samay Systems you built a Python framework used across 15+ client pipelines.
>  This directly answers the JD requirement: "develop reusable data engineering frameworks."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>
>  
>
> At Samay I was building compliance ELT pipelines for 15 enterprise clients simultaneously.
>  Every client had a different source system -- some were REST APIs, some were SFTP flat file
>  drops, some were direct database connections. Without structure, each pipeline was a
>  standalone script with copy-pasted retry logic, logging, error handling, and validation.
>  When I found a bug in the retry mechanism, I had to fix it in 15 different files. That
>  maintenance overhead was unsustainable, and the risk of divergence was real -- one pipeline
>  getting a fix that five others never received.
>
>  
>
> Task
>
>  
>
> Design a Python framework where common infrastructure (logging, retries, connection
>  management, schema validation) lived once and was inherited automatically by every pipeline,
>  while each client-specific pipeline only implemented the unique extraction and transformation
>  logic for its particular source system.
>
>  
>
> Action -- The design decisions
>
>  
>
> The foundation was Python's Abstract Base Class system, using ABC from the built-in abc
>  module. I created a BaseExtractor class that inherited from ABC and marked the extract
>  method with @abstractmethod. The consequence of this decorator is that Python will raise a
>  TypeError at instantiation time if any subclass fails to implement extract -- it cannot
>  even be instantiated. This moves the "did you forget to implement this?" check from runtime
>  (buried inside a 4-hour pipeline run) to construction time (caught immediately when the
>  object is created).
>
>  
>
> The design pattern at work is the Template Method pattern. The run method on the base class
>  defines the algorithm skeleton -- log the start, call extract, handle errors, log
>  completion. Subclasses override only extract, never run. This means every pipeline
>  automatically inherits consistent logging and error handling without any subclass needing to
>  think about it. A new engineer building a 16th client pipeline cannot accidentally ship
>  without logging because the base class provides it unconditionally.
>
>  
>
> For the extract method I designed it as a Python generator -- it uses yield to produce
>  DataFrames in chunks rather than returning one giant collection. The critical insight here is
>  memory: if a source has 10 million rows, loading everything into a list and returning it means
>  10 million rows in RAM simultaneously. With a generator, only one chunk (say 10,000 rows) is
>  in memory at any moment. The caller consumes each chunk, processes it, discards it, and asks
>  for the next one. The base class's run method uses yield from self.extract() which
>  delegates to the subclass generator transparently -- the whole pipeline becomes a streaming
>  chain without any single component holding the full dataset.
>
>  
>
> Configuration across 15 clients meant 15 different sets of parameters -- API URLs, batch
>  sizes, schema names, retry counts. I used Python's @dataclass decorator for configuration
>  objects. The decorator auto-generates __init__, __repr__, and __eq__ from the class
>  annotations, eliminating boilerplate. The important technical detail is field(default_factory=list)
>  for any list-type attribute. The naive approach -- writing tags: list = [] as a default --
>  creates a single list object once when the class is defined and shares it across all instances.
>  This is the mutable default argument bug: mutate the list on one instance and every other
>  instance sees the mutation. field(default_factory=list) tells the dataclass machinery to
>  call list() fresh for each new instance. I also used __post_init__ for validation --
>  the method runs automatically after __init__ completes, so invalid configurations raise
>  ValueError at object construction rather than failing deep inside a pipeline run.
>
>  
>
> Resource management -- database connections, file handles -- used Python context managers
>  via the @contextmanager decorator from contextlib. A context manager separates the
>  resource acquisition from resource release using a finally block that always executes
>  regardless of whether an exception was raised inside the with block. Writing it as a
>  decorated generator function (rather than a class with __enter__ and __exit__) is
>  simpler and reads more naturally. The downstream effect: no leaked Snowflake connections
>  even when a pipeline crashes halfway through.
>
>  
>
> For type safety across the framework I used Python type hints throughout -- Iterator[pd.DataFrame]
>  as the return type of extract, str | None for optional strings, PipelineConfig as the
>  parameter type for functions that accept configuration. These are not enforced at runtime by
>  default Python, but I ran mypy in CI as part of every pull request. Mypy is a static type
>  checker that reads the annotations and catches type mismatches before code ever runs --
>  a None dereference that would crash at 2 AM in a production pipeline gets caught as a CI
>  failure when the PR is raised.
>
>  
>
> I also used Protocol from typing for interfaces at the boundary between the framework
>  and callers. A Protocol is Python's structural typing mechanism -- any class that has the
>  right method signatures satisfies the Protocol, regardless of inheritance. This is different
>  from ABC which requires explicit inheritance. The distinction matters at architectural
>  boundaries: within the framework, ABC enforces implementation contracts at construction
>  time. At the framework's public API, Protocol allows callers to provide their own
>  implementations without inheriting from your base classes -- looser coupling, easier to test.
>
>  
>
> Result
>
>  
>
> One framework, 15 pipelines. A bug fix to retry logic required a single PR that propagated
>  to all clients automatically. Adding a new client integration meant creating one subclass,
>  implementing extract, and zero other code. The framework layer -- logging, retries,
>  connection management, schema validation -- never appeared in any client-specific file.
>  Onboarding time for a new pipeline dropped from two days to under half a day.
>
>   
>
> #### Technical Concept Breakdown 
>
>    
>
>   | Concept  | What It Is  | Why It Matters in Your Context 
>
>    
>
>   | Abstract Base Class (ABC)  | A class with @abstractmethod methods that subclasses must implement. Python raises TypeError at instantiation if any abstract method is missing.  | Moves "forgot to implement" bugs from runtime to construction time. At scale, this is the difference between a midnight prod failure and a caught bug before deployment. 
>
>  
>
>   | @abstractmethod  | Decorator that marks a method as required for all non-abstract subclasses.  | Enforces the interface contract at the language level, not through documentation or convention. 
>
>  
>
>   | Template Method Pattern  | The base class defines an algorithm skeleton with fixed and variable steps. Subclasses override only the variable steps.  | Shared infrastructure (logging, retries) lives once. Subclasses focus exclusively on their unique logic. No risk of infrastructure code being forgotten or diverging. 
>
>  
>
>   | Generator / yield  | A function that uses yield to produce values lazily, one at a time. Does not execute past the yield until the caller requests the next value.  | Memory-efficient streaming. 10M row extracts stay flat in memory because only one chunk at a time is ever materialized. 
>
>  
>
>   | yield from  | Delegation syntax for generators. yield from gen() is equivalent to iterating through gen() and yielding each value, but without the overhead of an explicit loop.  | Lets run() delegate to extract() transparently while keeping the streaming chain intact. 
>
>  
>
>   | @dataclass  | Class decorator that auto-generates __init__, __repr__, and __eq__ from annotated fields.  | Eliminates config class boilerplate. Derived fields and validation go in __post_init__. 
>
>  
>
>   | field(default_factory=...)  | Calls the factory function to create a fresh object for each dataclass instance.  | Prevents the mutable default argument bug: default=[] shares one list object across ALL instances. default_factory=list creates a new list per instance. 
>
>  
>
>   | __post_init__  | Called by the dataclass machinery after __init__ completes. Used for validation and derived field computation.  | Validate at construction time -- wrong config raises immediately, not mid-pipeline. 
>
>  
>
>   | @contextmanager  | Decorator that turns a generator with a single yield into a context manager. The finally block after the yield always runs on exit.  | Simpler than writing __enter__/__exit__. Guarantees resource cleanup even on exceptions. 
>
>  
>
>   | Type hints + mypy  | PEP-484 annotations (str, int, Iterator[T]) for function signatures. Mypy is the static type checker that enforces them at CI time.  | Catches type errors before runtime. Makes function signatures self-documenting. Enables IDE autocomplete on complex types. 
>
>  
>
>   | Protocol  | Structural typing interface. A class satisfies a Protocol if it has the required method signatures -- no inheritance needed.  | Looser coupling at API boundaries. Callers can pass in anything with the right methods; they don't need to inherit from your classes. Easier to mock in tests. 
>
>     
>
> #### How to Say It in the Interview 
>
>  
>
> "At Samay I had to solve a real maintenance problem -- 15 client pipelines that were
>  essentially the same script copy-pasted with different configs. I built a Python OOP
>  framework around the Abstract Base Class pattern. The base class used the Template Method
>  design pattern: run() defined the skeleton -- logging, retry, error handling -- and
>  subclasses only implemented extract(), which was a generator that yielded DataFrame chunks
>  for memory efficiency. The key enforcement mechanism was @abstractmethod -- Python itself
>  raised a TypeError if you tried to instantiate a subclass that hadn't implemented extract,
>  so you could never accidentally deploy an incomplete pipeline. Configuration was dataclasses
>  with field(default_factory=list) for mutable defaults -- avoiding the classic Python bug
>  where all instances share one list object. I also ran mypy in CI so type errors were caught
>  at PR time rather than at 2 AM in production."
>
>   
>
> #### Likely Follow-up Questions 
>
>  
>
> "What is the mutable default argument bug?"
>  The problem occurs when you write a function or class with a mutable object as a default
>  parameter value -- for example def __init__(self, tags=[]). Python creates that default
>  list once when the function definition is executed, and every call that uses the default
>  shares the same list object. If one caller appends to the list, the next caller sees that
>  mutation. The fix is to use None as the default and create the list inside the function
>  body, or in dataclasses, use field(default_factory=list) to create a fresh list for each
>  instance.
>
>  
>
> "Difference between ABC and Protocol?"
>  ABC is nominal typing -- a class must explicitly inherit from the ABC to satisfy it.
>  If a subclass fails to implement an abstract method, Python raises TypeError at
>  instantiation. Protocol is structural typing -- any class that has the right method
>  signatures satisfies the Protocol, regardless of inheritance. ABC is appropriate within a
>  framework where you control all implementations and want hard enforcement. Protocol is
>  appropriate at public API boundaries where you want to accept anything duck-typed-compatible
>  without forcing callers to inherit from your classes.
>
>  
>
> "Why use a generator instead of returning a list?"
>  A generator uses yield to produce values lazily -- it only runs until the next yield
>  when the caller requests the next value. Returning a list materializes everything in memory
>  at once. For a pipeline extracting 10 million compliance records, returning a list means
>  holding all 10 million rows in RAM simultaneously. A generator that yields 10,000-row
>  chunks means the maximum RAM usage at any point is one chunk. The downstream pipeline can
>  process, write, and discard each chunk before requesting the next. It also enables short
>  circuits -- if a downstream error occurs after the first three chunks, you never extracted
>  the remaining seven.
>
>   
>
> ### Python Story 2 -- PySpark DataFrame API: Schemas, Pandas UDFs, Window Functions 
>
>   
>
> Every Databricks and PySpark bullet on your resume is Python. This story covers the
>  Python-specific decisions that separate correct PySpark from fast, production-grade PySpark.
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>
>  
>
> At Epik, security event data arriving from Azure Event Hubs was raw JSON bytes with no
>  enforced schema. The Bronze-to-Silver transformation required parsing these bytes into a
>  strongly typed structure, running custom enrichment logic that plain Spark SQL could not
>  express (IP address classification, threat score normalization based on internal lookup
>  tables), and computing stateful rolling statistics -- event rate per source IP per tenant
>  over a sliding 5-minute window. These requirements pushed against the edges of what Spark
>  SQL handles naturally.
>
>  
>
> Task
>
>  
>
> Write PySpark transformations in Python that were: schema-enforced at ingestion, enriched
>  with custom Python logic at production speed, and augmented with rolling-window statistics.
>  The wrong Python choices here (inferred schemas, row-by-row UDFs) would have worked
>  functionally but been 10-50x slower at the event volumes we were processing.
>
>  
>
> Action -- The design decisions
>
>  
>
> For schema definition I always write explicit StructType objects with StructField entries
>  rather than relying on inferSchema=True. The inferSchema option reads the entire input
>  file or JSON body to guess types -- this is expensive, and for streaming from Event Hubs,
>  impossible (a stream has no end to sample from). More importantly, inferSchema makes
>  assumptions that are often wrong: a column that happens to contain only "1234" in the
>  sample data gets inferred as LongType when the business requirement is StringType because
>  it is a code, not a number. Explicit schemas also allow nullable=False on columns that
>  must never be null -- setting this means Spark will reject writes with null values in that
>  column if schema enforcement is enabled on the Delta table, turning data quality from a
>  convention into a constraint. For the semi-structured metadata field (arbitrary key-value
>  pairs per event type), I used MapType(StringType(), StringType()) which represents a
>  dictionary column in Spark's type system -- queryable by key using bracket notation.
>
>  
>
> For custom enrichment logic, the decision between Python UDFs, Pandas UDFs, and Spark SQL
>  built-in functions is one of the most important performance choices in PySpark Python work.
>  The built-in Spark SQL functions (things like from_json, regexp_extract, unix_timestamp,
>  to_date) are the fastest option because they execute entirely inside the JVM without
>  crossing the language boundary at all. When business logic is too complex for built-ins, the
>  next choice is a Pandas UDF, also called a vectorized UDF. A Pandas UDF is decorated with
>  @pandas_udf and its function signature receives and returns a pd.Series -- an entire
>  column at once rather than one row at a time. The bridge between JVM and Python in a
>  Pandas UDF uses Apache Arrow, an in-memory columnar data format designed for zero-copy data
>  transfer. Zero-copy means the data is not serialized and deserialized -- the memory layout
>  that Spark uses internally is the same format Arrow uses, so transferring the entire column
>  to Python has near-zero overhead compared to serializing each row individually.
>
>  
>
> A regular Python UDF does the opposite: it serializes each row from the JVM to the Python
>  process using pickle, executes Python on that single row, serializes the result back via
>  pickle, then moves to the next row. This row-by-row ping-pong across the JVM-Python boundary
>  is the source of the 10-50x slowdown. The only time to use a regular Python UDF is when
>  the logic truly cannot be vectorized -- when it involves stateful Python objects that cannot
>  operate on a Pandas Series. In practice, IP address classification, URL parsing, custom
>  normalization logic, and most string processing can all be vectorized easily with Pandas
>  Series methods.
>
>  
>
> Window functions addressed the stateful rolling-statistics requirement. A window function
>  in Spark computes a value for each row using a defined "window" of related rows, without
>  collapsing the DataFrame the way groupBy and agg would. The window definition has three
>  components: partitionBy which resets the window for each group (equivalent to GROUP BY in
>  SQL), orderBy which defines row ordering within the partition, and a frame specification
>  that defines which rows are included in the window relative to the current row. For the
>  rolling 5-minute event count per tenant-IP pair, I used rangeBetween(-300, 0) on a Unix
>  timestamp column. The rangeBetween frame uses the ORDER column's numeric value -- so
>  -300, 0 means "include all rows whose Unix timestamp is within 300 seconds before and
>  equal to the current row's timestamp." This is a time-range window. The alternative,
>  rowsBetween(-N, 0), counts N preceding rows by position regardless of their timestamp
>  values -- this would give a rolling event count by count, not by time, which would be wrong
>  when event rates are variable.
>
>  
>
> The lag function computes the value from N rows behind the current row within the same
>  partition and ordering -- this is how I computed "seconds since last event from the same
>  source IP," which was the primary signal for detecting automated scanning patterns. A human
>  browsing a network will have irregular inter-event gaps. An automated scanner produces
>  events at a consistent machine-speed rate. lag(unix_timestamp_col, 1) gives the
>  previous row's timestamp, and subtracting gives the delta.
>
>  
>
> The most common PySpark Python mistakes I explicitly avoided: calling collect() which
>  pulls the entire DataFrame to the driver node (fine for summary statistics on small outputs,
>  catastrophic on raw event data); calling count() in a loop which triggers a full Spark job
>  per iteration; and creating Spark operations inside a UDF (UDFs must be pure Python functions
>  with no access to the Spark context).
>
>  
>
> Result
>
>  
>
> Schema-enforced, null-rejecting Bronze-to-Silver transformation in Python. IP classification
>  via Pandas UDFs ran at the same order of magnitude as pure SQL for our event volumes.
>  The rolling 5-minute event count enabled a rate-based alerting rule that caught three genuine
>  security incidents in the first month of operation -- incidents that the threshold-only rules
>  missed because they considered aggregate daily totals rather than instantaneous event rates.
>
>   
>
> #### Technical Concept Breakdown 
>
>    
>
>   | Concept  | What It Is  | Why It Matters in Your Context 
>
>    
>
>   | StructType / StructField  | Explicit Spark schema definition. Each field has a name, type, and nullable flag.  | Never use inferSchema in production. Explicit schemas catch type mismatches at write time, enable null enforcement, and are required for streaming. 
>
>  
>
>   | nullable=False  | Schema constraint that makes Spark reject writes with null values in that column when enforcement is on.  | Data quality enforced at the storage layer. Bad data is rejected at the gate rather than silently propagating. 
>
>  
>
>   | MapType  | Spark column type for a dictionary (key-value map) with variable keys.  | Models semi-structured data where not all rows have the same fields. Query via bracket notation on the column. 
>
>  
>
>   | Spark SQL built-in functions  | Functions like from_json, unix_timestamp, regexp_extract that execute in the JVM with no Python overhead.  | Fastest option. Use whenever business logic can be expressed with them. 
>
>  
>
>   | Regular Python UDF  | A Python function registered with Spark via udf(). Serializes data row-by-row via pickle across the JVM-Python boundary.  | Last resort -- row-by-row pickle serialization is 10-50x slower than vectorized alternatives. Use only when logic truly cannot be vectorized. 
>
>  
>
>   | Pandas UDF (vectorized UDF)  | A Python function decorated with @pandas_udf that receives and returns a pd.Series. Data transfers as a whole column via Apache Arrow.  | The right way to add Python logic at scale. Arrow's zero-copy transfer eliminates per-row serialization overhead. 10-50x faster than regular UDFs. 
>
>  
>
>   | Apache Arrow  | In-memory columnar data format used for zero-copy JVM-to-Python data transfer in Pandas UDFs.  | The technical reason Pandas UDFs are fast. Spark's internal memory format and Arrow's format are compatible -- no serialization needed. 
>
>  
>
>   | Window Function  | Computes a value for each row across a window of related rows without reducing the DataFrame.  | Rolling aggregations, lag/lead values, rankings -- stateful calculations across related rows that are impossible with plain groupBy. 
>
>  
>
>   | rangeBetween(start, end)  | Window frame defined by ORDER column value range relative to the current row. -300, 0 on a Unix timestamp = last 300 seconds.  | Time-based sliding windows. Distinct from rowsBetween which counts by row position. Critical distinction when event rates are variable. 
>
>  
>
>   | rowsBetween(start, end)  | Window frame defined by row position -- N preceding rows regardless of ORDER column values.  | Position-based rolling windows. Use for "last N events" semantics rather than "last N seconds." 
>
>  
>
>   | lag(column, N)  | Window function that returns the value from N rows behind the current row within the partition ordering.  | Compute inter-event deltas: current timestamp minus previous timestamp gives time since last event. 
>
>     
>
> #### How to Say It in the Interview 
>
>  
>
> "For PySpark I always write explicit StructType schemas rather than inferring them. Schema
>  inference requires reading the full dataset to guess types, is unreliable for schemas like
>  compliance codes where numeric-looking strings should stay as strings, and is impossible in
>  streaming where there's no end to sample from. For custom enrichment logic I use Pandas
>  UDFs rather than regular Python UDFs -- the difference is how data crosses the JVM-Python
>  boundary. A regular UDF uses pickle per row, one row at a time. A Pandas UDF transfers the
>  entire column via Apache Arrow, which is a zero-copy operation because Spark and Arrow use
>  the same in-memory columnar format. For the rolling 5-minute event count per source IP I
>  used a window function with rangeBetween(-300, 0) on a Unix timestamp column -- that is a
>  time-range window, meaning it includes all rows whose timestamp falls within 300 seconds of
>  the current row's timestamp, not a fixed row count. The distinction matters when event rates
>  vary -- a machine scanner fires 100 events in 5 minutes, a human might fire 3."
>
>   
>
> #### Likely Follow-up Questions 
>
>  
>
> "When do you use a Spark SQL built-in vs Pandas UDF vs Python UDF?"
>  Priority order: first, use a Spark SQL built-in function if one exists for the logic -- these
>  run entirely in the JVM with zero Python overhead and are always fastest. Second, if you need
>  Python logic, use a Pandas UDF with @pandas_udf so data transfers as a whole column via
>  Arrow. Third and last resort only, use a regular Python UDF when the logic truly cannot be
>  vectorized into a Pandas Series operation.
>
>  
>
> "What is the difference between rangeBetween and rowsBetween?"
>  rowsBetween(-3, 0) means the 3 rows immediately preceding the current row by position in
>  the partition's ordering -- it counts by row number. rangeBetween(-300, 0) means rows
>  whose ORDER column value is within 300 of the current row's value -- when the ORDER column
>  is a Unix timestamp, this means the last 300 seconds. For time-based windows where event
>  rates are variable, rangeBetween on a timestamp is the correct approach. rowsBetween
>  would give you a rolling 3-event window regardless of whether those 3 events happened over
>  1 second or 1 hour.
>
>  
>
> "What is the GIL and does it affect PySpark?"
>  The Global Interpreter Lock prevents multiple Python threads from executing Python bytecode
>  simultaneously in one process. In PySpark, the JVM manages true parallelism across worker
>  nodes -- Python UDFs run in separate Python processes on each worker, not in threads, so the
>  GIL is not a bottleneck for distributed work. The GIL matters when you try to use Python
>  multi-threading for CPU-bound parallelism within a single process -- for that, you need
>  multiprocessing, not threading.
>
>   
>
> ### Python Story 3 -- REST API Client: Pagination, Rate Limiting, Retry Backoff 
>
>   
>
> At Samay and Zemoso you built API integrations repeatedly. This is the production Python
>  patterns story for robust API clients.
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>
>  
>
> At Samay, each client's compliance data was pulled from 4 to 6 external REST APIs --
>  regulatory feeds, HR systems, sanctions screening APIs, trade surveillance endpoints. Some
>  had strict rate limits of 100 requests per minute. Some had unreliable uptime, returning 500
>  errors unpredictably under load. Regulatory APIs returned millions of compliance records
>  across thousands of pages. The naive approach -- a bare requests.get() loop -- failed
>  constantly: rate limit 429 responses, timeout exceptions, and APIs that returned 500 errors
>  midway through a 2-hour extract job, killing the entire run with no resume capability.
>
>  
>
> Task
>
>  
>
> Write a reusable Python API client class that handled pagination transparently, throttled
>  request rate to stay within API limits, and retried transient failures with exponential
>  backoff -- all reusable across every client integration without modification.
>
>  
>
> Action -- The design decisions
>
>  
>
> For retry logic I used the tenacity library rather than hand-rolling a retry loop. Tenacity
>  lets you compose retry strategies as decorators on the method that makes the actual HTTP
>  call. The strategy I used was wait_exponential with multiplier=1, min=2, max=60 -- this
>  means: wait 2 seconds before the first retry, double that to 4 seconds before the second,
>  8 before the third, 16 before the fourth, and cap at 60 seconds for any subsequent retries.
>  The exponential growth is important because it gives a struggling API server time to recover
>  rather than hammering it with retry requests every few seconds.
>
>  
>
> The retry_if_exception_type parameter is equally critical. I specified it to only retry on
>  requests.Timeout and requests.ConnectionError -- transient network conditions that are
>  worth retrying. If a ValueError occurs (programming error -- wrong field name), or a KeyError
>  (unexpected response structure), those are bugs in our code, not transient server conditions.
>  Retrying them just repeats the same failure five times. The tenacity before_sleep_log
>  parameter logs a warning before each retry attempt so engineers can see in the log stream
>  how many retries happened before success, which is useful for identifying intermittently
>  flaky APIs. The reraise=True setting means if all five attempts fail, the original
>  exception propagates to the caller rather than being wrapped in a tenacity exception type.
>
>  
>
> Rate limiting used a token bucket approach with time.monotonic() for elapsed time
>  measurement. The token bucket concept is: tokens accumulate at a constant rate (one token
>  per 1 / rate_limit_rps seconds), and each request consumes one token. Before every HTTP
>  request, the client checks how much time has elapsed since the last request and sleeps for
>  the deficit if needed. I used time.monotonic() specifically rather than time.time()
>  because time.time() can go backwards when the system clock is adjusted by NTP
>  synchronization. time.monotonic() is a counter guaranteed never to decrease -- essential
>  for elapsed time measurement in timing-sensitive code.
>
>  
>
> For the HTTP session itself I used requests.Session rather than the top-level
>  requests.get() convenience function. A Session object maintains TCP connections via
>  HTTP keep-alive -- when you make a second request to the same host, it reuses the existing
>  TCP connection from a pool rather than performing a new TCP handshake. For an extract job
>  making hundreds of sequential API calls to the same host, this connection pooling provides
>  meaningful throughput improvement. The Session also persists headers across calls, so the
>  Authorization header is set once at initialization and sent on every request automatically.
>
>  
>
> Pagination was implemented as a Python generator method that yields one page of records at
>  a time. The caller never interacts with page numbers or cursors -- they iterate over the
>  generator and receive one list of records per iteration, stopping when the generator is
>  exhausted. Internally the method handles both offset-based pagination (where you pass
>  ?page=N) and cursor-based pagination (where the API returns a next_page_token or
>  next_cursor value to include in the next request). Cursor-based pagination is preferable
>  when available because it is stable under concurrent inserts -- with offset pagination, if
>  records are inserted into the source database while you are paginating, some records shift
>  to a different page number and you get duplicates or gaps. A cursor points to a position in
>  an ordered sequence that remains stable regardless of inserts.
>
>  
>
> The generator pattern for pagination is elegant for a specific reason: memory usage stays
>  flat regardless of total record count. A client consuming the generator only holds one page
>  in memory at a time. If a downstream error occurs after fetching 200 pages, the generator
>  stops there -- it never fetched the remaining 800 pages it would have needed to had you
>  built a "fetch all then return" function.
>
>  
>
> Result
>
>  
>
> Zero manual restarts of API extract jobs due to transient network failures after deployment.
>  Rate-limited APIs were throttled transparently with no special handling by callers. Adding a
>  new API integration: configure the client with the base URL, API key, and rate limit, then
>  call paginate() in a for loop. The entire integration was one small subclass with
>  source-specific field mapping.
>
>   
>
> #### Technical Concept Breakdown 
>
>    
>
>   | Concept  | What It Is  | Why It Matters in Your Context 
>
>    
>
>   | Exponential backoff  | After each failure, wait an exponentially increasing interval before retrying: 2s, 4s, 8s, 16s... capped at a maximum.  | Gives a struggling API server time to recover. Avoids hammering it with rapid retries that make the overload worse. 
>
>  
>
>   | Jitter  | Adding randomness to backoff delays.  | If 1000 clients all back off for exactly 2 seconds after a server overload, they all retry simultaneously -- the thundering herd problem. Jitter spreads retries across time. 
>
>  
>
>   | tenacity  | Python retry library with composable decorator-based retry strategies.  | More expressive than hand-rolled loops. Handles logging, max attempts, wait strategies, exception type filtering cleanly. 
>
>  
>
>   | retry_if_exception_type  | Tenacity parameter specifying which exception types should trigger a retry.  | Critical: only retry transient errors (Timeout, ConnectionError). Never retry programming errors (ValueError, KeyError) -- that just repeats the failure. 
>
>  
>
>   | requests.Session  | Maintains TCP connections, cookies, and headers across multiple requests to the same host.  | HTTP keep-alive / connection pooling. Sequential API calls in a loop are significantly faster when connections are reused. 
>
>  
>
>   | Token bucket  | Rate limiting algorithm: tokens accumulate at a constant rate; each request consumes one token. Sleep if the bucket is empty.  | Enforces average request rate while allowing short bursts up to the bucket capacity. Simple and effective for REST API throttling. 
>
>  
>
>   | time.monotonic()  | A monotonically increasing counter that never goes backwards.  | Use for elapsed time measurement. time.time() can go backwards on NTP clock adjustments, which would break throttling logic. 
>
>  
>
>   | Cursor-based pagination  | API returns a cursor token pointing to the next page's position in an ordered sequence.  | Stable under concurrent inserts. Offset pagination (?page=3) skips or duplicates records if rows are inserted between page fetches. 
>
>  
>
>   | Generator for pagination  | yield-based method that produces one page of records per iteration, lazily fetching pages on demand.  | Memory stays flat regardless of total pages. Short circuits naturally if downstream processing stops early. 
>
>  
>
>   | raise_for_status()  | requests method that raises HTTPError for 4xx and 5xx status codes.  | Forces explicit error handling. Without it, a 500 response silently returns a Response object and you process an error body as if it were valid data. 
>
>     
>
> #### How to Say It in the Interview 
>
>  
>
> "My API client at Samay used tenacity for retry -- exponential backoff starting at 2
>  seconds, capped at 60, and critically, only retrying on transient network exceptions:
>  Timeout and ConnectionError. I explicitly excluded retrying on ValueError or KeyError
>  because those are programming bugs, not transient server conditions -- retrying them just
>  repeats the failure five times. Rate limiting was a simple token bucket using
>  time.monotonic() -- I specifically used monotonic rather than time.time() because
>  monotonic cannot go backwards on NTP clock adjustments. Pagination is a generator method
>  that yields one page at a time -- the caller iterates over it in a for loop without ever
>  thinking about page tokens or cursors. I preferred cursor-based pagination over offset-based
>  wherever the API offered it because cursors are stable under concurrent inserts, whereas
>  offset pagination can give you duplicates or gaps if records are being inserted into the
>  source while you're paginating."
>
>   
>
> #### Likely Follow-up Questions 
>
>  
>
> "What is the thundering herd problem?"
>  When many clients all fail at the same time (because a server went down), they all back off
>  for the same fixed interval, then all retry simultaneously, which recreates the exact load
>  spike that caused the failure. Adding jitter -- a small random offset to each client's
>  backoff interval -- spreads retries across a time window instead of concentrating them at
>  a single moment. The server recovers gradually rather than being hit with another spike.
>
>  
>
> "Why is cursor pagination better than offset pagination?"
>  With offset pagination you say "give me records 200-300." If another process inserts 5 records
>  before record 200 while you're paginating, your next request for records 200-300 shifts and
>  you get duplicates or miss records. A cursor encodes a position in an ordered sequence -- the
>  API says "the next page starts after this specific record." Inserts before that position don't
>  affect the cursor's validity.
>
>   
>
> ### Python Story 4 -- Testing Data Pipelines: pytest, Fixtures, Mocking 
>
>   
>
> The JD asks for automated testing frameworks. This is where you show you write testable,
>  professionally structured Python -- not just scripts.
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>
>  
>
> At Samay, pipeline code had no automated tests. Bugs were discovered when analysts reported
>  wrong numbers in compliance dashboards, sometimes days after a bad change merged. In
>  financial compliance the cost is severe -- an incorrect aggregation in a trade surveillance
>  pipeline could mean incorrectly filed regulatory reports and potential fines. I needed to
>  build a testing culture and framework that made catching bugs the CI system's job before
>  any code reached production.
>
>  
>
> Task
>
>  
>
> Build a pytest-based testing framework that could meaningfully test: pure Python
>  transformation logic, PySpark DataFrames, API client behavior against mocked HTTP responses,
>  and database write correctness.
>
>  
>
> Action -- The design decisions
>
>  
>
> The testing framework was built on pytest rather than the standard library's unittest
>  because pytest's fixture system and parametrize decorator are significantly more ergonomic.
>  The central organization mechanism is conftest.py -- a special file that pytest
>  auto-discovers and uses to define shared fixtures available to all tests in the directory
>  tree below it.
>
>  
>
> The most expensive resource in PySpark tests is the SparkSession itself -- starting a
>  SparkSession locally takes 3 to 5 seconds. Using @pytest.fixture(scope="session") means
>  the fixture is created once for the entire test run and shared across all tests. If I had
>  used the default scope="function", pytest would start and stop a new SparkSession for
>  every individual test -- a 100-test suite would spend 5 to 8 minutes just on SparkSession
>  startup. The session-scoped SparkSession is configured with local[2] as the master, which
>  runs Spark in-process using 2 local CPU threads -- no cluster needed, tests run in seconds.
>  The shuffle partitions are set to 2 rather than the default 200, which reduces unnecessary
>  overhead for the tiny test DataFrames.
>
>  
>
> For individual test DataFrames I used function scope (the default), meaning each test gets
>  a fresh DataFrame. This is test isolation -- tests that modify shared state can cause
>  order-dependent failures, where a test passes when run alone but fails when run after another
>  test that left shared state dirty. With function-scoped fixtures, there is no shared mutable
>  state between tests.
>
>  
>
> For testing API clients against HTTP responses, I used unittest.mock.patch.object to
>  replace the internal _get method with a mock that returns controlled responses. The
>  side_effect parameter accepts a list of values that the mock returns in sequence on
>  successive calls -- so I could simulate "first call returns page 1, second call returns page 2,
>  third call returns an empty page" without making any real HTTP requests. Tests are
>  deterministic (same inputs always produce same outputs), fast (no network round trips), and
>  cover exact edge cases including the empty-page termination condition. The patch.object
>  call is a context manager -- the mock is only active within the with block and the real
>  method is automatically restored when the block exits.
>
>  
>
> pyspark.testing.assertDataFrameEqual was the right tool for DataFrame assertions rather
>  than collecting rows and comparing manually. It handles two things that naive comparison
>  would miss: row ordering (Spark's distributed execution does not guarantee order without an
>  explicit orderBy) and floating-point precision (slight differences in floating-point
>  arithmetic should not fail tests). It also gives a readable diff when schemas or data
>  disagree.
>
>  
>
> @pytest.mark.parametrize was critical for the IP classification tests. I had one test
>  function with 8 input cases: a private IP, a public IP, a loopback address, a null input,
>  an empty string, an IP with an invalid octet, and two edge cases from the RFC ranges. Without
>  parametrize I would have written 8 nearly identical test functions. With parametrize
>  there is one function and a table of inputs and expected outputs. When a new edge case is
>  found in production, adding it to the parametrize list takes one line.
>
>  
>
> The most valuable test that came out of this process was a pagination edge case: the API
>  could return an empty-string next_page_token ("") when pagination was complete, rather
>  than None. In Python, an empty string is falsy -- if not token: break would correctly
>  stop on None but ALSO stop on "". However, "" can also be a valid cursor value in some
>  APIs -- if the logic was if token: the empty string would not be treated as "end of
>  pagination." The parametrize test with an explicit "" case caught this before it ever
>  hit a real API.
>
>  
>
> Result
>
>  
>
> Test suite caught 3 bugs before merge in its first two weeks: the null-handling crash in IP
>  classification, the empty-string pagination edge case, and an off-by-one in a date range
>  filter that was excluding the first day of each reporting period. All three were caught in
>  CI as failed PRs, none reached production.
>
>   
>
> #### Technical Concept Breakdown 
>
>    
>
>   | Concept  | What It Is  | Why It Matters in Your Context 
>
>    
>
>   | pytest  | Python testing framework. Auto-discovers and runs test_ prefixed functions. Fixture injection and parametrize are cleaner than unittest.  | The standard for modern Python projects. Fixture system makes test setup composable and reusable. 
>
>  
>
>   | @pytest.fixture  | A function that sets up test dependencies and injects them into test functions by parameter name.  | Reusable, scoped setup without inheritance hierarchies. Define once, use in any test that names it as a parameter. 
>
>  
>
>   | scope="session"  | Fixture created once per test run, shared across all tests.  | For expensive resources (SparkSession, DB connections). Avoiding per-test startup is the difference between a 2-minute and 30-minute test suite. 
>
>  
>
>   | scope="function"  | Fixture recreated for each test (the default).  | Test isolation. Prevents tests from sharing mutable state that causes order-dependent failures. 
>
>  
>
>   | conftest.py  | Special pytest file. Fixtures defined here are auto-discovered and available to all tests in the directory tree below.  | Single place to define shared resources like SparkSession, DB connections, sample data factories. 
>
>  
>
>   | pyspark.testing.assertDataFrameEqual  | Checks schema and data equality between two DataFrames, handling row ordering and floating-point differences.  | Spark does not guarantee row order in distributed execution. Naive comparison fails on correct output that happens to be in a different order. 
>
>  
>
>   | unittest.mock.patch.object  | Replaces a specific method on an object with a MagicMock for the duration of a with block. Restores the original on exit.  | Isolate code from external dependencies (HTTP, database, file system). Tests are fast, deterministic, and don't require live infrastructure. 
>
>  
>
>   | side_effect=[list]  | Mock parameter: each successive call to the mock returns the next value from the list.  | Simulate sequences of API responses without a real server. "Page 1 returns X, page 2 returns Y, page 3 returns empty." 
>
>  
>
>   | @pytest.mark.parametrize  | Runs one test function with multiple input/expected pairs as separate test cases.  | One function covers all edge cases. Adding a new edge case requires one line in the parameter table, not a new test function. 
>
>  
>
>   | Test isolation  | Each test starts from a clean, independent state with no shared mutable objects.  | Order-dependent test failures (tests that pass alone but fail when run after other tests) are the hardest category of test bugs to diagnose. Isolation prevents them. 
>
>     
>
> #### How to Say It in the Interview 
>
>  
>
> "For testing PySpark I used a session-scoped SparkSession fixture -- Spark takes 3 to 5
>  seconds to start, so you create it once per test run and share it. If you use function scope
>  you'd spend most of your test run on SparkSession startup overhead. For API client tests I
>  used patch.object with side_effect -- I give the mock a list of responses in sequence,
>  so I can simulate 'page 1, page 2, empty page' without any real HTTP calls. The test that
>  found the most valuable bug used parametrize to test IP classification across 8 cases --
>  private IP, public IP, null, empty string, invalid octet. The empty-string case caught a
>  real bug: if not token: break stops on empty string as well as None. For a pagination
>  guard, stopping early on "" would truncate a legitimate multi-page extract silently."
>
>   
>
> #### Likely Follow-up Questions 
>
>  
>
> "What is test isolation and why does it matter?"
>  Test isolation means each test has its own independent state -- no test depends on the side
>  effects of a test that ran before it. Without isolation you get order-dependent failures:
>  the test passes when run alone but fails when run as part of the suite because a previous
>  test left shared state modified. These are the most difficult test failures to diagnose
>  because the bug appears in test B but the cause is in test A. Pytest's fixture system with
>  function scope enforces isolation by creating fresh state for each test.
>
>  
>
> "What is a mock and when would you use it?"
>  A mock is an object that replaces a real dependency with a controlled fake that records how
>  it was called and returns configurable values. Use mocks for: external dependencies that
>  would make tests slow (HTTP APIs, databases), non-deterministic dependencies (clocks, random
>  number generators), and dependencies that have side effects you don't want in tests (sending
>  emails, writing to production databases). The rule of thumb is to mock at the boundary of
>  your system -- replace the things your code calls, not the internals of your code itself.
>
>   
>
> ### Python Story 5 -- Dagster Python: Assets, Resources, Sensors 
>
>   
>
> Dagster is Python-native. Assets, resources, schedules, and sensors are all Python
>  functions. This shows you understand the programming model, not just the UI.
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>
>  
>
> At Epik the pipeline needed to be more than a cron job running a script. It needed: declarative
>  dependency tracking between data assets so Dagster could visualize and enforce lineage,
>  injectable resources so the same pipeline code could run against real Snowflake in
>  production and an in-memory fake in tests, proactive freshness monitoring with automatic
>  alerting when a Silver asset violated its 15-minute SLA, and event-driven triggering when
>  new files arrived in the ADLS Bronze container rather than fixed-schedule polling.
>
>  
>
> Task
>
>  
>
> Implement the medallion pipeline orchestration in Dagster using software-defined assets,
>  configurable resources, asset checks for data quality gating, and event-driven sensors.
>
>  
>
> Action -- The design decisions
>
>  
>
> Dagster's software-defined asset model is a direct implementation of Dependency Injection as
>  a first-class framework concept. A Dagster asset is a Python function decorated with @asset.
>  Its function parameters declare its dependencies -- both on data (upstream assets, injected as
>  their output types) and on infrastructure (resources, declared as ResourceParam[T] type
>  annotations). Dagster resolves these dependencies at runtime: it determines which upstream
>  assets to materialize first, then passes their outputs and the configured resource instances
>  into the function. The function itself contains pure business logic -- it does not manage
>  connections, does not handle retry, does not know which environment it is running in.
>
>  
>
> The ConfigurableResource base class from Dagster is a Pydantic model with an additional
>  method protocol for resource behavior. Declaring a resource as a ConfigurableResource
>  subclass means Dagster validates its configuration at launch time -- a missing required field
>  like account or database raises a validation error immediately when the pipeline starts,
>  not when the first asset function tries to use the resource mid-run. The production deployment
>  configuration file provides real Snowflake credentials. The test configuration provides a
>  mock resource with identical method signatures but no real connections -- it captures writes
>  into an in-memory dictionary that tests can assert against.
>
>  
>
> This is the practical power of Dependency Injection in the context of data pipelines: the
>  silver_security_events asset function is identical in production and test. The environment
>  changes via configuration, not via code branches. No if os.environ['ENV'] == 'test'
>  conditionals scattered through business logic.
>
>  
>
> Asset checks address a recurring problem in data engineering: transformation logic that
>  successfully runs but produces incorrect output. A pipeline might complete without raising
>  any exception while silently writing a DataFrame where 20% of event_id values are null
>  because of an upstream join issue. Without a check, this bad data propagates through to Gold
>  and into dashboards. An @asset_check is a Python function that receives the asset's output
>  and returns an AssetCheckResult with a passed boolean and optional metadata. The
>  blocking=True parameter is the critical configuration: when set, a failed check prevents
>  any downstream assets from materializing. The bad data is contained at the failing asset --
>  it cannot propagate downstream automatically.
>
>  
>
> Sensors implement event-driven pipeline triggering. A @sensor is a Python function that
>  Dagster calls on a configurable polling interval. It can yield RunRequest objects to
>  trigger pipeline runs, or yield nothing if there is no new work to do. The run_key
>  parameter on RunRequest is the idempotency mechanism -- Dagster maintains a record of
>  which run_key values have already triggered runs, and will not submit a duplicate run for
>  the same run_key. This means the sensor can poll every 60 seconds checking for new files
>  in ADLS, and even if it detects the same file multiple times across successive polls, it will
>  only trigger one pipeline run for that file. The sensor uses context.cursor to track where
>  the last successful check ended -- typically the timestamp of the most recently processed
>  file -- and updates the cursor after yielding all new run requests.
>
>  
>
> FreshnessPolicy is declared directly on an asset and specifies the maximum acceptable lag
>  between when the asset should have been materialized and when it actually was. Dagster
>  computes this continuously and surfaces violations in the UI and can push them to alerting
>  systems. This is proactive monitoring -- rather than waiting for an analyst to notice a stale
>  dashboard at 9 AM and file a ticket, the system alerts the data engineering team at 3 AM
>  when the lag first exceeds 15 minutes.
>
>  
>
> Result
>
>  
>
> Pipeline orchestration expressed entirely as Python functions with explicit dependency
>  declarations, testable via resource substitution, with data quality gates that automatically
>  blocked downstream materialization on bad data. The sensor-driven architecture reduced the
>  average latency from file landing in Bronze to Silver completion from 45 minutes (fixed
>  Databricks cluster startup + schedule wait) to under 10 minutes (serverless + event trigger).
>
>   
>
> #### Technical Concept Breakdown 
>
>    
>
>   | Concept  | What It Is  | Why It Matters in Your Context 
>
>    
>
>   | Dependency Injection  | Passing dependencies (DB connections, API clients) into functions via parameters rather than constructing them inside.  | Core software engineering principle enabling testability. Swap real dependencies for test fakes via configuration, not code changes. 
>
>  
>
>   | @asset decorator  | Marks a Python function as a Dagster software-defined asset. The function's return value is the asset's materialization. Parameters declare dependencies.  | Declarative DAG construction. Dagster builds the dependency graph from function signatures rather than requiring explicit wiring code. 
>
>  
>
>   | ConfigurableResource  | Dagster base class (a Pydantic model) for injectable, type-safe resources with configuration schema.  | Pydantic validation at launch time. Swappable via configuration between environments. 
>
>  
>
>   | ResourceParam[T]  | Type annotation on an asset function parameter telling Dagster to inject a resource of type T.  | Zero-boilerplate resource injection. Dagster resolves and provides the right configured instance. 
>
>  
>
>   | @asset_check  | Decorator marking a function as a data quality check for a specific asset. Returns AssetCheckResult.  | First-class data quality in the Dagster asset graph. Visible in UI, alertable, and optionally blocking. 
>
>  
>
>   | blocking=True  | Asset check option: a failed check prevents all downstream assets from materializing.  | Hard data quality gate. Bad data is contained at the failing asset rather than propagating automatically through the pipeline. 
>
>  
>
>   | @sensor  | Python function polled by Dagster on a configurable interval. Yields RunRequest objects to trigger runs.  | Event-driven orchestration. Trigger runs based on file arrivals, API events, or any arbitrary Python condition. 
>
>  
>
>   | run_key  | Unique idempotency token for a RunRequest. Dagster will not submit duplicate runs with the same run_key.  | Sensors can poll frequently without launching duplicate pipeline runs for the same input file. 
>
>  
>
>   | FreshnessPolicy  | Policy on an asset declaring maximum acceptable lag before Dagster flags the asset as stale.  | Proactive SLA monitoring. System alerts when data freshness is violated, before analysts report stale dashboards. 
>
>  
>
>   | context.cursor  | Sensor context field for storing the sensor's last-processed position between polls.  | State persistence across sensor polls. Enables "check for files newer than the last run's timestamp." 
>
>     
>
> #### How to Say It in the Interview 
>
>  
>
> "In Dagster, the key Python design insight is that assets are pure functions: their
>  parameters declare their dependencies -- both upstream asset outputs and injectable resources
>  -- and Dagster resolves everything at runtime. The function itself contains only business
>  logic. This makes every asset function unit-testable by providing mock resources in the test
>  configuration without changing any code in the function. The blocking=True on asset checks
>  was important for us -- without it a check failure is just a warning in the UI. With it,
>  downstream assets literally cannot materialize if the upstream check fails. For event-driven
>  triggering I wrote a sensor with run_key set to the file path -- run_key is the
>  idempotency token, so even if the sensor polls the same file multiple times across successive
>  60-second intervals, Dagster only submits one run for it."
>
>   
>
> #### Likely Follow-up Questions 
>
>  
>
> "What is dependency injection and why does it help with testing?"
>  Dependency injection means that a function or class receives its dependencies as parameters
>  rather than constructing them internally. A function that constructs its own database
>  connection internally is hard to test because you can't control what connection it gets. A
>  function that receives a connection as a parameter can be tested by passing a fake connection
>  that records what was written to it. In Dagster, the resource system implements dependency
>  injection at the framework level -- you never write conn = Snowflake.connect() inside an
>  asset function, so tests can provide InMemoryWriter and production provides the real
>  SnowflakeWriter via configuration.
>
>  
>
> "What is the difference between a sensor and a schedule in Dagster?"
>  A schedule triggers runs at fixed time intervals -- every hour, every day at midnight.
>  A sensor triggers runs based on a condition -- a file arriving, an API returning new data,
>  an upstream asset completing with a specific metadata value. Sensors are event-driven;
>  schedules are time-driven. For our use case, a schedule would mean waiting up to 60 minutes
>  for the next scheduled run after a file landed. A sensor detected the file and triggered
>  within 60 seconds of landing.
>
>   
>
> ### Python Concepts Quick Reference 
>
>   
>
> Fundamentals that come up in follow-up questions -- be ready to discuss any of these fluently.
>
>    
>
> #### Core Patterns 
>
>  
>
> Decorators
>  A decorator is a function that takes a function as input and returns a modified function.
>  The @decorator syntax is shorthand for func = decorator(func). Common use cases in
>  data engineering: @retry for automatic retry logic, @lru_cache for memoization,
>  @pytest.fixture for test setup, @asset for Dagster asset declaration.
>
>  
>
> Generators and yield
>  A generator function uses yield to produce values lazily. When the caller requests the
>  next value, execution resumes from the yield statement. Memory usage stays flat because
>  the generator only holds the current item in memory. The yield from syntax delegates to a
>  sub-generator, chaining lazy sequences without materializing intermediate collections.
>
>  
>
> Context Managers and with
>  The with statement ensures cleanup code always runs by calling __exit__ (or the
>  @contextmanager function's finally block) when the block exits, whether normally or via
>  exception. Use for any resource that needs cleanup: database connections, file handles,
>  temporary directories, transaction blocks.
>
>  
>
> functools.lru_cache
>  @lru_cache(maxsize=128) memoizes a function's return values indexed by its arguments.
>  On repeated calls with the same arguments, it returns the cached result without re-executing
>  the function. LRU = Least Recently Used eviction when the cache is full. Use for: expensive
>  database lookups called repeatedly with the same tenant or dimension keys.
>
>  
>
> Custom exceptions
>  Define a base exception class for your domain (class PipelineError(Exception)) with
>  specific subclasses (ExtractionError, ValidationError). This lets callers write
>  except ExtractionError to handle extraction failures specifically while letting other
>  exceptions propagate. Avoid catching broad Exception -- it swallows bugs silently.
>
>  
>
> asyncio for I/O concurrency
>  async def functions are coroutines. await suspends the coroutine while waiting for I/O,
>  allowing the event loop to run other coroutines. asyncio.gather() runs multiple coroutines
>  concurrently. For 15 parallel API calls: sequential = 15 x 2s = 30s. Async concurrent = ~2s
>  total. The GIL is not a problem here because await yields the thread voluntarily -- there
>  is no CPU contention, just I/O waiting.
>
>   
>
> #### Python Fundamentals Answer Bank 
>
>    
>
>   | Question  | Precise Answer 
>
>    
>
>   | What is the GIL?  | Global Interpreter Lock. Prevents multiple Python threads from executing bytecode simultaneously. Not a bottleneck for I/O-bound work (threads yield at I/O). Bottleneck for CPU-bound parallelism -- use multiprocessing instead. 
>
>  
>
>   | is vs ==  | is checks object identity (same memory address). == checks value equality. x is None is correct; x == None works but is not idiomatic -- None is a singleton so identity check is appropriate. 
>
>  
>
>   | Mutable default bug  | def f(tags=[]) creates one list object at function definition time, shared across all calls. Fix: def f(tags=None): tags = tags or []. In dataclasses: field(default_factory=list). 
>
>  
>
>   | Shallow vs deep copy  | copy.copy() copies the container but shares references to nested objects. copy.deepcopy() recursively copies everything. Matters when nested mutable objects (lists of lists, dicts of dicts) need to be independent copies. 
>
>  
>
>   | *args and **kwargs  | *args captures extra positional arguments as a tuple. **kwargs captures extra keyword arguments as a dict. Use in wrapper functions that need to forward arbitrary arguments to the wrapped function. 
>
>  
>
>   | zip(strict=True)  | Raises ValueError if the two iterables have different lengths. Without strict=True, zip silently truncates to the shorter iterable -- this can silently lose data when pairing two lists that should have the same length. 
>
>  
>
>   | __repr__ vs __str__  | __repr__ is the unambiguous developer representation -- ideally eval(repr(obj)) == obj. __str__ is the human-readable representation. print(obj) calls str. If only one is defined, repr is used as fallback. 
>
>  
>
>   | @property  | Makes a method callable without parentheses. Used for computed attributes and to add validation to attribute access via getters and setters without changing the calling interface. 
>
>  
>
>   | collections.defaultdict  | defaultdict(list) automatically creates an empty list on first access of any missing key. Eliminates if key not in d: d[key] = [] boilerplate in grouping logic. 
>
>  
>
>   | itertools.chain  | chain(list_a, list_b) iterates over both sequences as one without concatenating them into a new list. Memory-efficient for chaining large iterables. 
>
>  
>
>   | Pickling  | Python's object serialization protocol (pickle.dumps/pickle.loads). Used by multiprocessing for inter-process communication and by PySpark for row-by-row UDF serialization. The reason regular Python UDFs in Spark are slow. 
>
>  
>
>   | __slots__  | Replacing the per-instance __dict__ with a fixed-size attribute array. Memory benefit: 30-50% reduction for classes with millions of instances. Tradeoff: can no longer add arbitrary attributes dynamically. 
>
>     
>
> #### Pandas Optimization Quick Reference 
>
>    
>
>   | Pattern  | Why It Helps 
>
>    
>
>   | df["col"].astype("category")  | Low-cardinality string columns (status codes, event types) stored as integer indices. 5-10x memory reduction. 
>
>  
>
>   | pd.read_csv(path, chunksize=N)  | Process CSV files larger than RAM by iterating N-row chunks. Never loads the full file. 
>
>  
>
>   | df.query("severity > 5 and tenant == @tid")  | Readable boolean filtering. The @var syntax references Python local variables inside the query string. 
>
>  
>
>   | df.eval("roi = (revenue - cost) / cost")  | Vectorized multi-column expression evaluated in one pass. Avoids creating intermediate Python objects for each operation. 
>
>  
>
>   | Avoid df.iterrows()  | Row-by-row Python iteration over a DataFrame is 100 to 1000x slower than vectorized column operations. Use .apply(), .map(), or direct column arithmetic. 
>
>  
>
>   | pd.to_datetime(col, utc=True)  | Always normalize timestamps to UTC on ingest. Timezone-naive timestamps silently produce wrong results in time-based window calculations. 
>
>     
>
> ## CHALLENGES, FAILURES & DEBUGGING STORIES 
>
>   
>
> These are the questions that separate senior engineers from junior ones: "Tell me about
>  a time you failed," "What's the hardest production bug you've debugged?", "Tell me about
>  a mistake that had business impact." Answer these with specificity and ownership.
>  The formula: what broke, why it was hard to find, what you changed, what you learned.
>
>    
>
> ### Failure 1 -- Silent Data Multiplication from a PySpark Join (Epik Solutions) 
>
>   
>
> Type: Silent data corruption / wrong join semantics
>  Impact: Security event counts inflated 3x in compliance dashboards for 6 days before detection
>
>    
>
> #### What Happened 
>
>  
>
> The Bronze-to-Silver pipeline at Epik joined raw security events against a tenant metadata
>  table to enrich each event with its tenant's compliance tier and regulatory region. This join
>  had been running in production for two weeks without any obvious error. No exceptions, no
>  failed pipeline runs, clean Dagster materialization history. The pipeline looked healthy.
>
>  
>
> Six days in, an analyst raised a ticket: event counts in the Acuity compliance dashboards
>  were approximately three times higher than the counts the client's own SIEM system showed
>  for the same time windows. The discrepancy was noticed only because the client had a
>  cross-system sanity check in their weekly review process.
>
>  
>
> #### Why It Was Hard to Find 
>
>  
>
> The pipeline's monitoring only checked for job completion and schema compliance -- it did not
>  verify that output row counts were in the expected range relative to input row counts. A
>  successful pipeline run with no schema violations and no exceptions looked identical to a
>  correct one. The inflation was not 2x or 10x (which would have been obvious) but roughly
>  3x, which matched the fact that three different data delivery methods had been configured
>  per tenant in the metadata table -- three rows in the metadata table per tenant, one per
>  delivery channel.
>
>  
>
> The join I had written was on tenant_id alone. Since the metadata table had three rows per
>  tenant (one for each channel), every event for that tenant joined to all three, tripling the
>  count. This is a classic join fan-out from an undetected one-to-many relationship. The
>  correct join key was the composite (tenant_id, primary_channel) -- only one row per tenant
>  per primary channel. I had looked at the metadata table's documented schema and assumed
>  tenant_id was unique, which it was in the original version but was no longer true after a
>  schema change two weeks before the pipeline launched.
>
>  
>
> #### What I Did 
>
>  
>
> The debugging process had three stages. First I verified the symptom by comparing the Silver
>  table row count for a specific tenant and date window against the raw event count from the
>  Bronze table -- 3.1x ratio confirmed for every tenant. Second I ran the same join logic
>  manually against a 1-day sample and computed the GROUP BY tenant_id, COUNT(*) on the
>  result versus the same aggregation on the Bronze input. The ratio appeared in the first
>  query. Third I examined the metadata table and found three rows per tenant where I had
>  assumed one.
>
>  
>
> The immediate fix was to correct the join predicate to include the composite key and backfill
>  the affected Silver partitions by reprocessing the prior six days through Databricks.
>
>  
>
> The preventive fix was adding a @asset_check with blocking=True that computed the ratio
>  of Silver row count to Bronze row count for the same event date and failed the check if the
>  ratio exceeded 1.1 (a 10% tolerance for legitimate deduplication). This check would have
>  caught the issue on the first pipeline run.
>
>  
>
> #### What I Learned 
>
>  
>
> Row count monitoring at each pipeline stage is not optional for production data pipelines.
>  Schema validation (is the schema correct?) is table stakes. Count validation (is the output
>  count in an expected range relative to the input?) is what actually catches semantic errors
>  like fan-out joins. The most dangerous failures are the ones that produce no exceptions and
>  look healthy in all the places you are monitoring.
>
>  
>
> For join correctness specifically: never assume uniqueness of a join key without
>  explicitly verifying it with a COUNT(DISTINCT key) = COUNT(*) check, or by reading the
>  source system's data dictionary rather than inferring from the schema. Schema change
>  notifications should trigger a review of all joins on that table.
>
>   
>
> #### How to Say It in the Interview 
>
>  
>
> "We had a silent data multiplication bug in production at Epik that inflated security event
>  counts by 3x for six days before an analyst caught it. The pipeline ran without errors,
>  passed schema validation, and had clean job completion history -- there was nothing in our
>  monitoring that would flag it. The root cause was a join fan-out: I joined events to a
>  tenant metadata table on tenant_id alone, assuming it was unique, but a schema change two
>  weeks earlier had added three rows per tenant for different delivery channels. Every event
>  was joining to all three rows. The fix was correcting the join key to the composite and
>  backfilling six days. The preventive fix was an asset check that compared Silver-to-Bronze
>  row count ratios and blocked materialization if the ratio exceeded 1.1. The lesson for me
>  was that count validation is as important as schema validation -- a pipeline that runs
>  successfully but produces wrong counts is worse than a pipeline that fails, because you
>  don't know the data is wrong."
>
>   
>
> #### Likely Follow-up Questions 
>
>  
>
> "How would you design a monitoring system to prevent this class of issue?"
>  Three layers: First, row count ratio checks at each pipeline stage -- Silver count should be
>  within an expected range of Bronze count. An asset check or Great Expectations expectation
>  that asserts output_count between 0.9 * input_count and 1.1 * input_count catches fan-out
>  and silent deduplication. Second, business-level metric monitoring -- the end metric (total
>  events per tenant per day) should be within expected bounds based on historical distributions.
>  Statistical anomaly detection on these metrics catches issues that count-ratio checks miss.
>  Third, cross-system reconciliation for high-stakes pipelines: compare counts between your
>  pipeline's output and the source system's own counts for the same time window.
>
>   
>
> ### Failure 2 -- Pagination Truncation Caused Missing Compliance Records (Samay Systems) 
>
>   
>
> Type: Silent data loss / subtle Python truthiness bug
>  Impact: 11 days of incomplete trade records for two clients -- caught during internal audit
>
>    
>
> #### What Happened 
>
>  
>
> At Samay, one of the regulatory API clients returned a next_page_token field in its
>  pagination response. When there were no more pages, the API was documented to return an
>  empty string for next_page_token. My pagination logic checked if not token: break to
>  stop pagination. In Python, an empty string is falsy -- not "" evaluates to True -- so
>  this condition correctly stopped on an empty string.
>
>  
>
> The problem emerged when the API was updated (without a changelog announcement) to return
>  next_page_token as a value of "0" rather than "" to indicate end of pagination. The
>  string "0" is truthy in Python. My code now treated "0" as a valid cursor and passed it
>  in the next request's parameters. The API, receiving next_page_token="0" as if starting
>  fresh, returned the first page again. The pagination looped on the last two pages indefinitely
>  until the pipeline hit its configured timeout, then terminated gracefully with the last
>  successful write -- which was partial.
>
>  
>
> #### Why It Was Hard to Find 
>
>  
>
> The pipeline ran to completion with no errors. It hit the timeout and exited cleanly because
>  the timeout handling wrote whatever had been extracted to Snowflake and returned success.
>  The extracted count was lower than expected but there was no alerting on absolute record
>  counts -- only on pipeline success or failure. The issue was discovered during an internal
>  audit comparing the Snowflake staging table against a re-extract from the source API.
>
>  
>
> The 11-day window meant there were 11 days of trade records that had been partially
>  extracted -- the first N pages of trades per day existed in Snowflake, the remaining pages
>  did not. Because the API returns trades in reverse chronological order, the missing records
>  were the oldest trades within each day, which were less likely to appear in recent queries.
>
>  
>
> #### What I Did 
>
>  
>
> The audit finding showed count discrepancies by day. I reproduced the issue by re-running
>  the extractor against a specific day's data with verbose logging enabled -- the log showed
>  the page token cycling: page 1 response contained token "0", the client sent page 2 with
>  cursor="0", the API returned page 1 again. The loop was visible in the logs immediately.
>
>  
>
> The fix was changing the termination condition from the falsy check to an explicit None
>  check: if token is None: break. This stops on None only and treats any other value --
>  including empty string or "0" -- as a valid cursor, letting the API's actual end-of-data
>  signal drive termination (the empty data array in the response body) rather than the token
>  value.
>
>  
>
> The backfill required identifying the affected date ranges per client, re-extracting from
>  the API for those dates, and using a merge strategy (not an overwrite) to fill in the missing
>  records without disturbing the records that had been correctly extracted.
>
>  
>
> The preventive fix was adding a configurable maximum page count to the extractor, after which
>  it would log a warning and raise an exception rather than continuing silently. An 11,000-page
>  extract would be so far outside the historical norm for these APIs that an exception would
>  have been the right response, triggering manual investigation rather than a timed-out partial
>  write.
>
>  
>
> #### What I Learned 
>
>  
>
> Explicit None checks (if token is None) are always safer than falsy checks (if not token)
>  for sentinel values in protocol behavior. An empty string and None are both falsy in
>  Python but mean semantically different things -- None usually means "absent/not provided"
>  while "" means "explicitly empty string." The distinction matters when you are handling
>  API response fields where the API contract can change the sentinel value format.
>
>  
>
> The broader lesson is about silent success: a job that completes within its timeout and
>  writes some data looks successful in every operational metric. Count validation against
>  source-side record counts is the only way to detect partial extracts.
>
>   
>
> #### How to Say It in the Interview 
>
>  
>
> "We had a pagination bug at Samay that caused 11 days of incomplete compliance data for two
>  clients. The root cause was a Python truthiness issue: my pagination loop used if not token: break to stop when the API indicated end of pages. The API returned an empty string for
>  end-of-pagination, which is falsy, so it worked correctly. Then the API updated its contract
>  to return the string '0' instead of empty string -- '0' is truthy in Python, so my code
>  treated it as a valid cursor and looped forever until the timeout. The pipeline completed
>  cleanly every time, just with partial data, because the timeout handler wrote whatever it had.
>  The fix was changing to if token is None: break -- explicit None check instead of a falsy
>  check. The lesson that stuck with me was the difference between not token and token is None:
>  they look similar but behave differently for any falsy non-None value like empty string,
>  zero, or False. For sentinel values in protocol contracts, always use explicit identity
>  checks."
>
>   
>
> ### Failure 3 -- dbt Incremental Model Missing Soft-Deleted Records (Samay Systems) 
>
>   
>
> Type: Architectural design error / incremental strategy mismatch
>  Impact: Stale data in Silver for 3 months -- compliance records that had been revoked at
>  source continued appearing as active in Snowflake
>
>    
>
> #### What Happened 
>
>  
>
> At Samay, a dbt incremental model loaded compliance records from a staging Snowflake table
>  into the Silver layer. The incremental strategy used an updated_at timestamp filter: on
>  each run, the model queried for records where updated_at was greater than the last run's
>  maximum updated_at and merged them into the Silver table. This is a standard incremental
>  pattern and it worked correctly for new records and updates.
>
>  
>
> What it did not handle was soft deletes. The source compliance system marked records as
>  deleted by setting a is_deleted flag to True -- but it did NOT update the updated_at
>  timestamp when doing so. From the incremental model's perspective, a soft-deleted record
>  was indistinguishable from a record that simply had not changed. It was never included in
>  the incremental load because its updated_at was old. The Silver table continued to show
>  these records as active compliance records.
>
>  
>
> #### Why It Was Hard to Find 
>
>  
>
> The issue had no observable failure. Pipeline ran daily, completed successfully, produced
>  no schema errors. The compliance records in question were valid records at the time they
>  were first loaded, so they passed all business validation rules. The only way to detect the
>  issue was to cross-reference Snowflake's Silver table count against the source system's
>  "active records" count -- and the source system had no obvious reporting interface that made
>  this comparison easy.
>
>  
>
> The issue surfaced three months in when a client noticed that two contractors who had been
>  removed from their compliance portal weeks earlier were still appearing in the Samay
>  compliance reporting dashboard. Manual investigation traced the discrepancy from the
>  dashboard to the Gold model to the Silver model to the incremental logic.
>
>  
>
> #### What I Did 
>
>  
>
> The first step was quantifying the damage: I compared the full set of record_id values
>  in the Silver table against the source system's active record list. The count showed 847
>  records in Silver that the source system considered deleted or inactive.
>
>  
>
> The fix required re-evaluating the incremental strategy. The updated_at-based approach
>  was fundamentally wrong for this source because the source system's soft-delete mechanism
>  didn't touch updated_at. I had two options: either request that the source system fix
>  its soft-delete logic to update updated_at (rejected -- would require changes to a
>  production compliance system we didn't own), or switch the dbt incremental model to a full
>  re-scan strategy with a merge predicate.
>
>  
>
> I switched the model from strategy: incremental to a daily full merge. The model now
>  reads all records from the staging table, compares them against the Silver table on record_id,
>  and applies the full change set: insert new records, update changed records, and mark any
>  records in Silver that are absent from the source scan as is_deleted=True with a deletion
>  timestamp. This is more expensive than an incremental load (a daily full scan of the staging
>  table rather than a filtered query) but guaranteed correctness for all change types.
>
>  
>
> The backfill deleted the 847 stale records from Silver with a deleted_at timestamp
>  matching the best estimate of when they were removed from source.
>
>  
>
> #### What I Learned 
>
>  
>
> The right incremental strategy depends entirely on how the source system signals changes.
>  The standard updated_at incremental approach assumes the source system is well-behaved:
>  every change -- including deletions -- updates the updated_at field. Many production
>  systems are not well-behaved. Before choosing an incremental strategy, the right question
>  is: "Does this source system update its modification timestamp for ALL types of changes,
>  including soft deletes?" If the answer is "I don't know," the safer default is a full merge
>  strategy with tombstone handling, even if it is more expensive.
>
>  
>
> The other lesson was about the gap between "pipeline succeeds" and "data is correct." A
>  pipeline that runs daily with no errors for three months can silently accumulate a growing
>  delta of wrong data if the incremental logic has a blind spot. Business-level reconciliation
>  checks -- total active record counts compared against source -- are the only reliable
>  detection for this class of issue.
>
>   
>
> #### How to Say It in the Interview 
>
>  
>
> "The hardest data correctness bug I dealt with at Samay was a dbt incremental model that was
>  silently missing soft-deleted compliance records for three months. The incremental strategy
>  used an updated_at filter to identify changed records -- completely standard. But the source
>  system's soft-delete process set an is_deleted flag without updating updated_at. From
>  the incremental model's perspective, those deleted records were unchanged and were never
>  re-processed. They stayed active in Snowflake while the source showed them as deleted. The
>  only reason we caught it was a client noticed two removed contractors still appearing in
>  our dashboards. The fix was switching from an updated_at incremental to a full daily
>  merge with tombstone handling -- more expensive, but the only correct approach for a source
>  system that doesn't update modification timestamps on soft deletes. The lesson: always
>  validate the source system's change-signaling behavior before choosing an incremental
>  strategy. Don't assume updated_at covers all change types."
>
>   
>
> ### Failure 4 -- PySpark Data Skew OOM Failure on Large Tenant (Epik Solutions) 
>
>   
>
> Type: Infrastructure failure / data distribution problem
>  Impact: Security event pipeline OOM-crashing for largest client, blocking Silver
>  materialization for 14 hours
>
>    
>
> #### What Happened 
>
>  
>
> At Epik, the Silver-to-Gold pipeline aggregated security events by tenant_id and event_type
>  to compute daily summary statistics. This pipeline ran without issues for three months while
>  clients were in onboarding. When the largest enterprise client (a financial services firm
>  with roughly 150x the event volume of any other client) reached full production traffic,
>  the Spark job started failing with executor OOM errors consistently.
>
>  
>
> The error message was ExecutorLostFailure (executor 3 exited caused by one of the running tasks) followed by java.lang.OutOfMemoryError: GC overhead limit exceeded. The job would
>  fail at the same stage every time: the window function computing rolling statistics within
>  each tenant_id partition.
>
>  
>
> #### Why It Was Hard to Find 
>
>  
>
> OOM errors in Spark are often misdiagnosed as infrastructure issues -- "we need bigger executors"
>  is the first instinct. I had initially gone down that path: submitted a request to increase
>  executor memory from 8GB to 16GB. The job still OOM'd, just slightly later. Doubling memory
>  again would have been expensive and still wrong.
>
>  
>
> The Spark UI told the real story. The "Tasks" tab for the failing stage showed 199 tasks
>  completing in under 2 seconds each, and one task running for 40 minutes with an input size
>  of 82GB. That one task was holding all of the largest client's event data because the
>  partitionBy("tenant_id") in the window function had placed all of their events in a single
>  Spark partition -- and that partition was assigned to one executor.
>
>  
>
> This is data skew: when your partition key has a highly unequal distribution (one tenant has
>  150x the rows of any other), partitioning by that key creates one enormous partition and
>  hundreds of tiny ones. The large partition overwhelms the executor handling it while the
>  others sit idle. Adding more executor memory treats the symptom but does not fix the problem.
>
>  
>
> #### What I Did 
>
>  
>
> The diagnostic was comparing task execution times and input sizes across the failing stage
>  in the Spark UI. Once data skew was confirmed as the cause, the fix was a salting strategy
>  on the partition key.
>
>  
>
> Salting works by appending a random number (the "salt") to the partition key, transforming
>  a skewed single-tenant partition into N evenly distributed partitions. For a COUNT or
>  SUM aggregation, you can safely salt, compute partial aggregations per salt bucket, and
>  then merge the partial results. For a window function that requires seeing all of a tenant's
>  events ordered by timestamp (as our rolling event rate calculation did), salting is
>  incompatible with a single window -- you cannot split a time-ordered window computation
>  across multiple partitions.
>
>  
>
> The right fix for the window function case was a two-phase approach: compute the initial
>  salted aggregations at a sub-tenant level (by tenant_id plus event_source_region, which
>  distributed the large tenant's data across 12 partitions), then compute the cross-region
>  totals in a second aggregation pass. This restructuring required separating the "per-region
>  rate" and "total-tenant rate" statistics into two models, but the data was actually more
>  granular and useful at the regional level for security analysis purposes.
>
>  
>
> #### What I Learned 
>
>  
>
> Increasing executor memory is the wrong first response to a Spark OOM in a data aggregation
>  pipeline. The right first step is examining the Spark UI for task time and input size
>  distribution across the failing stage. A task that takes 50x longer than its siblings or
>  processes 100x more data than its siblings is the diagnostic signature of data skew, and no
>  amount of additional memory fixes a distribution problem.
>
>  
>
> The broader lesson is about cardinality assumptions: a partition key that is balanced today
>  may become severely skewed when a single large customer onboards. Pipeline design should
>  include analysis of the worst-case key distribution, not just the average case.
>
>   
>
> #### How to Say It in the Interview 
>
>  
>
> "At Epik, our Silver-to-Gold pipeline started OOM-crashing after the largest enterprise
>  client went to full production. Initial instinct was to increase executor memory -- which
>  didn't fix it. The Spark UI told the real story: the Tasks view showed 199 tasks finishing
>  in 2 seconds each and one task running for 40 minutes with 82GB of input. Classic data skew:
>  partitionBy('tenant_id') put all of this client's events in one partition on one executor.
>  The fix was restructuring the window computation to partition by a more granular key --
>  tenant_id plus event_source_region -- which distributed the large tenant's data across
>  12 partitions instead of 1. The statistics became more granular (per-region rather than
>  per-tenant only) but also more useful for security analysis. The lesson: Spark OOM with a
>  skewed task time distribution is a data skew problem, not a memory problem. Look at task
>  input sizes in the Spark UI before touching any memory configuration."
>
>   
>
> #### Likely Follow-up Questions 
>
>  
>
> "How do you detect data skew before it causes failures?"
>  Three approaches: First, analyze key cardinality and distribution in the source data before
>  building the pipeline. A simple GROUP BY partition_key, COUNT(*) showing the top 10
>  groups by count reveals skew. Second, monitor Spark stage metrics in production -- the ratio
>  of max task duration to median task duration within a stage is the skew indicator. A ratio
>  above 5x warrants investigation. Third, instrument your pipeline with partition size logging:
>  compute the partition size distribution before any wide transformation and alert if the
>  max-to-median ratio exceeds a threshold.
>
>   
>
> ### Failure 5 -- Terraform State Drift Caused 6-Hour Pipeline Outage (Epik Solutions) 
>
>   
>
> Type: Infrastructure management failure / IaC drift
>  Impact: All Epik pipelines failing with cryptic permission errors for 6 hours on a Monday
>
>    
>
> #### What Happened 
>
>  
>
> At Epik, Azure infrastructure was managed with Terraform: Key Vault for secrets, Event Hubs
>  namespaces, Databricks workspaces, Storage accounts, and their associated RBAC and access
>  policy configurations. A Monday morning deployment ran successfully through CI/CD, and then
>  every pipeline started failing within minutes. The error messages were cryptic Azure SDK
>  exceptions about secret retrieval failures -- something along the lines of "The user, group,
>  or application does not have secrets get permission on key vault."
>
>  
>
> The pipelines had been working perfectly the previous Friday. No code changes had merged
>  over the weekend. The deployment that morning had not touched Key Vault configuration.
>
>  
>
> #### Why It Was Hard to Find 
>
>  
>
> The immediate suspicion was the Monday deployment -- but reviewing the Terraform plan that
>  had been applied showed no Key Vault changes. The plan had only touched Event Hubs consumer
>  group settings. This was correct and expected.
>
>  
>
> The problem was that a developer on the team had manually added their personal service
>  principal to the Key Vault access policy on Friday afternoon to debug a separate issue. They
>  forgot to remove it when they were done. Because Terraform's state file did not know about
>  this manual addition, when Terraform applied on Monday it compared its desired state
>  (no manual service principal in the access policy) against the live state (access policy
>  with both the correct managed identity AND the manual service principal), determined that
>  the difference was in scope, and removed the manual service principal as an "untracked
>  resource."
>
>  
>
> The problem was that in doing so, Terraform also reset the access policy block format, which
>  in an older version of the azurerm Terraform provider reset all access policies for the
>  vault to only those explicitly listed in the Terraform configuration -- and our Terraform
>  configuration was missing the Databricks managed identity that the pipelines used for secret
>  retrieval. The managed identity had been added to the Key Vault via the Azure portal six
>  months earlier (before Terraform managed this resource) and had never been codified into
>  the Terraform configuration.
>
>  
>
> #### What I Did 
>
>  
>
> The immediate fix was identifying the failing secret retrieval, locating the correct managed
>  identity for the Databricks pipeline service principal, and manually adding it back to the
>  Key Vault access policy via the Azure portal. Pipelines recovered within 10 minutes once
>  the permission was restored.
>
>  
>
> The root cause fix was a two-day effort to audit every manually-created Azure resource
>  against the Terraform state file and codify the discrepancies. The Key Vault access policy
>  was the obvious one, but the audit found three other resources that existed in Azure but not
>  in Terraform state -- a Network Security Group rule, a storage account lifecycle policy, and
>  a diagnostic settings configuration. All four were imported into the Terraform state using
>  terraform import and their corresponding resource blocks added to the configuration.
>
>  
>
> The process control fix was establishing a team rule: no manual portal changes to
>  Terraform-managed infrastructure. Any change that needs to be made in production must go
>  through a Terraform PR. For debugging scenarios requiring temporary access, changes must be
>  documented and either reverted immediately or codified in a PR within 24 hours.
>
>  
>
> We also added a terraform plan job to the CI pipeline that ran on a nightly schedule
>  against the live production environment and alerted if any non-empty plan was detected.
>  A non-empty plan against a production environment where no changes are expected means drift
>  has occurred -- either a manual change in Azure or a missing resource in Terraform state.
>
>  
>
> #### What I Learned 
>
>  
>
> IaC drift is an insidious class of problem because it accumulates silently. Individual manual
>  changes seem harmless in the moment -- adding temporary debug permissions, tweaking a
>  resource setting directly in the portal for speed. But each change widens the gap between
>  what Terraform thinks the infrastructure looks like and what it actually looks like. The next
>  Terraform apply becomes unpredictable because it reconciles the delta against what it
>  believes to be the desired state, and that reconciliation may remove or modify things you
>  didn't intend to touch.
>
>  
>
> The specific lesson about Terraform access policies: when Terraform manages a resource block
>  that has a list attribute (like access policies), it enforces the full list on apply -- any
>  member of the list not in the Terraform configuration is removed. This is not a bug, it is
>  correct idempotent behavior. The failure was our configuration not being complete.
>
>   
>
> #### How to Say It in the Interview 
>
>  
>
> "We had a 6-hour pipeline outage at Epik on a Monday morning caused by Terraform state
>  drift. The root chain was: a developer manually added a temporary service principal to a
>  Key Vault access policy on Friday for debugging and forgot to remove it. Monday's Terraform
>  apply saw the drift and reconciled it -- but the reconciliation reset the full access policy
>  list to only what was in Terraform state, which was missing the Databricks managed identity
>  that all our pipelines used for secret retrieval. The managed identity had been added via
>  the portal six months before Terraform managed that resource and had never been codified.
>  Everything failed with cryptic permission errors within minutes of the deploy. The fix was
>  re-adding the managed identity, then spending two days doing a full Terraform state audit
>  and importing all the manually-created resources. The process fix was adding a nightly
>  terraform plan against production: if the plan is non-empty when no changes are expected,
>  drift has occurred and someone gets paged. Manual portal changes to Terraform-managed
>  infrastructure became a team policy violation."
>
>   
>
> #### Likely Follow-up Questions 
>
>  
>
> "What is Terraform state drift and how do you prevent it?"
>  Terraform state drift occurs when the actual infrastructure diverges from what Terraform's
>  state file records -- typically from manual changes made outside of Terraform. On the next
>  apply, Terraform reconciles the delta between desired state (in configuration) and
>  recorded state (in the state file), which can result in unexpected modifications or
>  deletions of resources that exist in reality but not in state. Prevention: establish a
>  "Terraform-managed means hands off" policy for production resources, add nightly drift
>  detection plans in CI, use terraform import to codify existing resources before Terraform
>  takes ownership of them, and use resource locks in Azure to prevent accidental manual
>  modifications to critical infrastructure.
>
>   
>
> ### Failure 6 -- Debugging a Memory Leak in a Long-Running Python Ingestion Process (Zemoso) 
>
>   
>
> Type: Performance / resource management failure in production Python
>  Impact: Ingestion service restarting every 4-6 hours due to OOM, dropping events
>
>    
>
> #### What Happened 
>
>  
>
> At Zemoso, the LabOps platform ran a Python-based ingestion service that continuously
>  polled laboratory instrument APIs every 30 seconds to collect measurement data. The service
>  was deployed as a container. Within a week of deployment, the on-call team noticed the
>  container was restarting roughly every 4 to 6 hours -- the OOM killer was terminating it
>  when memory usage exceeded the container's limit.
>
>  
>
> The service was not doing anything that should accumulate memory. Each polling loop fetched
>  data from an API, transformed it into a DataFrame, wrote to PostgreSQL, and discarded the
>  DataFrame. At least, that was the design.
>
>  
>
> #### Why It Was Hard to Find 
>
>  
>
> The first thing I checked was the obvious: the DataFrames themselves. The polling loop was
>  using Pandas, and each cycle created a new DataFrame. I verified that the DataFrame reference
>  went out of scope at the end of each loop iteration and assumed Python's garbage collector
>  would reclaim the memory. This was correct -- DataFrames were not the leak.
>
>  
>
> The actual leak was in the logging configuration. The service used Python's standard
>  logging module. During initialization, a custom log handler had been added that stored
>  log records in an in-memory list (intended for a future "retrieve last N log messages via
>  API" feature that had never been implemented). This handler was appended to the root logger
>  with no maximum size on the in-memory list. Every log message from every library in the
>  process -- not just application logs but also library debug logs from requests, sqlalchemy,
>  and the PostgreSQL driver -- was being stored in this growing list. Over 4-6 hours of
>  30-second polling with verbose library logging, the list accumulated hundreds of thousands
>  of log records.
>
>  
>
> The logger handler was invisible in the normal code path -- it was configured in the
>  application startup code and then never referenced again, but it held a reference to every
>  log record created, preventing garbage collection.
>
>  
>
> #### What I Did 
>
>  
>
> I added memory profiling to the container using the tracemalloc module from Python's
>  standard library, which tracks memory allocations and can report the top N allocation sites
>  by size. I attached it to the running service by adding a debug endpoint that returned the
>  tracemalloc snapshot in JSON format. After running for 2 hours, the snapshot showed the
>  in-memory log handler's list as the dominant allocation -- thousands of logging.LogRecord
>  objects.
>
>  
>
> The immediate fix was removing the in-memory log handler (the feature it was built for was
>  never going to be implemented anyway). The proper fix if we had kept it would have been
>  bounding the list to the last 1000 records using a collections.deque(maxlen=1000) -- a
>  double-ended queue with a maximum length automatically discards the oldest item when the
>  limit is reached.
>
>  
>
> I also added a memory metrics endpoint to the service that the monitoring system polled
>  every minute, logging the process RSS memory size. This made memory growth visible on a
>  dashboard rather than discoverable only when the container restarted.
>
>  
>
> #### What I Learned 
>
>  
>
> Memory leaks in Python are less common than in C/C++ because of garbage collection, but they
>  do occur. The common sources are: objects stored in containers that are never cleared
>  (logging handlers, caches without eviction, global registries), circular references that
>  prevent reference-count-based collection (Python's cyclic GC handles these but with delay),
>  and large objects stored in global scope or class variables rather than local scope.
>
>  
>
> The tracemalloc module is underused for Python memory debugging. It is part of the standard
>  library, has no dependencies, and can be enabled in production with a feature flag for
>  debugging sessions. The key function is tracemalloc.take_snapshot() followed by comparing
>  two snapshots over time -- the difference shows what allocations are growing.
>
>  
>
> The collections.deque(maxlen=N) pattern is the right way to implement any in-memory
>  bounded buffer -- a recent-events store, a log tail, a sliding window of metrics. It is more
>  memory-safe than a list with a periodic del list[:-N] trim because it enforces the bound
>  atomically on every append.
>
>   
>
> #### How to Say It in the Interview 
>
>  
>
> "At Zemoso I debugged a Python service that was OOM-crashing every 4 to 6 hours in
>  production. My first suspicion was Pandas DataFrames not being released, but I verified
>  those were going out of scope correctly. The actual leak was a custom logging handler added
>  at startup that stored every log record in an unbounded Python list -- including verbose
>  debug logs from third-party libraries. After 4 hours of 30-second polling with library debug
>  logging enabled, the list had hundreds of thousands of LogRecord objects. I found it using
>  tracemalloc, Python's standard library memory profiler, by comparing two snapshots taken
>  an hour apart -- the growing allocation was clearly the log record list. The fix was removing
>  the unused handler. The right pattern if you need an in-memory log buffer is
>  collections.deque(maxlen=1000) -- a deque with a max length automatically discards the
>  oldest element on each append, so it is memory-bounded by design."
>
>   
>
> #### Lessons Learned Summary 
>
>    
>
>   | Story  | Root Cause Category  | Prevention Pattern 
>
>    
>
>   | Silent join fan-out  | Wrong join key assumption + no count monitoring  | Asset check asserting Silver/Bronze row ratio; verify join key uniqueness before use 
>
>  
>
>   | Pagination truncation  | Python truthiness vs explicit None check  | Always use is None for sentinel checks on protocol values 
>
>  
>
>   | dbt incremental blind spot  | Incremental strategy mismatch with source change behavior  | Validate source soft-delete behavior before choosing incremental strategy; prefer full merge for uncertain sources 
>
>  
>
>   | PySpark data skew OOM  | Partition key cardinality assumption failed at scale  | Analyze key distribution before building aggregation pipeline; monitor max/median task duration ratio 
>
>  
>
>   | Terraform state drift  | IaC drift from manual portal changes + incomplete state  | Nightly drift detection in CI; codify all manually-created resources; enforce no-manual-changes policy 
>
>  
>
>   | Python memory leak  | Unbounded in-memory container in global scope  | Prefer bounded collections (deque(maxlen=N)) for any in-memory buffer; use tracemalloc for memory debugging 
>
>     
>
> ## EPIK SOLUTIONS — Senior Data Engineer (Jul 2025 – Present) 
>
>  
>
> #### Enterprise Security Data Platform 
>
>   
>
> ### Bullet 1 — Azure Databricks Medallion Lakehouse + Delta Live Tables 
>
>   
>
> "Architected Azure Databricks medallion lakehouse (Bronze/Silver/Gold) using Delta Live Tables and PySpark, ingesting 50M+ daily security events with schema enforcement and full lineage tracking via Unity Catalog."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>  Epik Solutions was building an enterprise security analytics platform for large clients — think security operations centers that needed to detect threats across millions of firewall logs, endpoint events, and cloud audit trails. Their existing setup was a flat blob of raw files dumped into Azure Storage with no organization, no quality guarantees, and no way to trace where data came from. Analysts were writing fragile SQL against raw files with no idea if the data was valid or stale.
>
>  
>
> Task
>  Design the foundational data architecture — the system that everything else would sit on top of. My responsibility was to build a structured, reliable, traceable data platform that could handle 50 million+ events per day and still guarantee data quality at every stage.
>
>  
>
> Action — Step by step
>
>   
> -  
>
> What a Medallion Lakehouse is and why it matters:
>  Instead of one chaotic raw data layer, I designed three distinct layers in ADLS Gen2:
>
>   
> - Bronze: Raw, append-only data. Exactly as it arrived from the source. No transformations. If something breaks downstream, you always have the original. 
> - Silver: Cleaned, typed, deduplicated, schema-enforced. Bad records filtered out or quarantined, timestamps normalized to UTC, columns cast to correct types. 
> - Gold: Business-ready, pre-aggregated tables. What analysts and dashboards actually query. Optimized for read performance.
>  This is called the Medallion Architecture — coined by Databricks. It gives you both a historical raw record AND a clean query layer simultaneously.   
> -  
>
> Delta Live Tables (DLT):
>  Instead of writing individual PySpark jobs and chaining them manually, I used Delta Live Tables — Databricks' declarative pipeline framework. You define each table as a Python function decorated with @dlt.table and declare its upstream dependencies. DLT handles:
>
>   
> - Dependency resolution (runs upstream tables before downstream ones automatically) 
> - Auto-recovery: if a job fails mid-run, it knows exactly which tables succeeded and which to re-run 
> - Data quality constraints: you annotate each table with @dlt.expect_or_drop("valid_ip", "src_ip IS NOT NULL") — rows violating the constraint are either dropped, quarantined, or cause the pipeline to fail depending on severity 
> - Pipeline monitoring: a built-in UI showing table-by-table run status, row counts, expectation pass/fail rates   
> -  
>
> PySpark transformations:
>  Between Bronze and Silver I wrote PySpark jobs that:
>
>   
> - Deduplicated events using dropDuplicates(['event_id']) with a window to keep the latest version of any re-sent event 
> - Parsed nested JSON in the raw_payload column using from_json(col('raw_payload'), schema) — Spark can deserialize JSON into typed structs in one pass 
> - Applied schema enforcement using a predefined StructType schema — any column type mismatch surfaces as an error before bad data proceeds   
> -  
>
> Unity Catalog for lineage:
>  Unity Catalog is Databricks' unified governance layer. Every table I created was registered in the catalog with its owner, tags, and full column-level lineage — so you can click any column in any Gold table and trace exactly which raw source column it came from, through every transformation step. This is critical for compliance: when an auditor asks "where did this field come from?", you have a visual proof.
>
>    
>
> Result
>  50M+ daily events processed reliably across the three layers. Schema violations caught at the Silver layer before they could corrupt Gold analytics. Lineage tracking satisfied the security compliance team's audit requirements. The architecture became the pattern every subsequent client deployment at Epik followed.
>
>   
>
> #### 🔬 Technical Concept Breakdown 
>
>    
>
>   | Term  | What It Is  | Why It Matters 
>
>    
>
>   | Medallion Architecture  | Bronze (raw) → Silver (clean) → Gold (business-ready) data organization pattern.  | Gives you raw replay ability AND clean analytics in one system. Industry standard for lakehouses. 
>
>  
>
>   | Delta Live Tables (DLT)  | Databricks' declarative pipeline framework. Define tables as functions; DLT handles orchestration, recovery, quality checks.  | Less operational overhead than writing Spark jobs + Airflow DAGs. Built-in quality constraints. 
>
>  
>
>   | Delta Lake  | Open-source storage layer adding ACID transactions and a transaction log to Parquet files.  | Makes cloud storage (ADLS/S3) reliable like a database. Enables upserts, deletes, time travel. 
>
>  
>
>   | ADLS Gen2  | Azure Data Lake Storage Gen2 — Microsoft's cloud object storage optimized for analytics. Hierarchical namespace + RBAC.  | The storage backbone for Azure-based data platforms. Cheaper than databases, infinitely scalable. 
>
>  
>
>   | PySpark  | Python API for Apache Spark — distributed data processing across a cluster.  | Process data too large for a single machine. Parallelized across many cores/nodes automatically. 
>
>  
>
>   | Unity Catalog  | Databricks' centralized governance layer: tables, schemas, access policies, column-level lineage in one place.  | Fine-grained access control + automatic data lineage across all Databricks workspaces. 
>
>  
>
>   | Column-Level Lineage  | Ability to trace any column in any table back to its original source column through all transformation steps.  | Compliance & debugging superpower. "Where did this number come from?" answered visually. 
>
>  
>
>   | Schema Enforcement  | Rejecting writes that don't match the expected table schema (column names, types).  | Prevents silent schema drift from breaking downstream pipelines. The first line of data quality defense. 
>
>  
>
>   | DLT @dlt.expect_or_drop  | A data quality annotation: rows failing the condition are dropped (or quarantine/fail depending on severity).  | Inline data quality without writing separate validation code. Results tracked in DLT Event Log. 
>
>     
>
> #### 💬 How to Say It in the Interview 
>
>  
>
> "At Epik we were ingesting 50 million security events a day and the original setup was just raw files dumped into blob storage — no structure, no quality guarantees. I designed the full medallion architecture: Bronze for raw append-only storage, Silver for cleaned and schema-enforced data, Gold for analytics-ready tables. I implemented it using Delta Live Tables, which is Databricks' declarative pipeline framework — you define each table as a Python function, annotate data quality expectations inline, and DLT handles dependency resolution, failure recovery, and monitoring automatically. Everything was registered in Unity Catalog so we had column-level lineage from Gold all the way back to the raw source — that's what the security compliance team needed for their audit trail."
>
>   
>
> #### ❓ Likely Follow-up Questions 
>
>   
> -  
>
> "What's the difference between Delta Lake and a regular data lake?"
>  → A regular data lake is just files on object storage — no transactions, no ACID, no history. Delta Lake adds a transaction log (_delta_log) that records every operation. This enables ACID guarantees (writes are atomic), time travel (query old versions with VERSION AS OF), and schema enforcement. Without Delta, your data lake becomes a data swamp over time.
>
>   
> -  
>
> "Why use DLT instead of regular Spark jobs with Airflow?"
>  → Regular Spark + Airflow requires you to write the orchestration, failure handling, and quality check logic yourself. DLT gives you auto-retry on partial failures, built-in quality constraint tracking with row-level metrics, and a visual pipeline graph with no extra code. The tradeoff is DLT is more opinionated — it works best for the medallion pattern.
>
>   
> -  
>
> "What is Unity Catalog and how does it differ from the legacy Hive Metastore?"
>  → The Hive Metastore in Databricks was workspace-scoped — each workspace had its own catalog with no cross-workspace visibility. Unity Catalog is account-level — one governance layer for all workspaces. It also adds column-level security (masking policies), row-level security, and automated data lineage that the Hive Metastore never had.
>
>     
>
> ### Bullet 2 — Snowflake + dbt for Enterprise Security Analytics 
>
>   
>
> "Built Snowflake data warehouse models with dbt for enterprise security analytics, applying incremental materializations, clustering keys, and Snowpipe auto-ingest to reduce query latency by 45% downstream."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>  After the medallion lakehouse was built in Databricks, the Gold layer data needed to flow into Snowflake — the warehouse that downstream BI tools and analysts queried directly. Security analysts needed to run queries like "show me all high-severity alerts from the last 30 days grouped by tenant and threat type." Without proper modeling these queries scanned hundreds of millions of rows and took 3+ minutes. Unusable in a live SOC environment.
>
>  
>
> Task
>  Build the Snowflake transformation layer using dbt — turning the raw-ish data from Databricks into clean, optimized, analyst-friendly models. Reduce query latency to under 10 seconds for standard analyst queries.
>
>  
>
> Action — Step by step
>
>   
> -  
>
> What dbt is (and what it is not):
>  dbt (data build tool) is a transformation framework. It does NOT extract or load data — it only transforms data that's already in your warehouse. You write SQL SELECT statements, dbt wraps them in CREATE TABLE AS or CREATE VIEW AS statements, and runs them in the right dependency order. The magic is: dbt makes SQL a proper software engineering artifact — with version control, tests, documentation, and lineage.
>
>   
> -  
>
> dbt model layers:
>  I organized the dbt project into three layers mirroring the medallion architecture:
>
>   
> - Staging models (stg_*): One-to-one with source tables. Just renaming columns, casting types, filtering out test data. No business logic. Materialized as views (no storage cost, always fresh). 
> - Intermediate models (int_*): Joining staging tables together, applying business logic (e.g., enriching alerts with tenant metadata). Materialized as ephemeral models (CTEs, not stored) or tables for heavy joins. 
> - Mart models (mart_*): The final analytics-ready tables. Fact and dimension tables following star schema. Materialized as incremental tables.   
> -  
>
> Incremental materialization — this is where the 45% latency reduction came from:
>  For the mart_security_alerts table (the main fact table), I used dbt's materialized = 'incremental' with an is_incremental() filter:
>
>  
>
> ```text
> {{ config(materialized='incremental', unique_key='alert_id') }}
> SELECT * FROM {{ ref('int_alerts_enriched') }}
> {% if is_incremental() %}
>   WHERE event_time > (SELECT MAX(event_time) FROM {{ this }})
> {% endif %}
>
> ```
>
> On the first run: full table build. On every subsequent run: only processes rows newer than the latest record already in the table. This turned a 20-minute full refresh into a 90-second incremental run.
>
>   
> -  
>
> Clustering keys:
>  Snowflake's query optimizer benefits enormously from clustering keys on high-cardinality filter columns. I added cluster_by = ['event_date', 'tenant_id'] on the main fact table. Snowflake reorganizes micro-partitions so queries filtering on those columns scan a tiny fraction of the data. 90% of analyst queries filter on date range + tenant — this single change cut scan volume drastically.
>
>   
> -  
>
> Snowpipe auto-ingest:
>  Data from Databricks landed in ADLS Gen2 as Parquet files. Instead of running a scheduled COPY INTO job every hour, I configured Snowpipe — Snowflake's continuous micro-batch ingestion. An Azure Event Grid notification triggers Snowpipe whenever a new file lands in the storage path. Snowpipe loads it within 1-2 minutes automatically, with no scheduled job to maintain.
>
>   
> -  
>
> dbt tests:
>  Every model had automated tests defined in schema.yml:
>
>   
> - not_null on primary key columns 
> - unique on alert_id 
> - accepted_values on severity column: [low, medium, high, critical] 
> - relationships — every tenant_id in the fact table must exist in dim_tenant
>  These run as part of CI/CD — a PR that breaks a test doesn't get merged.    
>
> Result
>  Query latency on standard analyst queries dropped 45%. Incremental runs cut transform time from 20 minutes to 90 seconds. Snowpipe meant data was in Snowflake within 2 minutes of landing in storage. Analysts went from "I'll get you that report tomorrow" to "let me pull it up right now."
>
>   
>
> #### 🔬 Technical Concept Breakdown 
>
>    
>
>   | Term  | What It Is  | Why It Matters 
>
>    
>
>   | dbt (data build tool)  | SQL-based transformation framework. Write SELECT statements; dbt handles building, testing, and documentation.  | Brings software engineering practices (tests, version control, docs, lineage) to SQL transformations. 
>
>  
>
>   | dbt Materialization  | How dbt persists a model: view (no storage), table (full rebuild every run), incremental (only new rows), ephemeral (CTE).  | Choosing the right materialization is 90% of dbt performance tuning. 
>
>  
>
>   | Incremental Materialization  | On the first run, build the full table. On subsequent runs, only process rows newer than the current max.  | Turns a 20-minute full rebuild into a 2-minute delta load. Essential for large fact tables. 
>
>  
>
>   | is_incremental() block  | dbt Jinja macro that evaluates to true only on non-full-refresh runs. Used to add a WHERE filter.  | Tells dbt "when I'm doing an incremental run, only look at new data." 
>
>  
>
>   | Snowflake Clustering Key  | Metadata that physically co-locates micro-partitions with the same key values. Equivalent to partitioning.  | Drastically reduces scan volume for queries filtering on the cluster key. Best on date + high-cardinality dimension. 
>
>  
>
>   | Micro-partition  | Snowflake's internal storage unit: 50–500MB of compressed, columnar data.  | Snowflake's query optimizer skips micro-partitions whose min/max range doesn't overlap the query filter. 
>
>  
>
>   | Snowpipe  | Snowflake's continuous micro-batch ingestion. Triggers on new file arrival via cloud storage notifications.  | Near-real-time data availability without polling or scheduled COPY INTO jobs. 1-2 minute SLA. 
>
>  
>
>   | dbt schema.yml tests  | Data quality tests defined declaratively in YAML: not_null, unique, accepted_values, relationships.  | Automated data contract enforcement. Run in CI/CD to prevent breaking changes from merging. 
>
>  
>
>   | Staging / Intermediate / Mart  | dbt layer convention: staging = raw source cleanup, intermediate = business logic joins, mart = analytics-ready final tables.  | Separation of concerns. Easier debugging, reuse, and onboarding for new engineers. 
>
>     
>
> #### 💬 How to Say It in the Interview 
>
>  
>
> "Snowflake was the analyst-facing warehouse — everything Databricks produced flowed there. I built the transformation layer in dbt, organized into staging, intermediate, and mart layers. The biggest win was incremental materialization on the main alerts fact table — instead of rebuilding 200 million rows every run, I added an is_incremental block that only processes rows newer than the current max event time. That took transform time from 20 minutes to 90 seconds. For query performance I added clustering keys on event_date and tenant_id, which is Snowflake's way of co-locating micro-partitions — queries filtering on those columns went from scanning the whole table to scanning maybe 5% of it. Data freshness I solved with Snowpipe: files landing in ADLS triggered automatic micro-batch loads in under 2 minutes, so analysts were always querying data that was at most 2 minutes old."
>
>   
>
> #### ❓ Likely Follow-up Questions 
>
>   
> -  
>
> "What's the difference between dbt Core and dbt Cloud?"
>  → dbt Core is the open-source CLI tool — free, runs anywhere, no UI. dbt Cloud is the hosted version — adds a scheduler, a web IDE, CI/CD integration, observability dashboards, and the dbt Explorer for visual lineage. We used dbt Core with Azure DevOps for CI/CD.
>
>   
> -  
>
> "How does dbt handle slowly changing dimensions?"
>  → dbt has a snapshot feature — it tracks row-level history using a dbt snapshot command with a strategy (timestamp or check). It adds dbt_valid_from and dbt_valid_to columns to create a Type 2 SCD automatically.
>
>   
> -  
>
> "What is Elementary and how does it relate to dbt testing?"
>  → Elementary is a dbt package that stores dbt test results as data in your warehouse over time. Instead of just pass/fail on each run, you get historical trending — "this column's null rate was 0.1% last week and is 3% today." It adds observability to dbt tests. Acuity KP specifically listed it — it sits on top of your existing dbt tests and adds time-series tracking and alerting.
>
>     
>
> ### Bullet 3 — Azure Event Hubs + Databricks Structured Streaming 
>
>   
>
> "Designed Azure Event Hubs streaming ingestion pipelines feeding Databricks Structured Streaming jobs into Delta Lake, achieving sub-5-minute data freshness SLA for real-time security alerting workflows."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>  Some security events couldn't wait for a batch pipeline. A lateral movement attack — where a compromised account accesses multiple systems in sequence — might complete in under 10 minutes. If your data pipeline had a 1-hour batch window, the detection would always come too late. The security alerting team needed event data available for their detection rules within 5 minutes of the event occurring.
>
>  
>
> Task
>  Design a streaming ingestion pipeline that continuously moved security events from source systems into Delta Lake with a guaranteed sub-5-minute freshness SLA.
>
>  
>
> Action — Step by step
>
>   
> -  
>
> Azure Event Hubs:
>  Event Hubs is Azure's managed message streaming service — think of it as Azure's equivalent of Apache Kafka. Source systems (endpoint agents, cloud audit log forwarders, network taps) published events as JSON messages to Event Hubs topics called namespaces/event hubs. Event Hubs retains messages for up to 7 days, so if the Databricks consumer falls behind or crashes, it can replay from its last position.
>
>  
>
> Key Event Hubs concepts:
>
>   
> - Partitions: Each event hub is split into N partitions for parallelism. Messages with the same partition key go to the same partition (preserving per-source ordering). 
> - Consumer Groups: Each reader (Databricks in this case) has its own consumer group with independent offset tracking. 
> - Capture: Event Hubs can auto-archive messages to ADLS Gen2 as Avro files — this gave us the Bronze layer for free.   
> -  
>
> Databricks Structured Streaming:
>  Structured Streaming is Spark's streaming execution engine. Unlike micro-batch systems, it models a data stream as an unbounded DataFrame — you write the same transformation code as for batch, and Spark handles the continuous processing.
>
>  
>
> My streaming job:
>
>  
>
> ```text
> df = (spark.readStream
>   .format("eventhubs")
>   .options(**ehConf)
>   .load())
>
> parsed = df.select(
>   from_json(col("body").cast("string"), event_schema).alias("data"),
>   col("enqueuedTime").alias("ingestion_time")
> ).select("data.*", "ingestion_time")
>
> query = (parsed.writeStream
>   .format("delta")
>   .option("checkpointLocation", checkpoint_path)
>   .trigger(processingTime="30 seconds")
>   .toTable("silver.security_events"))
>
> ```
>
> The .trigger(processingTime="30 seconds") means: process whatever arrived in the last 30 seconds every 30 seconds. This gives ~1-minute end-to-end latency from event emission to Delta table availability.
>
>   
> -  
>
> Checkpointing:
>  The checkpointLocation is a folder in ADLS Gen2 where Spark persists the stream's progress — which Event Hubs offsets have been processed. If the streaming job crashes and restarts, it resumes exactly from where it left off. No data lost, no duplicates.
>
>   
> -  
>
> Exactly-once semantics with Delta Lake:
>  Delta Lake + Structured Streaming together provide exactly-once processing — each event is written to Delta exactly once, even if a job fails midway and is restarted. This is because Delta's transaction log records which offsets were committed, and Structured Streaming checks this before writing.
>
>   
> -  
>
> Meeting the 5-minute SLA:
>
>   
> - Event emitted by source → Event Hubs: ~1-5 seconds 
> - Event Hubs → Databricks trigger: 30-second trigger interval 
> - Databricks transformation + Delta write: ~20-30 seconds 
> - Total: well under 2 minutes in normal operation. SLA of 5 minutes was met with 3x headroom.    
>
> Result
>  Sub-5-minute data freshness SLA achieved and maintained. Security alerting rules that previously ran on 1-hour-old data now ran on data that was 1-2 minutes old. Lateral movement detection accuracy improved significantly because correlated events arrived in the same analysis window.
>
>   
>
> #### 🔬 Technical Concept Breakdown 
>
>    
>
>   | Term  | What It Is  | Why It Matters 
>
>    
>
>   | Azure Event Hubs  | Azure's managed event streaming service. Compatible with Apache Kafka protocol.  | Decouples event producers from consumers. Durable, scalable, 7-day retention for replay. 
>
>  
>
>   | Event Hubs Partition  | An ordered log within an event hub. Messages with the same partition key are ordered within a partition.  | More partitions = more parallel consumers. Per-key ordering guaranteed within a partition. 
>
>  
>
>   | Consumer Group  | An independent view into an event hub. Each consumer group tracks its own offset.  | Multiple downstream systems can read the same event hub independently at their own pace. 
>
>  
>
>   | Databricks Structured Streaming  | Spark's streaming engine. Treats a stream as an unbounded DataFrame. Write batch-style code; runs continuously.  | Same API as batch Spark. Simplifies code — no separate streaming framework to learn. 
>
>  
>
>   | .trigger(processingTime=...)  | How often Spark wakes up to process accumulated messages. 30s = micro-batch every 30 seconds.  | Controls latency vs throughput tradeoff. Shorter = lower latency, higher overhead. 
>
>  
>
>   | Checkpoint Location  | A folder in cloud storage where Spark writes stream progress (last committed offset).  | Enables fault-tolerant, exactly-once restarts. If job crashes, it resumes from last checkpoint. 
>
>  
>
>   | Exactly-once Semantics  | Each message is processed and written to the output exactly once, even on failure + restart.  | Data integrity guarantee. Without it, retries cause duplicates or missed records. 
>
>  
>
>   | Event Hubs Capture  | Event Hubs' built-in auto-archival to ADLS Gen2 as Avro files at configurable intervals.  | Free Bronze layer. Raw event archive without any pipeline code. 
>
>  
>
>   | from_json()  | Spark SQL function to parse a JSON string column into a typed struct using a provided schema.  | Needed because Event Hubs delivers message body as bytes — you deserialize it in Spark. 
>
>     
>
> #### 💬 How to Say It in the Interview 
>
>  
>
> "For real-time security alerting we needed data in Delta Lake within 5 minutes of an event happening — batch pipelines couldn't satisfy that. I built the streaming layer using Azure Event Hubs as the ingestion buffer — source agents pushed events there — and Databricks Structured Streaming as the consumer. The streaming job read from Event Hubs, parsed the JSON body, transformed it to the Silver schema, and wrote to Delta with a 30-second trigger. The checkpoint location in ADLS ensured exactly-once delivery — if the job crashed and restarted, no duplicates, no gaps. End-to-end latency was consistently under 2 minutes, well within the 5-minute SLA. I also turned on Event Hubs Capture to get a free Bronze archive — Avro files in ADLS automatically, zero code."
>
>   
>
> #### ❓ Likely Follow-up Questions 
>
>   
> -  
>
> "How does Structured Streaming handle late-arriving data?"
>  → Spark has a withWatermark() API: df.withWatermark("event_time", "10 minutes") tells Spark to wait up to 10 minutes for late events before finalizing a window. Events arriving after the watermark are dropped. Without watermarking, Spark holds state indefinitely for all possible late events — memory leak.
>
>   
> -  
>
> "Event Hubs vs Kafka — when would you use one vs the other?"
>  → Event Hubs is fully managed on Azure with zero operational overhead — no cluster to run. Kafka gives you more control: custom configurations, more connector ecosystem, works outside Azure. Event Hubs actually implements the Kafka protocol, so you can use Kafka clients against Event Hubs. If you're all-in on Azure and don't need Kafka-specific features, Event Hubs is simpler to operate.
>
>     
>
> ### Bullet 4 — Azure Infrastructure + Terraform + Azure DevOps CI/CD 
>
>   
>
> "Provisioned end-to-end data infrastructure on Azure (ADLS Gen2, Databricks, Event Hubs, Key Vault) using Terraform IaC, reducing environment setup time from days to under 2 hours via Azure DevOps CI/CD."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>  Every new client onboarding at Epik required a new isolated Azure environment — a separate Databricks workspace, ADLS storage accounts, Event Hubs namespace, and Key Vault. The original process involved manually clicking through the Azure Portal, which took 2-3 days of DevOps time, was error-prone (someone always forgot a firewall rule), and produced environments that were slightly different from each other in ways that caused subtle bugs.
>
>  
>
> Task
>  Eliminate manual infrastructure provisioning. Codify the entire environment in Terraform so a new client environment could be stood up in under 2 hours with a single pipeline run.
>
>  
>
> Action — Step by step
>
>   
> -  
>
> What Terraform is:
>  Terraform is Infrastructure as Code — you describe your desired infrastructure in .tf files (HCL language), run terraform plan to see what will change, then terraform apply to make it happen. Terraform talks to Azure (and every other cloud) via providers. The key insight: infrastructure becomes code — version-controllable, reviewable, testable, reproducible.
>
>   
> -  
>
> What I provisioned in Terraform:
>
>   
> - ADLS Gen2 storage account with hierarchical namespace, Bronze/Silver/Gold containers, and lifecycle management policies (auto-archive files older than 90 days to cool tier) 
> - Azure Databricks workspace with Unity Catalog enabled, cluster policies, and auto-scaling compute configurations 
> - Azure Event Hubs namespace with client-specific event hubs, consumer groups, and Capture to ADLS enabled 
> - Azure Key Vault for all secrets (storage access keys, API credentials, Snowflake passwords) — nothing stored in code or config files 
> - Azure AD service principal with minimum required RBAC roles (not Owner — exactly what was needed)   
> -  
>
> Azure Key Vault for secrets management:
>  No secret ever touches code or a config file. All credentials are stored in Key Vault and retrieved at runtime:
>
>   
> - Databricks jobs retrieve secrets via dbutils.secrets.get(scope='kv-scope', key='snowflake-password') 
> - Python pipelines use the Azure SDK: SecretClient(vault_url, DefaultAzureCredential()).get_secret("snowflake-password").value 
> - Key Vault itself is provisioned and configured by Terraform including access policies   
> -  
>
> Azure DevOps CI/CD pipeline:
>  I built a two-stage Azure Pipeline:
>
>   
> - PR stage: terraform validate + terraform plan — the plan output is posted as a PR comment so reviewers can see exactly what infrastructure will change 
> - Merge to main: terraform apply -auto-approve — deploys the change to the target environment 
> - Environment isolation: separate Terraform state files per environment (dev/staging/prod) stored in Azure Blob backend with state locking   
> -  
>
> State management:
>  Terraform tracks what it has deployed in a state file — a JSON file mapping Terraform resources to real Azure resource IDs. I stored state in Azure Blob Storage with state locking via a lease mechanism — prevents two pipeline runs from applying simultaneously and corrupting state.
>
>    
>
> Result
>  New client environment setup: 2 hours end-to-end (pipeline run time). Previously: 2-3 days of manual work. Zero configuration drift between environments — dev, staging, and prod were identical because they all deployed from the same Terraform code.
>
>   
>
> #### 🔬 Technical Concept Breakdown 
>
>    
>
>   | Term  | What It Is  | Why It Matters 
>
>    
>
>   | Terraform  | Open-source Infrastructure as Code tool. Declares desired infrastructure state in HCL; applies it against cloud APIs.  | Reproducible, version-controlled infrastructure. The industry standard for cloud IaC. 
>
>  
>
>   | HCL (HashiCorp Config Language)  | Terraform's declarative configuration language.  | Human-readable syntax for defining resources: resource "azurerm_storage_account" "bronze" { ... }. 
>
>  
>
>   | terraform plan  | Dry-run: shows exactly what Terraform will create, modify, or destroy before applying.  | Safety check. Review the plan before touching real infrastructure. 
>
>  
>
>   | Terraform State  | A JSON file mapping Terraform config to real cloud resources. Terraform reads it to know what's deployed.  | Without state, Terraform can't know what already exists. Stored remotely for team collaboration. 
>
>  
>
>   | Remote State Backend  | Storing Terraform state in Azure Blob / S3 / GCS instead of locally.  | Enables team collaboration. Prevents "works on my machine" with different local states. 
>
>  
>
>   | State Locking  | Preventing concurrent Terraform applies via a lease/lock on the remote state.  | Without locking, two simultaneous apply runs corrupt the state file. 
>
>  
>
>   | Azure Key Vault  | Azure's secrets management service. Store, rotate, and audit access to secrets, certificates, and keys.  | Never hardcode credentials. Key Vault is the Azure equivalent of AWS Secrets Manager. 
>
>  
>
>   | RBAC (Azure)  | Role-Based Access Control on Azure resources. Built-in roles: Owner, Contributor, Reader, plus custom roles.  | Least-privilege access. Service principals get only the IAM permissions they actually need. 
>
>  
>
>   | Azure DevOps Pipelines  | Microsoft's CI/CD platform. YAML-defined pipelines for build, test, and deploy workflows.  | Automates terraform apply on merge, gates deployment behind PR review. 
>
>  
>
>   | Service Principal  | An Azure AD identity for applications/pipelines (not humans). Used for automated authentication.  | Pipelines authenticate as a service principal, not as a human account. Auditable, revocable. 
>
>     
>
> #### 💬 How to Say It in the Interview 
>
>  
>
> "Manual infrastructure provisioning at Epik took 2-3 days per new client — Azure Portal clicking, always slightly inconsistent between environments. I codified the entire stack in Terraform: ADLS storage accounts with lifecycle policies, Databricks workspace with Unity Catalog, Event Hubs, Key Vault — all of it. Every secret went into Key Vault at provision time; code retrieves secrets at runtime via the Azure SDK, nothing is ever in a config file. The Azure DevOps pipeline runs terraform plan on every PR so reviewers see the exact infrastructure diff before merging, then terraform apply on merge to main. New client environment: under 2 hours. Dev, staging, and prod are identical because they all deploy from the same Terraform code — no more 'it works in dev but not prod' mystery."
>
>   
>
> #### ❓ Likely Follow-up Questions 
>
>   
> -  
>
> "How do you manage secrets in a data pipeline — what's wrong with environment variables?"
>  → Environment variables are better than hardcoded strings, but they're still plaintext in memory, visible in process listings, and hard to rotate across many machines. Key Vault (or AWS Secrets Manager) adds: encryption at rest and in transit, fine-grained access policies (which service principal can read which secret), automatic rotation, and audit logs of every access. Databricks secret scopes backed by Key Vault integrate seamlessly.
>
>   
> -  
>
> "What's the difference between Terraform and Azure ARM templates / Bicep?"
>  → ARM templates and Bicep are Azure-native — they only work with Azure. Terraform is cloud-agnostic — same workflow for Azure, AWS, GCP. If your infrastructure spans multiple clouds or you want to avoid vendor lock-in on your IaC tooling, Terraform wins. Bicep is more ergonomic than ARM JSON but still Azure-only.
>
>     
>
> ### Bullet 5 — Dagster Orchestration + Great Expectations Data Quality 
>
>   
>
> "Implemented Dagster-orchestrated pipeline monitoring with Great Expectations (GX) data quality checks across all medallion layers, catching schema drift and anomalies before they reached production analytics layers."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>  We had a running medallion pipeline and streaming ingestion, but no systematic way to know if the data moving through those layers was actually good. Data quality issues were discovered reactively — an analyst would notice a weird number in a dashboard, trace it back, and find that a source system changed a field format three days ago. By then, three days of Gold data was corrupted.
>
>  
>
> Task
>  Build proactive, automated data quality monitoring that caught issues at each layer boundary before they propagated downstream. Orchestrate the quality checks in a way that pipelines automatically paused on failure rather than silently continuing with bad data.
>
>  
>
> Action — Step by step
>
>   
> -  
>
> Why Dagster (not Airflow):
>  Airflow models workflows as task DAGs — the unit is a task (a unit of work). Dagster models workflows as software-defined assets — the unit is a data asset (a table, a file, a model). This distinction matters:
>
>   
> - In Airflow: "run task X at 2 AM" 
> - In Dagster: "materialize the silver_security_events asset, which depends on bronze_raw_events and dim_threat_intel"  
>
> Dagster shows you the asset graph — a visual map of all your data assets and their dependencies. When an asset fails, Dagster highlights exactly which downstream assets are now stale. It also integrates natively with dbt — you can see your dbt models AS assets in the same graph as your Python pipelines.
>
>   
> -  
>
> Dagster asset definitions:
>  Each data layer (Bronze, Silver, Gold, dbt models) was defined as a Dagster @asset:
>
>  
>
> ```text
> @asset(
>   group_name="silver",
>   freshness_policy=FreshnessPolicy(maximum_lag_minutes=10)
> )
> def silver_security_events(bronze_raw_events):
>     # transformation logic
>     return transformed_df
>
> ```
>
> The freshness_policy tells Dagster: if this asset hasn't been materialized in the last 10 minutes, flag it as stale on the dashboard. Monitors alert on staleness.
>
>   
> -  
>
> Great Expectations (GX) integration:
>  Great Expectations is a Python data quality framework. You define Expectations — assertions about your data:
>
>   
> - expect_column_to_not_be_null("event_id") 
> - expect_column_values_to_be_between("severity_score", 0, 100) 
> - expect_table_row_count_to_be_between(min_value=10000, max_value=5000000) — if row count drops below 10K something upstream broke 
> - expect_column_values_to_match_regex("src_ip", r"^\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}$")  
>
> I organized expectations into Expectation Suites per layer — a Bronze suite (minimal: schema and completeness), a Silver suite (stricter: type correctness, value ranges, referential integrity), a Gold suite (business rules: no negative revenue, valid tenant IDs only).
>
>   
> -  
>
> Dagster + GX integration:
>  Used the dagster-ge integration library. Each Dagster asset had a GX validation step as an AssetObservation — it ran the expectation suite against the asset output and reported results back to Dagster's event log. If expectations failed, the asset was marked as failed in the asset graph, and Dagster blocked downstream asset materializations automatically.
>
>   
> -  
>
> Schema drift detection:
>  One of the most valuable GX expectations: expect_table_columns_to_match_ordered_list(columns). If a source system added, removed, or renamed a column, this expectation failed immediately at the Bronze → Silver transition, before any transformation logic tried to reference the missing column and caused a cryptic KeyError 3 layers deep.
>
>    
>
> Result
>  Schema drift and data quality issues caught at the Bronze/Silver boundary, not in production dashboards. Mean time to detection for data quality issues dropped from "analyst notices something wrong 2 days later" to "Dagster alert fires within 10 minutes of the first bad batch."
>
>   
>
> #### 🔬 Technical Concept Breakdown 
>
>    
>
>   | Term  | What It Is  | Why It Matters 
>
>    
>
>   | Dagster  | Asset-centric data orchestration platform. Builds, schedules, and monitors software-defined data assets.  | Models your pipeline as a graph of data assets with dependencies, lineage, and freshness policies. 
>
>  
>
>   | Software-Defined Asset (SDA)  | A Dagster @asset — a Python function that produces a persistent data artifact (table, file, model).  | The fundamental unit in Dagster. Replaces Airflow's task abstraction with a data-centric one. 
>
>  
>
>   | Asset Graph  | Dagster's visual map of all assets and their upstream/downstream dependencies.  | At a glance: what's healthy, what's stale, what's broken, and what's affected downstream. 
>
>  
>
>   | Dagster FreshnessPolicy  | Policy on an asset declaring the maximum acceptable staleness (e.g., materialized within last 10 minutes).  | Proactive staleness monitoring. Alert before an analyst notices stale data in a dashboard. 
>
>  
>
>   | Great Expectations (GX)  | Python framework for defining, documenting, and validating data quality expectations.  | expect_column_to_not_be_null, expect_values_to_be_between, etc. Assertion-based quality checks. 
>
>  
>
>   | Expectation Suite  | A named collection of GX expectations for a specific dataset/layer.  | Group related checks together. Bronze suite = basic checks; Gold suite = strict business rule checks. 
>
>  
>
>   | Validation Result  | GX's output after running an expectation suite: pass/fail per expectation + row-level details on failures.  | The evidence of data quality. Stored for historical trending and audit. 
>
>  
>
>   | Schema Drift  | When a source system changes its schema (adds/removes/renames columns) without notifying downstream consumers.  | One of the top causes of silent pipeline failures. Early detection is everything. 
>
>  
>
>   | Elementary  | dbt package that stores dbt test results over time in your warehouse. Adds anomaly detection and alerting on top.  | Acuity KP's listed tool. Extends dbt tests with time-series trending — "null rate went from 0.1% to 3%." 
>
>  
>
>   | Dagster + dbt integration  | Dagster can import a dbt project and represent all dbt models as Dagster assets.  | One unified asset graph showing both Python pipeline assets and dbt SQL model assets together. 
>
>     
>
> #### 💬 How to Say It in the Interview 
>
>  
>
> "We were discovering data quality issues reactively — an analyst would notice something wrong in a dashboard two days after the source system had silently changed a field format. I fixed that with Dagster and Great Expectations. Dagster is asset-centric — instead of thinking about tasks, you think about data assets and their dependencies. Every layer in the medallion architecture was a Dagster asset with a freshness policy. I attached Great Expectations validation suites to each asset — Bronze suite checked schema and completeness, Silver suite added type correctness and value ranges, Gold suite added business rules. Dagster blocked downstream materializations automatically when GX expectations failed. Schema drift was caught at the Bronze-Silver boundary within 10 minutes of the first bad batch instead of days later."
>
>   
>
> #### ❓ Likely Follow-up Questions 
>
>   
> -  
>
> "Dagster vs Airflow — which would you recommend for a new project?"
>  → Dagster for greenfield. The asset-centric model is a better mental model for data engineering — you reason about your data, not your tasks. Dagster's integration with dbt is first-class, the UI shows you what data is fresh vs stale, and it has better software engineering ergonomics (testability, type hints, resource injection). Airflow has a larger ecosystem and more operational familiarity but the task DAG abstraction doesn't naturally model data lineage.
>
>   
> -  
>
> "What is Elementary and how does it complement Great Expectations?"
>  → Great Expectations is a validation framework — you assert things about data and get pass/fail. Elementary is a dbt observability tool — it stores dbt test results as data in your warehouse over time and adds anomaly detection on top (e.g., if column null rate doubles vs its 7-day average, alert). GX is better for rich, custom validations. Elementary is better for trend-based anomaly detection on top of your existing dbt tests. They're complementary.
>
>     
>
> ### Bullet 6 — Team Tech Leadership, dbt Style Guides, Delta Partitioning Standards 
>
>   
>
> "Led data modeling reviews and pipeline design sessions across a 5-engineer team, establishing dbt style guides and Delta Lake partitioning standards adopted as team-wide conventions."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>  As the team at Epik grew to 5 engineers, each one had slightly different dbt conventions — some named staging models stg_, others stage_, some used incremental materialization everywhere, others used tables everywhere regardless of size. Delta tables had inconsistent partitioning: one engineer partitioned by event_date, another by year_month, another didn't partition at all. This inconsistency made code reviews slow, made debugging painful ("which convention does this repo use?"), and made it hard for new engineers to onboard.
>
>  
>
> Task
>  Establish team-wide conventions for dbt project structure and Delta Lake partitioning, and run design review sessions that prevented bad patterns from reaching main before they became technical debt.
>
>  
>
> Action — Step by step
>
>   
> -  
>
> dbt Style Guide (what I documented and enforced):
>
>   
> - Naming: stg_<source>__<entity> (double underscore separates source from entity), int_<verb>_<entity>, mart_<domain>__<entity>. Example: stg_eventhubs__security_events, int_enrich_alerts, mart_security__alert_summary 
> - Materialization rules: Views for staging (cheap, always fresh), incremental for large fact tables (>10M rows), table for dimension tables and intermediates (small, frequently joined) 
> - Test requirements: Every staging model must have not_null + unique on primary key. Every fact table must have relationships tests on all foreign keys. 
> - Documentation: Every model must have a description in schema.yml. Every column that's not obviously named must have an inline description. 
> - CTEs over subqueries: All multi-step SQL written as a series of named CTEs, not nested subqueries. final CTE at the bottom is what gets selected.   
> -  
>
> Delta Lake partitioning standards:
>
>   
> - Partition only on columns used in frequent WHERE filters. Never partition on high-cardinality columns (e.g., user_id — creates millions of tiny files, the "small file problem"). 
> - Standard: partition by event_date (date, not datetime) for time-series data. If query patterns also filter on tenant_id, add it as a secondary cluster key. 
> - Z-Ordering: For columns that aren't the partition key but are frequently filtered, use Databricks' OPTIMIZE table ZORDER BY (column) to physically co-locate related data within partitions.   
> -  
>
> Design review process:
>  I ran bi-weekly 30-minute "data design reviews" where any engineer working on a new pipeline or model would present their proposed approach before coding. The format: (1) what are the source tables, (2) what is the target schema, (3) what materialization strategy and why, (4) what data quality checks. This prevented significant rework — catching "you're using a table materialization on a 500M row model that rebuilds every 20 minutes" before it's already in production.
>
>    
>
> Result
>  Code reviews became faster because reviewers could check against documented standards rather than debating conventions in every PR. Onboarding a new engineer went from "figure it out from existing code" to "read the style guide, then read two existing models as examples." Delta partitioning inconsistencies were eliminated across the codebase.
>
>   
>
> #### 🔬 Technical Concept Breakdown 
>
>    
>
>   | Term  | What It Is  | Why It Matters 
>
>    
>
>   | Small File Problem  | When Delta/Parquet tables accumulate thousands of tiny files, query performance degrades due to per-file overhead.  | Over-partitioning (partitioning on high-cardinality columns) creates millions of files. OPTIMIZE compacts them. 
>
>  
>
>   | Delta OPTIMIZE  | Databricks command that compacts small Delta files into larger, more efficient ones.  | Fixes small file problem. Run periodically on high-write tables. 
>
>  
>
>   | Z-Ordering  | Delta Lake feature: OPTIMIZE table ZORDER BY (col) co-locates rows with similar values in the same files.  | For columns frequently filtered that aren't the partition key. Multi-dimensional data skipping. 
>
>  
>
>   | dbt Naming Conventions  | stg_ for staging, int_ for intermediate, mart_ for final analytics models.  | Consistent naming = instant context. You know the purpose and layer of any model from its name. 
>
>  
>
>   | CTE Pattern  | Write SQL as a series of named WITH blocks, final SELECT at the bottom from a final CTE.  | Readability. Debugging. Each step is independently inspectable. No nested subquery hell. 
>
>  
>
>   | Tech Lead Role  | Setting technical standards, conducting design reviews, unblocking team members on architecture decisions.  | Beyond individual contribution — scaling your knowledge across the team through documentation and process. 
>
>      
>
> ## SAMAY SYSTEMS LLC — Data Engineer (Jul 2022 – Jun 2025) 
>
>  
>
> #### Financial Compliance SaaS Platform 
>
>   
>
> ### Bullet 7 — Azure Data Factory ELT Pipelines (10+ Sources, Multi-Tenant) 
>
>   
>
> "Built Azure Data Factory ELT pipelines ingesting structured and semi-structured data from 10+ REST APIs and flat-file sources into ADLS Gen2, processing 10K+ compliance records daily across 15+ enterprise tenants."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>  Samay Systems built a compliance tracking SaaS platform for financial services firms. Each client (tenant) had their own data: compliance reports from regulatory APIs (FINRA, SEC feeds), transaction records from flat files dropped via SFTP, trade surveillance data from REST APIs, employee training records from HR systems. 15 clients, each with 4-6 data sources = 60+ individual data feeds that needed to flow into the platform daily.
>
>  
>
> Task
>  Build the data ingestion layer that pulled from all these heterogeneous sources and landed the data in ADLS Gen2, with proper tenant isolation so one client's data never mixed with another's.
>
>  
>
> Action — Step by step
>
>   
> -  
>
> What Azure Data Factory is:
>  ADF is Azure's cloud ETL/ELT orchestration service. It has three core concepts:
>
>   
> - Linked Services: Connection configurations to data sources (REST APIs, SFTP servers, SQL Server, ADLS, Snowflake). Think of them as ODBC connection strings managed in the UI. 
> - Datasets: A named reference to a specific data location within a Linked Service (a specific SFTP path, a specific REST endpoint URL). 
> - Pipelines: The actual workflow — activities (Copy Data, Execute Script, Call REST API, etc.) connected with dependencies and control flow.   
> -  
>
> Parameterized pipelines for multi-tenancy:
>  Instead of building one pipeline per tenant (60+ pipelines), I built parameterized pipeline templates with parameters like tenant_id, source_endpoint_url, target_adls_container. A single "ingest_rest_api" pipeline template served all REST API sources across all tenants — you just pass different parameters. ADF's ForEach activity iterated over a JSON config of tenant-source configurations and spawned parallel pipeline runs.
>
>   
> -  
>
> REST API ingestion with pagination:
>  Most regulatory APIs returned paginated results (e.g., 1000 records per page). I built a pipeline with a Until loop activity that:
>
>   
> - Called the API with a page token 
> - Appended results to a staging file in ADLS 
> - Checked the response for a next_page_token field 
> - Looped until no more pages  
>
> This is the standard pagination pattern for REST APIs in ADF.
>
>   
> -  
>
> SFTP flat-file ingestion:
>  For clients that dropped CSV/Excel files on SFTP servers, ADF's SFTP Linked Service watched for new files using a tumbling window trigger (fires for every fixed-length time window, one run per window). Files were copied to ADLS Bronze with the tenant ID and ingestion timestamp embedded in the folder path: bronze/tenant_{id}/year={y}/month={m}/day={d}/.
>
>   
> -  
>
> Tenant isolation:
>  Every file landed in a tenant-specific ADLS container with Azure AD RBAC scoped to that container. No ADF pipeline for tenant A could read or write to tenant B's container — enforced at the storage layer, not just in application code.
>
>    
>
> Result
>  60+ data feeds ingested daily across 15 enterprise tenants from a handful of parameterized ADF pipeline templates. Tenant isolation enforced at the storage RBAC layer. New tenant onboarding: add their config to the JSON parameter file, no new pipeline code needed.
>
>   
>
> #### 🔬 Technical Concept Breakdown 
>
>    
>
>   | Term  | What It Is  | Why It Matters 
>
>    
>
>   | Azure Data Factory (ADF)  | Azure's managed ETL/ELT orchestration service. Build data pipelines visually or via JSON definition.  | The Azure equivalent of AWS Glue or Apache NiFi. Good for cloud-to-cloud data movement. 
>
>  
>
>   | Linked Service  | ADF's connection configuration to a data source (credentials, endpoint, auth method).  | The "connector" abstraction. Configure once, reuse across multiple datasets and pipelines. 
>
>  
>
>   | Parameterized Pipeline  | An ADF pipeline with parameter placeholders (@pipeline().parameters.tenant_id).  | One template, many executions with different configs. Eliminates copy-paste pipelines. 
>
>  
>
>   | ForEach Activity  | ADF activity that iterates over an array and spawns parallel (or sequential) inner pipeline runs.  | Drive multi-tenant or multi-source pipelines from a config array. 
>
>  
>
>   | Until Activity  | ADF activity that loops until a condition is true. Used for API pagination.  | "Keep calling the API until there are no more pages." 
>
>  
>
>   | Tumbling Window Trigger  | ADF trigger that fires for every fixed-length time window (e.g., every hour), one run per window, no overlap.  | Good for batch loads that need to process each time window exactly once. 
>
>  
>
>   | Multi-tenant Architecture  | A single platform instance serving multiple clients (tenants) with strict data isolation between them.  | SaaS fundamental. Each tenant's data must be logically and physically isolated. 
>
>     
>
> ### Bullet 8 — SQL Server → Snowflake Migration + Dagster Asset Pipelines 
>
>   
>
> "Migrated on-premise SQL Server compliance warehouse to Snowflake, designing star-schema dimensional models and orchestrating historical loads via Dagster asset pipelines, reducing analyst query latency 60%."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>  Samay's compliance warehouse lived on an on-premise SQL Server. As the client base grew to 15 tenants and data volume hit hundreds of millions of compliance records, SQL Server was struggling — queries took 10-15 minutes, indexes were ballooning, storage was a constant operational headache. The business decision was made to migrate to Snowflake. My job was to execute that migration without losing any historical data or breaking analyst workflows.
>
>  
>
> Task
>  Design the Snowflake target schema, execute the historical data migration from SQL Server, and cut over live production traffic — all without downtime and without data loss.
>
>  
>
> Action — Step by step
>
>   
> -  
>
> Schema redesign:
>  SQL Server schema was a normalized OLTP design — 3rd Normal Form with many lookup tables and foreign key constraints. This is good for transactional writes but terrible for analytical queries (lots of joins). I redesigned it as a Star Schema for Snowflake:
>
>   
> - fact_compliance_events: One row per compliance event, all foreign keys to dimensions 
> - dim_tenant, dim_regulation, dim_employee, dim_date 
> - Deliberately denormalized — some redundancy is fine in a warehouse to avoid joins  
>
> This single change was responsible for most of the 60% latency improvement.
>
>   
> -  
>
> Dagster asset pipelines for migration:
>  I used Dagster's software-defined assets to model the migration in phases:
>
>   
> - Asset 1: sql_server_extract_compliance_events — exported data from SQL Server as Parquet to ADLS (in chunks, by date range, to avoid memory issues) 
> - Asset 2: transform_to_snowflake_schema — PySpark job that remapped old SQL Server columns to new star schema column names, resolved lookup table foreign keys to denormalized values 
> - Asset 3: snowflake_historical_load — used Snowflake's COPY INTO from ADLS staging 
> - Asset 4: validate_migration_counts — GX expectation: row counts in Snowflake must match SQL Server source within 0.01% tolerance  
>
> Each asset ran independently and could be re-run if it failed — idempotent writes (MERGE, not INSERT) ensured no duplicates on retry.
>
>   
> -  
>
> Incremental cutover:
>  Historical load (5 years of data) ran over a weekend. For the cutover, I ran SQL Server and Snowflake in parallel for 2 weeks — both pipelines populated simultaneously. Analysts tested their Snowflake queries against SQL Server baseline before cutting over. This is called a parallel run — reduces risk because you have a fallback.
>
>   
> -  
>
> Dagster for ongoing orchestration:
>  After migration, Dagster orchestrated the ongoing ELT — ADF loaded raw data to ADLS, Dagster assets materialized the star schema layers in Snowflake in the right order, with data quality checks gating each layer.
>
>    
>
> Result
>  Zero data loss on migration (validated by count reconciliation). Analyst query latency dropped 60% — from 10-15 minutes on SQL Server to under 4 minutes on Snowflake star schema. Ongoing pipeline reliability improved because Dagster gave the team visibility into which assets were fresh vs stale.
>
>   
>
> #### 🔬 Technical Concept Breakdown 
>
>    
>
>   | Term  | What It Is  | Why It Matters 
>
>    
>
>   | 3NF (Third Normal Form)  | OLTP normalization: every non-key attribute depends only on the primary key. No redundancy.  | Optimal for transactional writes. Terrible for analytics — requires many joins for simple aggregations. 
>
>  
>
>   | Star Schema  | Fact table + denormalized dimension tables. Optimized for analytical read queries.  | Fewer joins, faster aggregation, simpler SQL. The Kimball methodology standard for data warehouses. 
>
>  
>
>   | Snowflake COPY INTO  | Bulk-load command: reads files from cloud storage and loads into a table in parallel.  | Orders of magnitude faster than INSERT statements for large-scale data loads. 
>
>  
>
>   | Parallel Run  | Running old and new systems simultaneously during a migration, comparing outputs before cutting over.  | The safest migration strategy. You can roll back if Snowflake produces different results. 
>
>  
>
>   | Count Reconciliation  | Asserting that row counts between source and destination match within an acceptable tolerance.  | The most basic migration validation. If counts don't match, data was lost or duplicated. 
>
>  
>
>   | Idempotent Write  | A write operation that produces the same result no matter how many times you run it (no duplicates).  | Critical for reliable pipelines. MERGE/upsert is idempotent; blind INSERT is not. 
>
>  
>
>   | Dagster Asset Pipeline  | A Dagster workflow where each step is a software-defined asset, run in dependency order.  | Models the migration as data artifacts with lineage, not just a sequence of tasks. 
>
>     
>
> ### Bullet 9 — PySpark ELT on Databricks (Replacing ADF Transformations) 
>
>   
>
> "Adopted Azure Databricks and Delta Lake to replace brittle ADF transformation logic, building PySpark-based ELT jobs with idempotent writes, watermarking, and schema evolution handling across all compliance datasets."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>  ADF's transformation capabilities (Data Flow activities) were initially used for the T in ELT — cleaning and transforming data after ingestion. Over time, these ADF Data Flows became increasingly complex, hard to test, and impossible to debug when they failed. ADF Data Flows are essentially a drag-and-drop GUI tool — they're fine for simple column renames, but not for complex conditional logic, multi-step business rule application, or anything requiring Python. We kept hitting the ceiling of what the GUI tool could do.
>
>  
>
> Task
>  Move all complex transformation logic from ADF Data Flows into PySpark jobs on Databricks, making the transformations testable, version-controllable, and maintainable.
>
>  
>
> Action — Step by step
>
>   
> -  
>
> Idempotent writes with Delta MERGE:
>  The key requirement: if a job runs twice (failure + restart), no duplicate data. I implemented every write as a Delta MERGE (upsert):
>
>  
>
> ```text
> delta_table.alias("target").merge(
>   source_df.alias("source"),
>   "target.compliance_event_id = source.compliance_event_id"
> ).whenMatchedUpdateAll().whenNotMatchedInsertAll().execute()
>
> ```
>
> This inserts new records and updates existing ones. Running the same job twice: second run updates the same rows to the same values. No new rows created. Idempotent.
>
>   
> -  
>
> Watermarking for incremental loads:
>  Instead of processing the full compliance dataset on every run, I tracked a high watermark (the maximum event_timestamp value of records already processed) in a _pipeline_state Delta table. Each job run:
>
>   
> - Read the current watermark 
> - Queried source only for records newer than the watermark 
> - Processed and wrote those records 
> - Updated the watermark to the new maximum  
>
> This is the bookmark/watermark pattern — fundamental to incremental ELT.
>
>   
> -  
>
> Schema evolution handling:
>  Source compliance data came from APIs that occasionally added new fields. In a traditional setup, a new source column would fail the write because the target schema didn't have it. I enabled Delta's schema evolution (mergeSchema=True option on write):
>
>  
>
> ```text
> df.write.format("delta").option("mergeSchema", "true").mode("append").save(path)
>
> ```
>
> New columns in the source are automatically added to the Delta table schema. Existing columns are unchanged. No pipeline failure, no manual schema migration script needed.
>
>   
> -  
>
> Testing PySpark transformations:
>  Unlike ADF GUI flows, PySpark code is testable. I wrote unit tests using pyspark.testing.assertDataFrameEqual — created a small in-memory test DataFrame, ran the transformation function, asserted the output matched expected results. Tests ran in the Azure DevOps CI pipeline on every PR.
>
>    
>
> Result
>  Complex ADF Data Flows retired. All transformation logic now lived in version-controlled PySpark files with unit tests. Schema changes from source APIs no longer caused pipeline failures. Debugging a failed job went from "open ADF Studio and click through 50 connected boxes" to "read the Python stack trace."
>
>   
>
> #### 🔬 Technical Concept Breakdown 
>
>    
>
>   | Term  | What It Is  | Why It Matters 
>
>    
>
>   | Delta MERGE (Upsert)  | SQL/PySpark operation: insert if key doesn't exist, update if it does.  | Idempotent writes. Run the same job twice, same result, no duplicates. 
>
>  
>
>   | Watermark / High Watermark  | A saved value (usually max timestamp or ID) marking the furthest-processed record.  | Resume from where you left off. Don't reprocess the entire dataset on every run. 
>
>  
>
>   | _pipeline_state table  | A small Delta table tracking pipeline metadata (last run watermark, row counts, etc.).  | Persistent state for incremental jobs. Survives job restarts. 
>
>  
>
>   | Schema Evolution  | Ability to automatically add new columns to a table when new source columns appear.  | Prevents pipeline failures when upstream schemas change. Delta supports this natively. 
>
>  
>
>   | mergeSchema=True  | Delta write option that allows new source columns to be added to the target schema automatically.  | Enable schema evolution for append/overwrite operations. 
>
>  
>
>   | ADF Data Flows  | ADF's visual ETL transformation tool. Drag-and-drop UI for column transformations.  | Good for simple transformations. Breaks down for complex business logic. Hard to test. 
>
>     
>
> ### Bullet 10 — Power BI + DAX for Financial Compliance KPIs 
>
>   
>
> "Developed Power BI dashboards with DAX measures for compliance KPI reporting, connecting to Snowflake via DirectQuery to deliver real-time financial insights for 15+ enterprise tenants."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>  Compliance officers at each of Samay's 15 client firms needed to track KPIs like: % of trades reviewed on time, open regulatory findings by severity, employee training completion rates, and days since last audit. These weren't nice-to-have dashboards — in financial services, a compliance officer who can't prove oversight in real-time has a regulatory problem. They needed live numbers, not yesterday's Excel export.
>
>  
>
> Task
>  Build Power BI dashboards for compliance KPIs that (1) reflected real-time data, (2) were scoped per tenant so each firm saw only their own data, and (3) had DAX measures that correctly implemented financial compliance business logic.
>
>  
>
> Action — Step by step
>
>   
> -  
>
> DirectQuery vs Import:
>  I chose DirectQuery mode — queries go directly to Snowflake at report-open time. The alternative, Import mode, would cache data in Power BI and refresh on a schedule (fastest queries, but always stale by the refresh interval). For compliance reporting where officers needed live numbers before a regulatory call, stale data wasn't acceptable.
>
>   
> -  
>
> Key DAX measures I built:
>
>  
>
> Trade review timeliness (% of trades reviewed within required window):
>
>  
>
> ```text
> On-Time Review % = 
> DIVIDE(
>   CALCULATE(COUNTROWS(fact_trades), fact_trades[reviewed_within_sla] = TRUE),
>   COUNTROWS(fact_trades),
>   0
> )
>
> ```
>
> Rolling 30-day compliance score (requires date intelligence):
>
>  
>
> ```text
> 30-Day Compliance Score = 
> CALCULATE(
>   [Compliance Score],
>   DATESINPERIOD(dim_date[date], LASTDATE(dim_date[date]), -30, DAY)
> )
>
> ```
>
> DATESINPERIOD is a DAX time intelligence function — it returns a table of dates within a relative period from an anchor date. This pattern works because Power BI's date table enables the time-relative calculation to respect whatever date filter is active on the report.
>
>  
>
> YTD findings (year-to-date regardless of current date filter):
>
>  
>
> ```text
> YTD Findings = TOTALYTD(COUNTROWS(fact_findings), dim_date[date])
>
> ```
>
>   
> -  
>
> Row Level Security for multi-tenancy:
>  A single Power BI dataset served all 15 clients, but each compliance officer could only see their own firm's data. I implemented Row Level Security (RLS):
>
>   
> - Created a role TenantUser with the DAX filter: [tenant_id] = USERPRINCIPALNAME() 
> - Each user's Azure AD UPN was mapped to their tenant ID in a dim_user_tenant table 
> - When a compliance officer logs into Power BI Service, their UPN is passed to the RLS filter, which restricts all visuals to their tenant's data automatically   
> -  
>
> Snowflake + DirectQuery performance:
>  DirectQuery sends native SQL to Snowflake on every visual interaction. For this to be fast, the Snowflake models (built in dbt) needed to be pre-optimized: clustering keys on event_date and tenant_id (the most common filter combination), materialized aggregates for expensive KPIs, and query result caching enabled in Snowflake.
>
>    
>
> Result
>  15 compliance teams got live, self-service dashboards replacing daily email reports. RLS ensured complete tenant isolation in one shared Power BI dataset. Compliance officers went from "I need to call the data team to pull this number" to "I can pull it up before my regulatory call in 30 seconds."
>
>   
>
> #### 🔬 Technical Concept Breakdown 
>
>    
>
>   | Term  | What It Is  | Why It Matters 
>
>    
>
>   | DAX (Data Analysis Expressions)  | Formula language for Power BI and Excel Analysis Services. Used for measures and calculated columns.  | The calculation engine of Power BI. You need it to go beyond basic aggregations. 
>
>  
>
>   | DAX Measure  | A formula evaluated dynamically in the current filter context. Not stored physically.  | The right way to build KPIs. Always calculated fresh for whatever slicers are active. 
>
>  
>
>   | Filter Context  | The set of active filters (slicers, rows, columns) that constrain a DAX evaluation.  | Everything in Power BI is evaluated relative to the current filter context. The core DAX concept. 
>
>  
>
>   | CALCULATE()  | Evaluates an expression in a modified filter context. The most powerful DAX function.  | Override, add, or remove filters for a specific calculation. CALCULATE(measure, filter). 
>
>  
>
>   | DATESINPERIOD()  | DAX time intelligence: returns a table of dates in a relative period from an anchor date.  | Rolling N-day calculations. DATESINPERIOD(date_col, anchor, -30, DAY) = last 30 days. 
>
>  
>
>   | TOTALYTD()  | DAX shortcut for year-to-date calculation. Wraps CALCULATE with DATESYTD.  | YTD metrics that respect the current date filter context. 
>
>  
>
>   | Power BI DirectQuery  | Power BI sends queries to Snowflake at report-render time. Always live, no cache.  | Real-time data. Latency depends on Snowflake query performance. Needs good clustering/indexing. 
>
>  
>
>   | Row Level Security (RLS)  | Power BI security: DAX filter rules restricting which rows each user role sees.  | Multi-tenant dashboards. One dataset, each user sees only their data. Enforced server-side. 
>
>  
>
>   | USERPRINCIPALNAME()  | DAX function returning the logged-in user's email/UPN. Used in RLS to filter by user.  | Dynamic RLS — each user gets their own filtered view based on their identity. 
>
>     
>
> ### Bullet 11 — dbt Transformation Layer with Tests and Documentation 
>
>   
>
> "Implemented dbt transformation layer over Snowflake with modular SQL models, tests, and documentation, reducing ad hoc analyst SQL requests by 40% and improving data discoverability across the B2B platform."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>  Before dbt, analysts at Samay's client firms submitted tickets to the data team for every custom report — "I need compliance events filtered by regulation type X, joined with employee table, grouped by department." The data team spent 40% of their time writing one-off SQL queries for analysts. There was also no central documentation of what tables existed or what columns meant — analysts didn't know what data was available, so they kept asking.
>
>  
>
> Task
>  Build a dbt project that (1) standardized the transformation logic into reusable, well-documented models, (2) generated browsable documentation analysts could explore self-service, and (3) provided data quality tests so analysts could trust what they queried.
>
>  
>
> Action — Step by step
>
>   
> -  
>
> dbt docs:
>  dbt auto-generates a browsable documentation site from schema.yml descriptions. I wrote descriptions for every model and every column:
>
>  
>
> ```text
> models:
>   - name: mart_compliance__trade_reviews
>     description: "One row per trade requiring compliance review. Updated incrementally every 2 hours."
>     columns:
>       - name: trade_id
>         description: "Unique identifier for a trade. Foreign key to dim_trade."
>         tests:
>           - not_null
>           - unique
>       - name: review_sla_breached
>         description: "True if the trade was not reviewed within the regulatory 24-hour window."
>
> ```
>
> Running dbt docs generate + dbt docs serve produced a searchable HTML site with table descriptions, column definitions, lineage graphs, and test results.
>
>   
> -  
>
> dbt lineage graph:
>  dbt's docs site includes a DAG visualization — you can see which sources feed which staging models, which staging feeds which intermediate models, and which intermediates feed which marts. An analyst looking for "where does trade review data come from?" could navigate the lineage graph visually.
>
>   
> -  
>
> Modular SQL models:
>  I built semantic models in the mart layer that analysts could query directly with no additional joins:
>
>   
> - mart_compliance__trade_reviews: Pre-joined trade + employee + regulation data with all derived metrics 
> - mart_compliance__findings_summary: Pre-aggregated findings by tenant, regulation, and severity 
> - mart_compliance__training_completion: Pre-joined training records with employee and training requirement tables  
>
> These covered 90% of analyst query patterns. Instead of writing complex SQL, analysts ran: SELECT * FROM mart_compliance__trade_reviews WHERE tenant_id = '...' AND review_date >= '2024-01-01'.
>
>   
> -  
>
> Reducing ad-hoc requests:
>  The 40% reduction came from two things: (1) analysts could now query pre-joined marts instead of asking the data team to build custom joins, and (2) the self-service dbt docs let analysts discover what tables existed and what columns meant without emailing anyone.
>
>    
>
> Result
>  Data team's ad-hoc analyst request load dropped 40%. New analyst onboarding: "read the dbt docs, query the mart layer." Analysts went from black-box data consumers to self-sufficient query writers.
>
>   
>
> ### Bullet 12 — Unity Catalog RBAC + Column Security + Audit Lineage 
>
>   
>
> "Enforced data governance using Unity Catalog RBAC policies, column-level security, and audit lineage across Databricks workspaces, achieving compliance with enterprise data access control requirements for 15+ clients."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>  Financial compliance data is extremely sensitive — one client's trade data must be completely invisible to another client's users. Within a client, junior compliance analysts should see aggregated reports but not raw PII (Social Security numbers, account numbers in trade records). Senior analysts and compliance officers needed full access. Regulators required audit trails proving who accessed what data and when.
>
>  
>
> Task
>  Implement a data access control system in Databricks Unity Catalog that enforced multi-tenant isolation, column-level PII masking, and produced audit logs for regulatory review.
>
>  
>
> Action — Step by step
>
>   
> -  
>
> Unity Catalog RBAC hierarchy:
>  Unity Catalog organizes data as: Catalog → Schema → Table. RBAC is applied at any level:
>
>   
> - GRANT USE CATALOG ON CATALOG tenant_acme TO GROUP acme_analysts — gives Acme analysts access to Acme's catalog only 
> - GRANT SELECT ON TABLE tenant_acme.silver.compliance_events TO GROUP acme_analysts 
> - No Acme analyst can even see the existence of tenant_bcorp's catalog — not just access denied, completely invisible   
> -  
>
> Column masking policies:
>  For PII columns (employee SSN, account numbers), I created Dynamic Data Masking policies:
>
>  
>
> ```text
> CREATE OR REPLACE FUNCTION mask_ssn(ssn STRING)
> RETURNS STRING
> RETURN CASE WHEN IS_MEMBER('compliance_officers') THEN ssn
>             ELSE CONCAT('XXX-XX-', RIGHT(ssn, 4))
>        END;
>
> ALTER TABLE silver.employee_records
> ALTER COLUMN ssn SET MASK mask_ssn;
>
> ```
>
> A compliance officer sees 123-45-6789. A junior analyst sees XXX-XX-6789. Same query, same table, different result based on group membership. Zero application code changes needed.
>
>   
> -  
>
> Audit lineage:
>  Unity Catalog's System Tables (enabled in account settings) record every data access event in tables like system.access.audit — who ran what query, what tables and columns were accessed, at what time, from which IP and cluster. I set up a Dagster job that periodically queried these audit tables and produced a weekly "data access report" per tenant showing all access events for their data. This was the deliverable regulators required.
>
>   
> -  
>
> Row filters:
>  In addition to column masking, I added row filter policies on multi-tenant tables: even if a user somehow accessed a shared table (which they shouldn't under catalog-level RBAC), a row filter ensured they'd only see rows where tenant_id = current_user_tenant().
>
>    
>
> Result
>  All 15 clients' data governance requirements met. Audit reports produced automatically from Unity Catalog system tables. Zero cross-tenant data leakage incidents. Compliance team could demonstrate to regulators exactly which users accessed which data during any time period.
>
>   
>
> #### 🔬 Technical Concept Breakdown 
>
>    
>
>   | Term  | What It Is  | Why It Matters 
>
>    
>
>   | Unity Catalog RBAC  | GRANT/REVOKE on Catalog/Schema/Table/Column level. Users inherit permissions from groups.  | Fine-grained, auditable access control across all Databricks workspaces. 
>
>  
>
>   | Dynamic Data Masking  | A column-level policy function that returns masked values to unauthorized users but real values to authorized ones.  | Same query, different results by role. PII visible to authorized users only, no app changes needed. 
>
>  
>
>   | Row Filter Policy  | A policy that automatically appends a WHERE clause to queries on a table based on the user's identity.  | Tenant isolation at the row level. Even if the wrong user queries a shared table, they only see their rows. 
>
>  
>
>   | Unity Catalog System Tables  | Databricks-managed tables in system.* schemas recording audit logs, lineage, and usage.  | system.access.audit = every data access event. The backbone of compliance audit reporting. 
>
>  
>
>   | Data Lineage  | Tracking the origin, movement, and transformation of data from source to final table.  | Compliance requirement: "show us where this data came from and who touched it." 
>
>     
>
> ### Bullet 13 — Terraform + Azure DevOps CI/CD (Multi-Tenant) 
>
>   
>
> "Provisioned Azure data infrastructure (ADLS Gen2, ADF, Databricks, Synapse) with Terraform and Azure DevOps CI/CD pipelines, reducing manual deployment errors by 40% across multi-tenant environments."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>  Each of Samay's 15 client environments had its own isolated Azure infrastructure — separate ADLS accounts, ADF instances, Databricks workspaces, and Synapse Analytics. Changes to the shared platform (like adding a new pipeline type, updating a Databricks runtime version) had to be rolled out to 15 environments. Manual deployment scripts had a 40% error rate because someone always forgot to update one of the 15 environments, or applied a config change to prod but not staging.
>
>  
>
> Task
>  Codify the entire per-tenant Azure infrastructure in Terraform with a CI/CD pipeline that deployed consistently to all environments.
>
>  
>
> Action — Step by step
>
>   
> -  
>
> Terraform modules for reuse:
>  I built Terraform modules — reusable infrastructure packages. The tenant_environment module provisioned the full stack for one tenant (ADLS + ADF + Databricks + Synapse + Key Vault + RBAC). To add a new tenant, you called the module with tenant-specific variables:
>
>  
>
> ```text
>  "tenant_acme" ">module "tenant_acme" {
>   source = "./modules/tenant_environment"
>   tenant_id = "acme"
>   environment = "prod"
>   region = "eastus2"
>   compliance_tier = "financial"
> }
>
> ```
>
>   
> -  
>
> Azure DevOps CI/CD flow:
>
>   
> - PR pipeline: terraform fmt check (enforces consistent formatting), terraform validate, terraform plan for each environment. Plan output posted as PR comment. 
> - Merge to main: terraform apply sequentially for dev → staging → prod, with a manual approval gate between staging and prod. 
> - Drift detection: A nightly job ran terraform plan against each environment and alerted if there was any drift (manual changes made in the Azure Portal that aren't in Terraform).   
> -  
>
> Azure Synapse integration:
>  Azure Synapse Analytics was used by some clients as a dedicated SQL pool for heavy analytical queries that benefited from Synapse's MPP (Massively Parallel Processing) architecture — queries that needed to scan and aggregate billions of rows interactively. I provisioned Synapse dedicated SQL pools via Terraform and built ADF pipelines that loaded data from ADLS into Synapse using PolyBase (Synapse's high-throughput bulk load mechanism).
>
>    
>
> Result
>  Deployment error rate dropped 40% because every change went through code review and automated validation before touching any environment. Rolling out a platform update to 15 environments: one PR, one merge, one automated pipeline run.
>
>   
>
> #### 🔬 Technical Concept Breakdown 
>
>    
>
>   | Term  | What It Is  | Why It Matters 
>
>    
>
>   | Terraform Module  | A reusable, parameterized Terraform configuration package. Called like a function with variables.  | Write once, deploy many times with different inputs. The DRY principle applied to IaC. 
>
>  
>
>   | Azure Synapse Analytics  | Azure's unified analytics service: on-demand serverless SQL, dedicated SQL pools (MPP), and Spark.  | Dedicated SQL pools = Massively Parallel Processing for very large interactive queries. 
>
>  
>
>   | MPP (Massively Parallel Processing)  | Database architecture that distributes query processing across many nodes in parallel.  | Synapse/Redshift use this. Very fast for large scans and aggregations on petabyte-scale data. 
>
>  
>
>   | Drift Detection  | Identifying when real infrastructure differs from Terraform's desired state (due to manual Portal changes).  | Prevents config drift. Manual Portal changes that aren't in Terraform will be overwritten on next apply. 
>
>  
>
>   | Manual Approval Gate  | A CI/CD pipeline stage that pauses and requires a human to approve before continuing to prod.  | Safety. Never automatically deploy to production without human sign-off. 
>
>  
>
>   | terraform fmt  | Formats Terraform files to the canonical style. Used in CI to enforce consistent formatting.  | Code style consistency for HCL files. Like black for Python or prettier for JavaScript. 
>
>      
>
> ## ZEMOSO TECHNOLOGIES — Associate Data Engineer (Jul 2020 – Aug 2022) 
>
>  
>
> #### LabOps Platform 
>
>   
>
> ### Bullet 14 — Python ETL with Pandas + PySpark into PostgreSQL 
>
>   
>
> "Built Python ETL pipelines with Pandas and PySpark to ingest, clean, and transform scientific experiment datasets from lab instruments and REST APIs into a PostgreSQL analytical database for 500+ scientists."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>  Zemoso built a LabOps platform for scientific research institutions. Lab instruments (centrifuges, spectrophotometers, PCR machines) generated experiment data in proprietary formats (CSV exports, instrument-specific JSON) and uploaded it to shared network drives. Scientists needed this data queryable in a centralized database for analysis and cross-experiment comparisons. The challenge: 500+ scientists, each with their own instrument and data format quirks.
>
>  
>
> Task
>  Build Python-based ETL pipelines that ingested data from lab instruments and REST APIs, cleaned it, and loaded it into a PostgreSQL analytical database in a consistent, queryable schema.
>
>  
>
> Action — Step by step
>
>   
> -  
>
> Pandas for small-to-medium datasets:
>  For most instrument data (typically <1M rows per experiment), I used Pandas:
>
>   
> - pd.read_csv() / pd.read_json() to ingest 
> - .dropna(subset=['experiment_id', 'measurement_value']) — drop rows missing critical fields 
> - .astype({'measurement_value': 'float64', 'recorded_at': 'datetime64[ns]'}) — type coercion 
> - .drop_duplicates(subset=['reading_id']) — deduplication 
> - Then write to PostgreSQL via df.to_sql(table_name, engine, if_exists='append', index=False)   
> -  
>
> PySpark for large genomics datasets:
>  Some genomics experiments produced datasets too large for a single machine's memory (10GB+ CSV files). For these I used PySpark on a small Databricks cluster — same logic, distributed across workers. The transformation code was nearly identical to Pandas thanks to the API similarity.
>
>   
> -  
>
> REST API ingestion:
>  Some instruments had REST API interfaces. I wrote a Python client with retry logic:
>
>  
>
> ```text
> def fetch_with_retry(url, max_retries=3):
>     for attempt in range(max_retries):
>         try:
>             response = requests.get(url, timeout=30)
>             response.raise_for_status()
>             return response.json()
>         except requests.RequestException as e:
>             if attempt == max_retries - 1:
>                 raise
>             time.sleep(2 ** attempt)  # exponential backoff
>
> ```
>
> Exponential backoff: wait 1s, then 2s, then 4s between retries. Prevents hammering a struggling API.
>
>   
> -  
>
> PostgreSQL schema design:
>  I designed the target schema with proper normalization for the write side but with analytical indexes for the read side:
>
>   
> - Primary tables: experiments, readings, instruments, scientists 
> - Composite indexes on (experiment_id, recorded_at) for the most common query pattern 
> - JSONB column for instrument-specific metadata (PostgreSQL's native semi-structured type — queryable with -> operators)    
>
> Result
>  500+ scientists had a single queryable database for all experiment data across all instrument types. Cross-experiment comparisons that previously required manual data assembly became single SQL queries.
>
>   
>
> ### Bullet 15 — PostgreSQL Schema Design + Query Optimization 
>
>   
>
> "Designed normalized PostgreSQL schemas and optimized SQL queries for LabOps experiment tracking workflows, improving data retrieval performance by 30% and data integrity across 500+ experiment datasets."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>  Early in the project, the PostgreSQL database had grown organically — tables were added as needed, indexes were an afterthought, and queries that had been fast on small datasets were now taking 30+ seconds on the full 3-year data history. Scientists were complaining about the dashboard being unusable during busy lab periods.
>
>  
>
> Task
>  Profile the slow queries, redesign the schema where needed, and add proper indexes to bring query times to acceptable levels.
>
>  
>
> Action — Step by step
>
>   
> -  
>
> Query profiling:
>  Used EXPLAIN ANALYZE in PostgreSQL (the gold-standard for query performance analysis). This shows:
>
>   
> - Seq Scan = bad (reading the whole table). Index Scan = good (using an index for efficient lookup). 
> - Actual rows scanned vs estimated rows — large discrepancy means stale statistics, fixed with ANALYZE table 
> - Where the most time was spent (Sort operations, Hash Join operations, nested loops)   
> -  
>
> Index additions:
>  The single biggest win: a readings query filtered on experiment_id AND reading_type but the index only covered experiment_id. Added a composite index CREATE INDEX ON readings (experiment_id, reading_type) — PostgreSQL could now satisfy both filter conditions from the index alone (index-only scan). Query time: 28 seconds → 3 seconds.
>
>   
> -  
>
> Partial indexes for selective queries:
>  Many queries only cared about status = 'completed' experiments. A full index on status is inefficient because there are only a handful of distinct values (low cardinality). Instead: CREATE INDEX ON experiments (created_at) WHERE status = 'completed' — a partial index that only indexes completed experiments. Smaller index, faster query for that specific filter.
>
>   
> -  
>
> Schema normalization for data integrity:
>  Found a data integrity issue: instrument_type was stored as a free-text column in readings — same instrument appeared as "PCR", "PCR Machine", "pcr machine" depending on who uploaded data. I added a instruments dimension table, made instrument_id a foreign key in readings with a NOT NULL constraint, and wrote a one-time migration to normalize existing values.
>
>    
>
> Result
>  30% aggregate performance improvement across all tracked queries. The slowest dashboard query dropped from 28 seconds to 3 seconds. Data integrity issues on instrument type eliminated.
>
>   
>
> #### 🔬 Technical Concept Breakdown 
>
>    
>
>   | Term  | What It Is  | Why It Matters 
>
>    
>
>   | EXPLAIN ANALYZE  | PostgreSQL command that executes a query and shows the actual execution plan with real row counts and timings.  | The essential tool for query optimization. Shows you exactly where time is being spent. 
>
>  
>
>   | Sequential Scan (Seq Scan)  | Reading every row in a table. Fine for small tables or when you need most of the rows.  | For large tables with selective filters, a Seq Scan means you're missing an index. 
>
>  
>
>   | Index Scan  | Using a B-tree (or other) index to find rows directly by key value.  | Much faster than Seq Scan for selective queries. The goal of most query optimization. 
>
>  
>
>   | Composite Index  | An index on two or more columns: CREATE INDEX ON table (col_a, col_b).  | Most effective when queries filter on the leading columns in order. (a, b) helps WHERE a=X AND b=Y. 
>
>  
>
>   | Partial Index  | An index with a WHERE clause: only indexes rows matching the condition.  | Smaller and faster than a full index for selective queries. WHERE status = 'active' on an active-records query. 
>
>  
>
>   | JSONB  | PostgreSQL's binary JSON column type. Indexable, queryable with operators like -> and ->>.  | Store semi-structured data in PostgreSQL without losing queryability. Can add GIN indexes for JSONB key searches. 
>
>  
>
>   | Foreign Key Constraint  | A column-level constraint ensuring every value exists in the referenced table's primary key.  | Referential integrity enforcement at the database level. Can't have a reading for a non-existent experiment. 
>
>     
>
> ### Bullet 16 — Apache Airflow DAGs for Lab Data Workflows 
>
>   
>
> "Orchestrated batch data workflows using Apache Airflow DAGs with retry logic, SLA alerting, and dependency management, reducing manual pipeline intervention by 35% across 10+ lab data products."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>  By the time we had 10+ lab data pipelines running (one per instrument type, plus several cross-experiment aggregation jobs), there was no coordination — someone manually checked whether each one had run, and a failure in one job cascaded silently into downstream jobs producing stale reports without anyone noticing.
>
>  
>
> Task
>  Implement Airflow orchestration that ran all 10+ pipelines in the right order, retried failures automatically, alerted on SLA breaches, and gave the team a central monitoring view.
>
>  
>
> Action — Step by step
>
>   
> -  
>
> DAG design:
>  The main nightly pipeline DAG:
>
>  
>
> ```text
> ingest_instrument_a ──┐
> ingest_instrument_b ──┤──► clean_readings ──► compute_experiment_stats ──► refresh_dashboard
> ingest_instrument_c ──┘
>
> ```
>
> The three ingest jobs ran in parallel (no dependency on each other). clean_readings waited for ALL ingest jobs with trigger_rule='all_success'. If any ingest failed, the cleaning step and everything downstream was automatically skipped — no stale data processed.
>
>   
> -  
>
> Retry logic:
>  Every task configured with:
>
>  
>
> ```text
> default_args = {
>   'retries': 3,
>   'retry_delay': timedelta(minutes=5),
>   'retry_exponential_backoff': True,
> }
>
> ```
>
> Exponential backoff on retries: waits 5 min, then 10 min, then 20 min. Handles transient network/API failures without hammering a struggling source.
>
>   
> -  
>
> SLA alerting:
>  Defined an SLA on the refresh_dashboard task: sla=timedelta(hours=2). If the entire pipeline hadn't completed within 2 hours of the scheduled start, Airflow fired an SLA miss alert to the team's Slack channel. Scientists knew their morning reports would be fresh by 8 AM or they'd be notified if something was wrong.
>
>   
> -  
>
> XComs for inter-task data:
>  The ingest tasks pushed row counts to XCom: context['ti'].xcom_push(key='rows_ingested', value=len(df)). The clean_readings task pulled these counts and asserted the total was above a minimum threshold before proceeding — a lightweight sanity check that the ingest step actually produced data.
>
>   
> -  
>
> vs Dagster (since Acuity KP uses Dagster):
>  I built this on Airflow in 2020-2022, which was the industry standard at the time. The equivalent in Dagster would be defining each pipeline step as a @asset, using AutoMaterializePolicy.eager() so downstream assets auto-materialize when upstream ones are updated, and using FreshnessPolicy instead of SLA alerts. Same concepts, better ergonomics in Dagster.
>
>    
>
> Result
>  35% reduction in manual intervention — previously 2-3 pipeline failures per week required a human to manually re-run jobs in the right order. Now Airflow handled retries and dependency management automatically. SLA alerts meant the team knew about problems before scientists complained.
>
>   
>
> ### Bullet 17 — AWS Lambda + S3 Event-Triggered Ingestion 
>
>   
>
> "Built AWS Lambda and S3-event-triggered ingestion jobs for automated raw data landing and archival, reducing manual upload overhead by 40%."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>  Some lab instruments could only export data by pushing files to an S3 bucket (a common integration pattern). When a scientist finished an experiment, the instrument's export software uploaded the results file to S3. But then nothing happened — someone had to notice the file was there, manually trigger the ingestion pipeline, and verify it loaded. Scientists were running their own informal "did it load?" checks.
>
>  
>
> Task
>  Make S3 file uploads trigger automatic ingestion — zero manual steps from "file arrives in S3" to "data available in PostgreSQL."
>
>  
>
> Action — Step by step
>
>   
> -  
>
> S3 Event Notifications:
>  S3 can publish events when objects are created, deleted, etc. I configured an S3 Event Notification on the lab-raw-uploads bucket: ObjectCreated:Put events trigger a target. The target was an AWS Lambda function.
>
>   
> -  
>
> Lambda function:
>  The Lambda received an event payload containing the S3 bucket name and object key of the uploaded file:
>
>  
>
> ```text
> def lambda_handler(event, context):
>     bucket = event['Records'][0]['s3']['bucket']['name']
>     key = event['Records'][0]['s3']['object']['key']
>     
>     # download file from S3
>     obj = s3.get_object(Bucket=bucket, Key=key)
>     df = pd.read_csv(obj['Body'])
>     
>     # validate and transform
>     df = validate_and_clean(df)
>     
>     # write to PostgreSQL
>     df.to_sql('raw_readings', engine, if_exists='append', index=False)
>     
>     # archive: move to processed/ prefix
>     s3.copy_object(Bucket=bucket, CopySource=f"{bucket}/{key}", Key=f"processed/{key}")
>     s3.delete_object(Bucket=bucket, Key=key)
>
> ```
>
>   
> -  
>
> Why Lambda:
>  Lambda is serverless — there's no server running permanently waiting for files. Lambda wakes up on-demand, processes the file, and shuts down. Cost: pay only for the execution time (usually milliseconds to seconds). For a workload like "process a file when it arrives, maybe 50 times a day," Lambda is far cheaper than running a dedicated EC2 instance.
>
>   
> -  
>
> Archival:
>  After successful processing, the Lambda moved the file from the uploads/ prefix to processed/ — a permanent archival location. This meant: (1) raw data was always preserved, (2) the uploads/ folder only contained unprocessed files (easy to see what's pending), (3) reprocessing was possible (re-run Lambda against a processed/ file if needed).
>
>    
>
> Result
>  File upload → data in PostgreSQL: fully automated, under 3 minutes. Scientists no longer had a manual step in their workflow. The 40% overhead reduction came from eliminating the entire manual notification/trigger/verify loop.
>
>   
>
> #### 🔬 Technical Concept Breakdown 
>
>    
>
>   | Term  | What It Is  | Why It Matters 
>
>    
>
>   | AWS Lambda  | Serverless function execution. Run code on-demand without managing servers. Pay per execution.  | Event-driven compute. Perfect for "do X when Y happens" patterns with infrequent, bursty workloads. 
>
>  
>
>   | Serverless  | Infrastructure model where the cloud provider manages server provisioning and scaling. You write functions.  | No idle server costs. Auto-scales. Zero ops. The tradeoff: cold starts, max execution time limits. 
>
>  
>
>   | S3 Event Notification  | S3 triggers a notification (to Lambda, SQS, SNS) when a specified event occurs (object created, deleted).  | The primitive for S3-triggered automation. File arrives → Lambda fires immediately. 
>
>  
>
>   | S3 Object Key  | The full path of an object within a bucket: uploads/tenant_acme/2024/01/data.csv.  | Think of it as the file path in S3. Includes "folders" (which are just key prefixes in S3). 
>
>  
>
>   | Cold Start  | The latency when Lambda initializes a new execution container (imports, connection setup). Usually 1-5 seconds.  | For latency-sensitive workloads, keep Lambda warm with provisioned concurrency. For batch ingest, cold start is fine. 
>
>  
>
>   | Lambda Execution Role  | An IAM role assigned to the Lambda function defining what AWS services it can access.  | Least-privilege: Lambda should only have s3:GetObject, s3:PutObject, s3:DeleteObject on the specific bucket it needs. 
>
>     
>
> ### Bullet 18 — Full-Stack: React.js + Spring Boot + PostgreSQL 
>
>   
>
> "Delivered full-stack experiment tracking features integrating React.js front-ends with Spring Boot REST APIs and PostgreSQL, providing accurate data entry and retrieval across 10+ regulated scientific workflows."
>
>    
>
> #### STAR Story 
>
>  
>
> Situation
>  Beyond building the data pipelines, scientists also needed a web UI to manually enter experiment metadata, search for past experiments, and download reports. The platform needed a front-end connected to a proper REST API — not just a BI dashboard.
>
>  
>
> Task
>  Build full-stack features end-to-end: React.js UI for data entry and search, Spring Boot REST API for business logic, PostgreSQL for persistence.
>
>  
>
> Action — Step by step
>
>   
> -  
>
> Spring Boot REST API:
>  Built CRUD endpoints for experiment management:
>
>   
> - POST /api/experiments — creates a new experiment record with validation (@Valid, @NotNull annotations) 
> - GET /api/experiments/{id}/readings — paginated retrieval of readings for an experiment using Spring Data JPA with Pageable 
> - GET /api/experiments/search?scientist=X&dateFrom=Y&dateTo=Z — parameterized search using Spring Data JPA @Query with JPQL  
>
> Data persistence via Spring Data JPA (Hibernate) — no raw SQL for CRUD operations, JPA generates it. For complex analytical queries (aggregations, window functions), I used native SQL via @Query(nativeQuery=true).
>
>   
> -  
>
> React.js front-end:
>  Used React functional components with hooks:
>
>   
> - useState for form state management 
> - useEffect for fetching experiment data on component mount and on filter changes 
> - useCallback to avoid unnecessary API calls on re-renders  
>
> Search results table with client-side pagination (React useState tracking current page, fetching next page on scroll).
>
>   
> -  
>
> Data entry validation:
>  Validated at three layers:
>
>   
> - Front-end: HTML5 constraint validation + React custom validation hooks (immediate feedback) 
> - API layer: @Valid + Bean Validation annotations (@NotNull, @Size, @Pattern for required format) 
> - Database layer: NOT NULL, CHECK, and UNIQUE constraints in PostgreSQL  
>
> Defense in depth — a bad value rejected at the front-end is UX; rejected at the database is the last line of data integrity.
>
>    
>
> Result
>  Scientists could enter experiment metadata, search historical experiments, and export reports entirely through the web UI — no database access or data team involvement. 10+ regulated workflows supported with proper validation at every layer.
>
>    
>
> ## QUICK REFERENCE — 30-Second Pre-Interview Mental Warm-Up 
>
>    
>
>   | Concept  | One-liner to recall 
>
>    
>
>   | Medallion Architecture  | Bronze (raw) → Silver (clean) → Gold (analytics). Every layer boundary has quality gates. 
>
>  
>
>   | Delta Live Tables  | Declarative Databricks pipeline framework. Define tables as functions. Auto-handles retries, quality, lineage. 
>
>  
>
>   | Delta Lake  | Parquet + transaction log = ACID + time travel + schema enforcement. Makes storage reliable like a DB. 
>
>  
>
>   | dbt  | SQL-only transformation framework. SELECT statements become tables/views. Tests + docs built in. 
>
>  
>
>   | dbt Incremental  | On first run: full build. On subsequent runs: only new rows (watermark filter). 90s vs 20min. 
>
>  
>
>   | Snowpipe  | Snowflake's continuous micro-batch ingest triggered by new file in ADLS/S3. 1-2 min SLA. 
>
>  
>
>   | Snowflake Clustering Key  | Co-locates micro-partitions by key value. Queries on that column scan 5% of data instead of 100%. 
>
>  
>
>   | Dagster vs Airflow  | Dagster = asset-centric (what data). Airflow = task-centric (what work). Dagster is the modern choice. 
>
>  
>
>   | Dagster Asset  | @asset function = a unit of data in the asset graph. Has dependencies, freshness policy, observability. 
>
>  
>
>   | Great Expectations  | Assertion-based data quality. expect_column_not_null, expect_row_count_between, etc. 
>
>  
>
>   | Elementary  | dbt package: stores test results as data over time. Trending + anomaly detection on dbt tests. 
>
>  
>
>   | ADF  | Azure's managed ELT orchestration. Linked Services → Datasets → Pipelines. Good for cloud data movement. 
>
>  
>
>   | Event Hubs  | Azure Kafka equivalent. Partitioned, durable, Consumer Groups for independent readers. 
>
>  
>
>   | Structured Streaming  | Spark's streaming engine. Treat stream as unbounded DataFrame. 30s trigger = micro-batch. 
>
>  
>
>   | Checkpoint  | Spark persists stream progress in ADLS. Crash + restart = resume from last checkpoint, no duplicates. 
>
>  
>
>   | Terraform  | IaC: declare desired infra in HCL, plan to preview, apply to deploy. Reproducible, version-controlled. 
>
>  
>
>   | Key Vault  | Azure secrets management. Never hardcode credentials. Runtime retrieval via SDK or Databricks dbutils.secrets. 
>
>  
>
>   | Unity Catalog  | Databricks governance: Catalog → Schema → Table hierarchy. Column masking, row filters, audit lineage. 
>
>  
>
>   | RBAC (Least Privilege)  | Every user/role has exactly the minimum permissions needed. Nothing more. Limits blast radius. 
>
>  
>
>   | DAX CALCULATE  | Evaluates a measure in a modified filter context. The most important DAX function. 
>
>  
>
>   | DAX DirectQuery  | Power BI queries Snowflake live at render time. Always fresh. Needs Snowflake clustering to be fast. 
>
>  
>
>   | Power BI RLS  | DAX filter by role. Same dataset, each user sees their own tenant's rows. USERPRINCIPALNAME(). 
>
>  
>
>   | Schema Evolution  | mergeSchema=True on Delta write: new source columns auto-added to table. No pipeline failure. 
>
>  
>
>   | Watermark Pattern  | Save max(timestamp) as state. Next run: only process rows newer than watermark. Incremental ELT foundation. 
>
>  
>
>   | Idempotent Write  | Run the same job twice, same result, no duplicates. MERGE/upsert = idempotent. INSERT = not. 
>
>  
>
>   | Z-Ordering  | OPTIMIZE ZORDER BY col — co-locates data with similar values for faster queries on non-partition columns. 
>
>  
>
>   | EXPLAIN ANALYZE (PG)  | Shows actual query execution plan with timings. Seq Scan = missing index. Index Scan = good. 
>
>     
>
> Last updated: 2026-07-06 | Acuity KP — Senior Data Engineer Interview

## Source provenance

- [Original HTML](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Interview%20Prep%20company%20prep%20docs/Acuity%20Kp/Interview_STAR_Stories.html) · Interview Prep company prep docs/Acuity Kp/Interview_STAR_Stories.html
- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Interview%20Prep%20company%20prep%20docs/Acuity%20Kp/Interview_STAR_Stories.md) · Interview Prep company prep docs/Acuity Kp/Interview_STAR_Stories.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
