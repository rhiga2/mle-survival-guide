---
title: Databases
author: Ryley Higa
date: 2025-02-03
category: math
ordering: 011
layout: post
---
# Overview
## Data Models Overview
## History and Evolution of Databases
### Pre-relation DBs
### Relational DBs
### NoSQL DBs
* Types of NoSQL DBs:
  *  Document: We store information in a json (or other semi-structured/structured) format. 
  *  Key-value
  *  Graph
 
# Data Structures of DBs
* SSTables 
* B-Trees

# Replication


# Partitioning
* With data-intensive applications, the amount of data will not fit into memory or disk of one node. We need to distribute data across multiple nodes. 

# Transactions
* Multiple read and write operations grouped together as a logical unit.
* Single object writes ex: We want to write a large json object to a database. To do so we should split the writes into chunks within a transaction. 
* Multiple object writes ex: We want to display the number of unread emails, but the query to get that info is expensive. In this case, we use a separate counter to keep track of unread emails. Everytime we want to add a new email to the list we need a transaction to also write the unread email counter.

## ACID
* ACID guarantees may vary between implementations and is mostly a marketing term.
* Atomicity, consistency, isolation, and durability
  * Atomicity: We either execute all operations in a transaction or none at all. Transactions cannot be partially completed when a fault occurs. 
  * Consistency: Application-defined invariants are preserved (this is not the same "consistency" as CAP theorem). The C does not really belong in ACID as C cannot be guaranteed by the DB but is more so related to the application. 
  * Isolation: Running transactions should not see partial results of a concurrent transaction. 
  * Duability: Written data comitted successfully will not be forgotten. This ususally refers to replication. Perfect durability does not exist.
* The alternative to ACID is BASE (Basically Available, Soft state, Eventual consistency)


