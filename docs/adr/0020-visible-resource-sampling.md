# ADR 0020: Share visible resource sampling and policy observations

Status: Accepted

Date: 2026-09-08

Preferences consumes the shared resource snapshot with a short freshness budget. Sampling stops when its resource pane or document is hidden and resumes on visibility. A pending sample is not overlapped. Sidebar and preferences observe policy changes through the resource service and unsubscribe when detached.

The development frontend build and focused browser checks passed for pane sampling and external policy changes. This does not establish a measured CPU/RAM saving or complete consolidation of all optional resource monitors. Search-region state synchronization remains a separate open issue.
