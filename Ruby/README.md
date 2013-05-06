# Ruby
---

## TO SORT

### How to get UTC timestamp

``` ruby
time = Time.now.getutc
```

difference between two times is in seconds

>The difference between DATETIME and TIMESTAMP is a bit more subtle: 
  - DATETIME is formatted as YYYY-MM-DD HH:MM:SS. Valid ranges go from the year 1000 to the year 9999 (and everything in between. 
  - While TIMESTAMP looks similar when you fetch it from the database, it's really a just a front for a unix timestamp. Its valid range goes from 1970 to 2038. 
>The difference here, aside from the various built-in functions within the database engine, is storage space. Because DATETIME stores every digit in the year, month day, hour, minute and second, it uses up a total of 8 bytes. As TIMESTAMP only stores the number of seconds since 1970-01-01, it uses 4 bytes.


## References

- [In Ruby on Rails, what's the difference between DateTime, Timestamp, Time and Date?](http://stackoverflow.com/questions/3928275/in-ruby-on-rails-whats-the-difference-between-datetime-timestamp-time-and-da)