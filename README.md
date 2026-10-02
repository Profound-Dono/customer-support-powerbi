# Customer Support Operations & Service Quality Dashboard

## Overview

This project analyzes a synthetic customer support ticket dataset using Microsoft Power BI.

The goal was to investigate support workload, response-time performance, SLA compliance, ticket resolution, reopened tickets, and customer satisfaction.

The dashboard is designed to answer practical operational questions that a support or customer-experience team could use to monitor service quality and identify areas for further investigation.

## Business Questions

The analysis focuses on four areas:

### Executive Overview

* How many support tickets are being handled?
* What proportion of responded tickets breach the SLA?
* How quickly are customers receiving their first response?
* Which priorities, channels, and queues generate the most workload?

### Operations

* Which priorities have the highest SLA breach rates?
* Which queues have the slowest first-response times?
* Which queues have the longest resolution times?
* Where are unresolved tickets accumulating?
* Which queues generate the most reopened tickets?

### Customer Experience

* How does CSAT differ between queues?
* How does CSAT differ by priority?
* Is slower first response associated with lower CSAT?
* How many tickets received a CSAT response?

## Dataset

The project uses the Datanemics Customer Support Tickets dataset.
The dataset contains 4,000 synthetic customer support tickets covering January 2023 through February 2024.
Each row represents one support ticket.

### Main fields

* `ticket_id` — unique ticket identifier
* `opened_at` — ticket creation timestamp
* `channel` — support channel
* `queue` — support queue
* `priority` — ticket priority
* `subject` — ticket subject
* `first_response_min` — first response time in minutes
* `resolved_at` — ticket resolution timestamp
* `reopened` — whether the ticket was reopened
* `csat` — customer satisfaction score

## Data Preparation

Data preparation was performed using Power Query.

The main preparation steps included:

1. Importing the CSV dataset into Power BI.
2. Renaming the main table to `FactTickets`.
3. Correcting data types.
4. Creating `first_response_hours` from `first_response_min`.
5. Creating `resolution_hours` from `opened_at` and `resolved_at`.
6. Creating SLA target hours based on ticket priority.
7. Classifying tickets as `Met`, `Breached`, or `No Response`.
8. Creating dimension tables for channel, queue, and priority.
9. Creating a date table for the Power BI data model.
10. Creating a one-to-many relationship from the dimension tables to the ticket fact table.

## SLA Assumptions

For analytical purposes, the following first-response targets were used:

| Priority | SLA Target |
| -------- | ---------: |
| Urgent   |    4 hours |
| High     |    8 hours |
| Normal   |   24 hours |
| Low      |   48 hours |

These targets are analytical assumptions created for this project and are not presented as official service-level agreements from the dataset provider.

Tickets without a recorded first response are classified separately as `No Response` rather than being treated as SLA breaches.

## Data Model

The Power BI model uses a fact-and-dimension structure.

### Fact table

`FactTickets`

### Dimension tables

* `DimDate`
* `DimChannel`
* `DimQueue`
* `DimPriority`

The dimension tables filter the `FactTickets` table through one-to-many relationships.

## Key Metrics

The dashboard includes:

* Total Tickets
* Resolved Tickets
* Open Tickets
* Resolution Rate
* Median First Response Hours
* Median Resolution Hours
* SLA Breach Rate
* Average CSAT
* Reopened Tickets
* Reopened Rate
* CSAT Responses
* CSAT Response Rate

Median response and resolution times were used instead of averages where appropriate because response and resolution times can be strongly affected by unusually long cases.

## Dashboard Structure

### 1. Executive Overview

The Executive Overview provides a high-level view of:

* Ticket workload
* SLA performance
* First-response performance
* Customer satisfaction
* Tickets by priority
* Tickets by channel
* Tickets by queue

### 2. Operations

The Operations dashboard investigates:

* SLA breach rate by priority
* Median response time by queue
* Median resolution time by queue
* Open tickets by queue
* Reopened tickets by queue

### 3. Customer Experience

The Customer Experience dashboard investigates:

* Average CSAT by queue
* Average CSAT by priority
* Response time versus CSAT
* CSAT response coverage

## Key Findings

### 1. Response performance varies across support operations

SLA breach rates and median response times vary across priorities and queues, providing areas for further operational investigation.

### 2. A measurable unresolved workload remains

225 of the 4,000 tickets in the dataset were unresolved at the time of analysis, representing approximately 5.6% of all tickets.

### 3. CSAT coverage is limited

CSAT was available for 1,226 of the 4,000 tickets, representing approximately 30.7% of the dataset.

Therefore, CSAT results should be interpreted as survey-based results rather than as a complete representation of all tickets.

## Recommendations

1. Investigate SLA performance by priority and queue to identify areas requiring operational review.

2. Review queues with the largest unresolved backlogs and investigate whether workload, ticket complexity, or resolution processes contribute to the backlog.

3. Increase CSAT survey coverage to provide a larger sample for customer-experience analysis.

4. Investigate the relationship between first-response time and CSAT while avoiding causal conclusions from this dataset alone.

## Tools Used

* Microsoft Power BI
* Power Query
* DAX
* Data modelling
* Data visualization
* Exploratory data analysis

## Limitations

The dataset is synthetic rather than production customer-support data.

The SLA targets used in this project are analytical assumptions.

CSAT is missing for a substantial proportion of tickets, so customer-experience results should be interpreted with this limitation in mind.

The analysis identifies relationships and operational patterns but does not establish causal relationships.

## Project Outcome

This project demonstrates my ability to take a raw support dataset, prepare and model the data, create business metrics, build an interactive Power BI dashboard, identify operational patterns, communicate limitations, and translate analysis into practical recommendations.
