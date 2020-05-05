Close incidents
================

You close incidents to tell Coderr that it's been corrected.
Once closed, Coderr will ignore all incoming error reports for versions less or equal to the one you specified.

![](/screens/features/close/close-incident.png)

## Writing a solution

When closing an incident you can include a description where you include details regarding why it happened (root cause) and how you solved it.

We recommend that you take time and write a proper description, since it's useful for your team if this error happens again (we'll display the description directly).

## Enter a version number

Coderr uses this version number to automatically ignore all incoming reports that are for versions equal or less to the version that you specify.

*Do note that we only support semantic versioning. For all other versioning schemes we only ignore errors for the exact same version string.*

Without this feature, the incident would be reopened when a new report arrives for the closed incident.