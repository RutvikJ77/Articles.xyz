---
title: "Fact Modeling: The easy way out"
seoTitle: "Effortless Fact Modeling Techniques"
seoDescription: "Explore fact modeling, its challenges, and high data volume management using normalization and denormalization techniques"
datePublished: Mon Feb 03 2025 04:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6ut1i1a000309lbcakr7r6u
slug: fact-modeling-the-easy-way-out
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1738934963090/1d973fb8-9d0e-43b3-9e32-107d03ae4c9e.png
tags: analytics, data, dataengineering

---

*This article is based on my learnings and the content from Zach Wilson’s Data Engineering YouTube bootcamp.*

### TLDR;

This article explores the concept of fact modeling in data engineering, highlighting the distinction between facts and dimensions. It discusses the challenges of high data volume and granularity, and compares normalization and denormalization approaches for structuring data. The article also suggests methods like sampling, bucketing, streaming, and micro-batching to manage data volume and duplication. It provides guidance on identifying facts versus dimensions and offers questions to consider when engaging in fact modeling.

---

## Facts aka the truth

Computer science is a rational field, rooted deeply in fundamental logical thinking and mathematics. The reason I mention this, is for you to observe the patterns of reality and correlate with the learning.

The above 2 sentences have both a fact and a dimension. Facts are atomic i.e they cannot be broken down further. Dimensions on the other hand are descriptive and contextual to facts.

Truth always has challenges attached to it, primarily 2 in our case:

1. The more you observe, the more you capture = High Volume / Data
    
2. The more you capture, the more is the context required = High granularity & hence more duplicates
    

### Fact not so vs. Dimensions

Prior to solving on the challenges, let me share about the 1v1 battle between Facts and Dimensions. This tussle is not ordinary since fact will always be dependent on the context/dimension. To table it out:

| **Factor** | **Facts** | **Dimensions** |
| --- | --- | --- |
| Basics | Something that happened (transaction, event) | The object to which something happened (player, team, categories) |
| Volume | 10 - 100X of dimensional tables - due to detailed records | Much smaller as they store distinct values |
| Immutability | Immutable - It is what it is - once recorded, it is part of history | Mutable - change in team name, change in location |
| Appearance | Like Onion - has many layers which can be used for aggregations and calc. | Like Knife - slice and dice your “onion” using filtering, grouping and more. |

Each fact has 4 dimensions associated with it - Who, Where, When and How. To illustrate this take an example of you travelling for vacation to Hawaii.

**Fact:** You booked a flight.

**Dimensions:**

1. **Who:** You, the passenger who booked the flight has an ID associated.
    
2. **Where:** The departure and arrival locations of your flight. For example, departing from Los Angeles International Airport (LAX) and arriving at Daniel K. Inouye International Airport (HNL).
    
3. **When:** The date and time of your scheduled flight probably May 15, 2025, at 10:00 AM.
    
4. **How:** The class of service and method of booking. Giving you an upgrade to Business Class which you booked through a website.
    

### Approaches

Back from the imaginary vacation, Fact Modeling has 2 approaches to structure and store the data:

* **Normalization** - organizing data to reduce redundancy and ensure data integrity
    
    * Not having any dimensional attributes, just IDs to join on.
        
* **Denormalization** - adding redundant data to improve read performance and simplify queries.
    
    * Brings additional dimensional attributes with more storage.
        

To determine the right approach question about:

* Query performance requirements
    
* Data integrity needs
    
* Reporting and analysis demands
    

### Solving for Challenges

Drawing back to the challenges, to solve for higher volume of data methods of sampling and bucketing are advised. To resolve for duplication, Streaming and Micro-batching are suggested.

| **Sampling** | Selecting a subset from the entire dataset. Best used for metric driven values. |
| --- | --- |
| **Bucketing** | Grouping similar values together aka binning. Often performed using one of the impactful dimension ensuring faster joins. |
| **Streaming** | Processing data continuously as it arrives while maintaining the selection window and ideally an interval of 15 mins. |
| **Microbatching** | Batch + Stream processing hybrid approach. Dividing the data streams into small batches and treating them as micro jobs. The resulting graph looks like horizontal decision tree or like a “share” button |

The above ones are algorithmic methods that can be implemented, on an analytical scale, root cause analysis (identifying the issues with data quality or performance) and gap analysis (comparing the current state with the desire state to identify improvements) can be conducted to identify the potential reduction of volume in data.

TLDR; of Root Cause and Gap Analysis shared below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738872314531/5dcabd46-9316-4bfd-ad04-f8056f9cf3a9.png align="center")

## Is it a fact or dimension?

To identify if a record is a fact or dimension ask yourself:

“Does this record represent a measurable event or transaction (fact), or does it provide descriptive context for such events (dimension)?”

And when looking to analyze the records, **have a reason associated** with every step undertaken because “I feel like this should be the case” falls flat with your colleagues and the stakeholders.

---

## Questions to ask

Use the below questions as a reference, the next time you think for fact modeling:

1. What specific business questions do we need the fact data to answer?
    
2. Which dimensions are essential for providing context to the facts?
    
3. How will we ensure the accuracy and consistency of the fact data over time?
    

I appreciate your time reading through this. In the next article, I’ll share my learnings on Analytical Patterns. Stay curious!