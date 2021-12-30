Close corrected error
=====================

Corrected errors are marked as closed to let Coderr discard new error reports. 

![](/screens/features/close/close-incident.png)

## Writing a solution

When closing an error, you can include a description where you include details regarding why it happened (root cause) and how you solved it.

A complete description is useful for your team if this error happens again in a future version of your application (we'll display the description directly).

## Enter a version number

Coderr uses this version number to automatically ignore all incoming reports for versions equal or less to the version you specify.

*Do note that we only support semantic versioning. For all other versioning schemes we only ignore errors for the exact same version string.*

Without this feature, the error would be re-opened when a new report arrives for the error.