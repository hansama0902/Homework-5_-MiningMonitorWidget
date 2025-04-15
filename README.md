# MiningMonitorWidget - Usage Guide

This document explains the purpose, usage, options, and examples for using the MiningMonitorWidget component inside Observable notebooks.

## Purpose

The MiningMonitorWidget is a custom visual component for monitoring the operational status of mining machines. It provides interactive filtering, summary visualization, and key statistics such as average temperature and hashrate. The widget is useful in real-time dashboards where users need to quickly identify machine performance and detect problems.

---

## Observable Notebook Link

[Link to Observable Notebook](https://observablehq.com/d/17ad2f133c3f874a)


---
## How to import it on Observable

You can define the widget directly in a notebook by copying the MiningMonitorWidget function. If you have published it in another notebook, you can import it using:

import { MiningMonitorWidget } from "Shuhan Dong/MiningMonitorWidget"

This will make the widget available as a reusable component. Observable’s reactive runtime will handle reactivity and input binding automatically.

---

## How to load data (CSV)

To load your mining machine data, you can upload a file named `completed_mining_machine_table.csv` (or any other valid CSV), and use the following method:

viewof uploadedMachines = {
  const file = await FileAttachment("simple.csv").csv({typed: true});
  const container = html`<div></div>`;
  container.value = file;
  return container;
}

The CSV should contain fields like: `id`, `name`, `status`, `temperature`, `hashrate`, `uptime`, `location`.

## How to use in Observable

To use this widget in Observable, define or import the MiningMonitorWidget function in your notebook. You will also need to provide a dataset (such as a CSV file with mining machine data) and connect a status filter input to the widget.

Observable notebooks support reactive connections, so the widget works with Inputs.checkbox and Inputs.bind for seamless interactivity. After the setup, the widget will automatically update its display when the selected statuses or data change.

## Optional: Using outside of Observable

While the widget is designed specifically for Observable, it can be adapted for other JavaScript environments with some changes. For example, instead of relying on Inputs.bind and viewof, you can use standard event listeners and state management in frameworks like React or Vue.

## Widget Configuration Options

The widget accepts the following configuration options:

- `machines` (Array): A list of mining machine objects. Each object should contain fields like id, name, status, temperature, hashrate, etc.
- `initialStatuses` (Array): A list of available status values to filter by.
- `colorMap` (Object): A mapping of status names to colors used in charts and status tags.
- `maxTableEntries` (Number): Limits the number of machines displayed in the filtered table.
- `title` (String, optional): The heading displayed at the top of the widget.
- `showSummaryChart` (Boolean, optional): Whether to show the status bar chart.
- `showFilteredTable` (Boolean, optional): Whether to show the filtered machine table.

---


## Example CSV (completed_mining_machine_table.csv)

id,name,status,temperature,hashrate,uptime,location
miner-1,Mining Rig 1,Online,65,85,240,Room 1
miner-2,Mining Rig 2,Offline,52,0,0,Room 2
miner-3,Mining Rig 3,Overheated,82,45,180,Room 1
miner-4,Mining Rig 4,Underperforming,70,30,120,Room 2

---

## How it works

The widget listens for changes in a connected status input. When the user changes the selected statuses, the widget updates the summary chart, table, and stats. The data must be preloaded and passed in through the `machines` option. Using Inputs.bind allows the widget to synchronize its internal state with external controls. This setup creates a flexible, reactive, and user-friendly monitoring panel for dashboard applications.


1. A summary chart that shows the proportion of each status.
2. A table listing the machines that match the selected statuses.
3. A statistics bar showing the count of selected machines and average values.

When connected using `Inputs.bind()`, it stays synchronized with external filters. This makes it ideal for dashboards where multiple views must stay in sync.

---
## Bluesky

[Link to Tweet](https://bsky.app/profile/shuhandong.bsky.social/post/3lmv52dasjc2f)

---

## License

MIT License. Free to use and adapt.
