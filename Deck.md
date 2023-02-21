---
marp: true
paginate: true
class: invert
theme: default
---

# VS Performance Profiling and Diagnostic Tools

Tools in Visual Studio to help you find and fix performance issues in your code.

---

# Why Profiling? 

- Find memory leaks, and general performance issues
- Detect and Fix hard to find bugs and performance issues
- Fine-Tune and Improve app performance
- Find issues related to external libraries and dependencies

---

# Common Peformance Issues

- Mishandling CPU time
   - Misusing async patterns and threading - I/O bound vs CPU bound
   - Caching issues specially when dealing with apis
- Memory Issues
   - Memory leaks - not disposing of objects
   - Using too much memory specially when dealing with Lists
   - Issues around GC - may happen too often
 - External dependencies
   - Network or File system issues
   - Database issues
   - 3rd party libraries

---

# Performance Collection Methods

- **Sampling**:
  Collects statistical data about the work that is performed by an application during profiling. Least impact on performance
- **Tracing**:
  provides better information on how often a method was executed. If you need accurate measures of call numbers, use tracing. Huge Impact on performance
- **Instrumentation**
  Collects detailed information about the work that is performed by an application during a profiling run. Data collection is done by tools that either inject code into a binary file that captures timing information or by using callback hooks to collect and emit exact timing and call count information while an application runs. high overhead when compared to sampling-based approaches

<!--The value of sampling is that it has less overhead and for this reason is more likely to be statistically representative of the application running in production. The value of instrumentation profiling is that you can get exact call counts on how many times your functions were called. This gives you much more detailed information than normal sampling, which can distort the time taken in some scenarios. For example, functions that don't do much, but are called frequently, will show up more than they would in a real world scenario.

With instrumentation, every function call selected in your application is annotated and instrumented so that when it gets invoked it's added to the trace along with information about the caller. With sampling, the current call stack executing is polled from the CPU at an interval and then each frame is added to the trace.

-->

---

# Tools in Visual Studio

- Visual Studio Diagnostics Tools and PerfTips (While Debugging)
- Visual Studio Performance Profiler (Standalone Suite Alt+F2 in VS or CMD)
  - CPU Usage
  - Memory Profiler
  - Async Profiler
  - Databases
  - .NET performance counters
  - Event Viewer

---

![bg right h:100%](media/diagnostictools-update1.png)

# Diagnostic Tools

Breakpoints and associated timing data gets recorded in the Diagnostic Tools window.

---

![bg right w:100%](media/dbgdiag_perf_perftip.png)

# PerfTips
When the debugger stops execution at a breakpoint or stepping operation, the elapsed time between the break and the previous breakpoint appears as a tip 

---

