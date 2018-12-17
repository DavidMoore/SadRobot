# Registration-Free COM

## Troubleshooting

### The application has failed to start because its side-by-side configuration is incorrect.

When launching the application, you may see a dialog stating **The application has failed to start because its side-by-side configuration is incorrect. Please see the application event log or user the command-line sxstrace.exe tool for more detail.**

You can create a batch file to make it easier to run, parse and view the SxSTrace:

``
sxstrace.exe Trace -logfile:"%~dp0SxsTrace.trace"
sxstrace.exe Parse -logfile:"%~dp0SxsTrace.trace" -outfile:"%~dp0SxsTrace.txt"
start %~dp0SxsTrace.txt
``
