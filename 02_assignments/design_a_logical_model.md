# Assignment 1: Design a Logical Model

## Question 1
Create a logical model for a small bookstore. 📚

At the minimum it should have employee, order, sales, customer, and book entities (tables). Determine sensible column and table design based on what you know about these concepts. Keep it simple, but work out sensible relationships to keep tables reasonably sized. Include a date table. There are several tools online you can use, I'd recommend [_Draw.io_](https://www.drawio.com/) or [_LucidChart_](https://www.lucidchart.com/pages/).

## Question 2
We want to create employee shifts, splitting up the day into morning and evening. Add this to the ERD.

## Question 3
The store wants to keep customer addresses. Propose two architectures for the CUSTOMER_ADDRESS table, one that will retain changes, and another that will overwrite. Which is type 1, which is type 2?

_Hint, search type 1 vs type 2 slowly changing dimensions._

Bonus: Are there privacy implications to this, why or why not?
```
Proposed architecture 1 – This one is to overwrite changes and is therefore Type 1 SCD. This means that whenever a customer’s address gets updated, the old address gets overwritten by the new address and the table always contains the current address for a particular customer. 

Changes to the existing ERD: Customer table will have a field called address_id instead of customer_address and will have a many to one relationship to the address-id field in the new table Address. There is a last_updated field to keep track of when the address was last modified.

New_Table: Address
Columns: Address_id
         Street
         City
         State
         Postal_code
         Last_updated 

Proposed architecture 2 – This one is to retain changes and is therefore Type 2 SCD. This means that whenever a customer’s address changes, the old address(es) are retained, and a new row gets added to store the new address for a particular customer.

Changes to the existing ERD: Customer table will have a field called address_id instead of customer_address and will have a many to one relationship to the address-id field in the new table Address. Instead of the last_updated field, there is a is_current field to keep track of the current address.

New_Table: Address
Columns: Address_id
         Street
         City
         State
         Postal_code
         Is_current

Privacy implications – Type 1 minimizes the amount of personal information stored which is good for privacy as it reduces the risk of exposure in the event of a data breach. But it does not provide a history of address changes, which can be required for legal compliance. On the other hand, Type 2 stores a complete history of addresses for every customer, which is good for compliance purposes. But it requires more storage and increases the amount of personal information stored, thereby increasing privacy risks. So, there is a trade-off between more information and privacy risks.


```

## Question 4
Review the AdventureWorks Schema [here](https://i.stack.imgur.com/LMu4W.gif)

Highlight at least two differences between it and your ERD. Would you change anything in yours?
```

AdventureWorks uses best practices in database design, namely segmentation and normalization, to create a robust and detailed schema.

2 differences – 
Segmentation: AdventureWorks ERD is divided into multiple schemas, Sales, Purchasing, Person, Production, HumanResources, and dbo, which helps organize the database logically. Bookstore ERD is more simplified in nature and consists of a single schema probably because AdventureWorks is a much bigger application than what has been envisaged for Bookstore. 

Normalization: AdventureWorks ERD is highly normalized, seems like 3NF to me. Bookstore ERD uses a moderate level of normalization, 2NF to a large degree but not fully compliant.  

Changes to the proposed Bookstore ERD
With more time and information, I would like to make the Bookstore ERD as segmented and detailed as AdventureWorks with complex relationships rather than the simple relationships as proposed in the Bookstore ERD. Similarly, I would make changes to the Bookstore ERD to ensure that it complies with 3NF to eliminate redundancy. 




# Criteria

[Assignment Rubric](./assignment_rubric.md)

# Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `June 1, 2024`
* The branch name for your repo should be: `model-design`
* What to submit for this assignment:
    * This markdown (design_a_logical_model.md) should be populated.
    * Two Entity-Relationship Diagrams (preferably in a pdf, jpeg, png format).
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sql/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `model-design`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-3-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
