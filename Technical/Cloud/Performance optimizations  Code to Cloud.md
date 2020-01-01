# Performance optimizations : Code to Cloud

# Tips & Tricks

- Task Parallel Library(TPL)
  - ConfigureAwait(false)
    - [ConfigureAwait FAQ](https://devblogs.microsoft.com/dotnet/configureawait-faq/) Why would I want to use ConfigureAwait(false)?
    - **if you’re writing app-level code, \*do not\* use `ConfigureAwait(false)`**
    -  **if you’re writing general-purpose library code, use `ConfigureAwait(false)`**
  - 