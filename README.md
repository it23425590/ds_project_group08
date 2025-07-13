<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Distributed Logging System</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 30px;
      line-height: 1.6;
      background: #f9f9f9;
    }
    h1, h2, h3 {
      color: #2c3e50;
    }
    code {
      background: #eee;
      padding: 2px 4px;
      border-radius: 4px;
    }
    table {
      border-collapse: collapse;
      width: 100%;
      margin: 20px 0;
    }
    table, th, td {
      border: 1px solid #999;
    }
    th, td {
      padding: 8px 12px;
      text-align: left;
    }
    .architecture {
      font-family: monospace;
      white-space: pre;
      background: #f4f4f4;
      padding: 10px;
      border-radius: 5px;
    }
  </style>
</head>
<body>

  <h1>Distributed Logging System – Fault Tolerant, Time Synchronized, and Consistent</h1>

  <p>
    This repository contains a robust, fault-tolerant distributed logging system designed and implemented as part of the Distributed Systems (SE2062) module at SLIIT. It integrates techniques in fault tolerance, data replication, time synchronization, and consensus to ensure high availability and consistency across distributed nodes.
  </p>

  <h2>🧠 Overview</h2>
  <p>
    This system ensures reliable log collection and storage across multiple nodes, even in the presence of server crashes or network issues. It leverages a blend of asynchronous replication, NTP-based time synchronization, and a simplified Raft-like consensus algorithm to maintain data integrity.
  </p>

  <h2>🚀 Features</h2>
  <ul>
    <li>Fault-tolerant logging with automatic failover</li>
    <li>Asynchronous data replication across nodes</li>
    <li>Time synchronization using NTP</li>
    <li>Log buffering and reordering to handle out-of-order logs</li>
    <li>Timestamp correction using clock skew compensation</li>
    <li>Lightweight Raft-style consensus for leader election and replication agreement</li>
  </ul>

  <h2>🧱 Architecture</h2>
  <div class="architecture">
Client → Load Balancer → Primary Log Server → Backup Log Servers
                         ↑                    ↑
                 Time Sync (NTP)         Replication + Heartbeats
  </div>
  <ul>
    <li>Logs are first written to a primary server</li>
    <li>Then asynchronously replicated to backup servers</li>
    <li>Nodes synchronize time using NTP</li>
    <li>Uses a simplified Raft protocol for consensus and failover</li>
  </ul>

  <h2>⚙️ Technologies Used</h2>
  <ul>
    <li><strong>Python (FastAPI)</strong> – Web API for logging</li>
    <li><strong>asyncio / heapq</strong> – For asynchronous log buffering</li>
    <li><strong>NTP (ntplib)</strong> – Network Time Protocol integration</li>
    <li><strong>Custom Raft Algorithm</strong> – Consensus and leader election</li>
  </ul>

  <h2>📦 Modules</h2>
  <h3>1. Fault Tolerance</h3>
  <ul>
    <li>Redundant log storage across primary and backup servers</li>
    <li>Automatic failover mechanism detects primary failure and promotes a backup</li>
    <li>Server failure detection via heartbeat and health checks</li>
    <li>Log recovery when a previously failed server rejoins</li>
  </ul>

  <h3>2. Data Replication & Consistency</h3>
  <ul>
    <li>Uses Primary-Backup asynchronous replication</li>
    <li>Eventual consistency model for higher availability</li>
    <li>Deduplication mechanism via UUID/hash check on each log</li>
    <li>Write latency is slightly higher, but read latency remains unaffected</li>
  </ul>

  <h3>3. Time Synchronization</h3>
  <ul>
    <li>All nodes sync using NTP servers like <code>pool.ntp.org</code></li>
    <li>Clock skew analyzed using runtime offset tracking</li>
    <li>Buffered log reordering using a 1-second delay and priority queue</li>
    <li>Timestamp correction based on NTP offset</li>
  </ul>

  <h3>4. Consensus Algorithm</h3>
  <ul>
    <li>Implements a Raft-inspired algorithm for:</li>
    <ul>
      <li>Leader election with randomized timeout</li>
      <li>Heartbeat messages to maintain leadership</li>
      <li>Log replication agreement using AppendEntries RPCs</li>
      <li>Ensures quorum-based commit</li>
    </ul>
  </ul>

  <h2>⚖️ Trade-offs</h2>
  <table>
    <thead>
      <tr>
        <th>Feature</th>
        <th>Advantage</th>
        <th>Trade-off</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Asynchronous Replication</td>
        <td>High availability, fast writes</td>
        <td>Risk of data loss in edge cases</td>
      </tr>
      <tr>
        <td>Frequent NTP Sync</td>
        <td>Accurate timestamps</td>
        <td>Slight network/CPU overhead</td>
      </tr>
      <tr>
        <td>Buffered Log Reordering</td>
        <td>Correct log ordering</td>
        <td>Adds ~1 second delay</td>
      </tr>
      <tr>
        <td>Timestamp Correction</td>
        <td>Better accuracy post-skew</td>
        <td>May apply outdated offset</td>
      </tr>
    </tbody>
  </table>

  <h2>👨‍💻 Contributors</h2>
  <ul>
    <li><strong>Yatawara Y W U M K</strong> – IT23289598</li>
    <li><strong>Katugampala K K V T</strong> – IT23425590</li>
    <li><strong>Udara S M A</strong> – IT23372726</li>
    <li><strong>Sathurusinghe S A K S</strong> – IT23161160</li>
  </ul>

  <h2>📄 License</h2>
  <p>This project was developed as a university assignment. Reuse is allowed with attribution.</p>

  <h2>📬 Contact</h2>
  <p>If you'd like to learn more or collaborate, feel free to reach out to any of the contributors via SLIIT GitHub or student email.</p>

</body>
</html>
