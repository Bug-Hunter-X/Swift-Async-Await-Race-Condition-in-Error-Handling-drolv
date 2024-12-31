# Swift Async/Await Race Condition in Error Handling

This repository demonstrates a potential race condition in Swift's async/await error handling.  The provided code asynchronously fetches data from a URL.  If an error occurs during the data fetch and the `Task` is cancelled before the `catch` block is reached, the error will be swallowed and not logged.

## Problem Description
The `fetchData` function uses `async/await` to fetch data.  The `Task` ensures asynchronous execution; however, if the `fetchData` throws an error, and this task is cancelled before the `catch` block can execute the error handling, the error is never logged. This silent failure is a problem for debugging and monitoring.

## Solution
The solution involves ensuring proper error handling even if the task is cancelled.  This can be accomplished using a `try?` block within the `Task` or by adding a cancellation handler to ensure that the error is caught and handled.