![bg left](https://picsum.photos/1080?image=1)

# Demo

Demonstrate Diagnostic Tools  vs Performance Profiler

<!--
Open Visual Studio Run AspNetCoreDiagnosticScenarios in Debug Mode to show Diagnostic Tools, emphasis on debugging overhead process and how useful it will be. Quickly mention perf tips when breakpoint is hit.  
Also mention Alt + F2 Main performance profiler tools which works best in Release Mode. It can be shipped as command line stand alone tool for capturing live app in prod and then transferred and analysed in VS
-->

---

![bg right w:100%](media/cpu-use-lib-choose-cpu-usage.png)

# CPU Usage

One of the main tools in Performance profiler suite.

---

# The CPU Usage tool 

- Diagnose a slow-down or a process hang in your team’s codebase.

- Identify in timeline where CPU should be working and isn't or vice versa

- Identify performance issues in DevOps scenarios, such as when a customer reports that some requests or orders are not getting through to the retail website during peak season.

- If your latency issue isn’t within an API request, then you can check for high CPU utilization and other related issues with the CPU Usage tool. The CPU Usage tool can help you identify bottlenecks so that you can narrow down where to optimize.

<!--
The tool can help you diagnose the issue with your team’s production code. The tool provides automatic insights and various views of your data so that you can analyze and diagnose performance issues.

Often, the issues are in production, and it is challenging to debug at that moment, but this tool can help you capture enough information and evidence of the issue. After collecting a trace file, the analysis can quickly help you understand potential causes and give suggestions within the context of your code so that you can take the next steps to fix the issue.
-->

---

![bg w:100%](media/cpu-use-wt-report.png)

---
<!--  class: invert -->

|Name|Description|
|-|-|
|**Total&nbsp;CPU**|![Total % data equation](media/cpu_use_wt_totalpercentequation.png "CPU_USE_WT_TotalPercentEquation")<br/>The milliseconds and CPU percentage used by calls to the function, and functions called by the function, in the selected time range.  |
|**Self&nbsp;CPU**|![Self % equation](media/cpu_use_wt_selflpercentequation.png "CPU_USE_WT_SelflPercentEquation")<br /> The milliseconds and CPU percentage used by calls to the function in the selected time range, excluding functions called by the function.|
|**Module**|The name of the module containing the function.

---

![bg w:100%](media/cpu-use-wt-call-tree-annotated.png)

---

|Image|Description|
|-|-|
|![Step 1 w:40](media/procguid_1.png "ProcGuid_1")|The top-level node in CPU Usage call trees is a pseudo-node.|
|![Step 2 w:40](media/procguid_2.png "ProcGuid_2")|In most apps, when the **Show External Code** option is disabled, the second-level node is an **[External Code]** node. The node contains the system and framework code that starts and stops the app, draws the UI, controls thread scheduling, and provides other low-level services to the app.|
|![Step 3 w:40](media/procguid_3.png "ProcGuid_3")|The children of the second-level node are the user-code methods and asynchronous routines that are called or created by the second-level system and framework code.|
|![Step 4 w:40](media/procguid_4.png "ProcGuid_4")|Child nodes of a method have data only for the calls of the parent method.|

---

![bg right w:100%](media/cpu-use-wt-call-tree-view.png)

# Detailed CPU Usage View

- Caller/Callee
- Call Tree
- Modules
- Functions
- Flame Graph

---

![bg left](https://picsum.photos/1080?image=1)

# Demo

Demonstrate Performance Profiler CPU Usage

<!--
Open Visual Studio Run AspNetCoreDiagnosticScenarios in Debug Mode to show Diagnostic Tools, emphasis on debugging overhead process and how useful it will be. Quickly mention perf tips when breakpoint is hit.  
Also mention Alt + F2 Main performance profiler tools which works best in Release Mode. It can be shipped as command line stand alone tool for capturing live app in prod and then transferred and analysed in VS
-->

---

![bg right h:100%](media/memory-usage-start-diagnostics-session.png)

# Memory Usage

You can use the tool to study the real-time memory effects of scenarios you're actively developing in Visual Studio

---

![bg w:100%](media/memory-usage-report-overview-1-vs-2022.png)

---

![bg w:100%](media/memory-usage-snapshot-view-numbered-vs-2022.png)

---

|Image|Description|
|-|-|
|![Step 1 w:40](media/procguid_1.png "ProcGuid_1")|Total number of objects in memory when the snapshot was taken. Select this link to display a snapshot details report sorted by the count of instances|
|![Step 2 w:40](media/procguid_2.png "ProcGuid_2")| Difference between the total number of memory objects in this snapshot and the previous snapshot. Select this link to display a snapshot diff report sorted by the difference in the total count of instances|
|![Step 3 w:40](media/procguid_3.png "ProcGuid_3")| Total number of bytes in memory when the snapshot was taken. Select this link to display a snapshot details report sorted by the total size|
|![Step 4 w:40](media/procguid_4.png "ProcGuid_4")| Difference between the total size of memory objects in this snapshot and the previous snapshot. positive or negative number means the memory size of this snapshot is larger or smaller than the previous one.|

---

![bg right w:100%](media/dotnetalloctoolselected.png)

# Object Allocation Tool

You can see how much memory your app uses and what code paths allocate the most memory by using the .NET Object Allocation tool.

---

![bg w:100%](media/graphdotnetalloctimefiltered.png)

---

![bg w:100%](media/allocationexpandedlight.png)

---

![bg left](https://picsum.photos/1080?image=1)

# Demo

Demonstrate Memory Usage and Object Allocation Tracking

---

![bg right w:100%](media/async-tool-selected.png)

# .NET Async Tool

Use the .NET Async tool to analyze the performance of asynchronous code in your app.

---

![bg w:100%](media/async-tool-gotosource.png)

---

![bg left](https://picsum.photos/1080?image=1)

# Demo

Demonstrate .NET Async Tool

---

![bg right w:100%](media/db-launch.png)

# Database Tool

Use the Database tool to record the database queries that your app makes during a diagnostic session. You can then analyze information about individual queries to find places to improve your app's performance.

---

![bg w:100%](media/db-gotosource.png)

---

![bg left](https://picsum.photos/1080?image=1)

# Demo

Demonstrate Database Tool

---

![bg right w:100%](media/dotnet-counters-tool-selected.png)

# .NET Counters

The .NET Counters tool allows you to visualize dotnet counters over time right from within the Visual Studio profiler.

---

![bg w:100%](media/dotnet-counters-tool-report.png)

---

![bg left](https://picsum.photos/1080?image=1)

# Demo

Demonstrate .NET Counters

---

![bg right w:100%](media/eventsviewerselected.png)

# Event Viewer

In the Performance Profiler, you can collect diagnostic info while your app is running, and then examine the collected information after the app stops like a post-mortem analysis.

---

![bg w:100%](media/eventvieweraddcolumns.png)

---

|Column name|Description|
|----------|---------------------|
|Provider Name|The event source|
|Event Name|The event as specified by its provider|
|Text|Descriptions of the provider, event name, and ID for the event|
|Timestamp (ms)|When the event took place|
|Provider Guid|The ID of the event provider|
|Event ID|The ID of the event|
|Process ID|The process from which the event occurred (if known)|
|Process Name|The name of the process if it's actively running|
|Thread ID|The ID of the thread from which the event occurred (if known)|

---

![bg left](https://picsum.photos/1080?image=1)

# Demo

Demonstrate Event Viewer

---
<!--  class: marp -->
## Any Questions?

![bg right](https://picsum.photos/1080?image=237)


---
<!--  class: invert -->

# Links

- Youtube Series (aka.ms/vsprofilerseries)
- GitHub Repo (github.com/davidfowl/AspNetCoreDiagnosticScenarios)
- Documentation (learn.microsoft.com/en-us/visualstudio/profiling)
- Sysinternals for Windows (docs.microsoft.com/en-us/sysinternals)
- Sysinternals for Linux (github.com/Sysinternals)
