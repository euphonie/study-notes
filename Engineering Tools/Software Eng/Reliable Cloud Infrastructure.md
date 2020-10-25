
# Reliable Cloud Infrastructure

> Template: [Design and Process Workbook from Google ](https://docs.google.com/presentation/d/1gg6PTfgLNqh6CKXZ-k-HjHGKq5n3uz9OBXBG_K43TC4/edit?usp=sharing)

## Steps

### 1. Defining a case study
- Add a brief description
- List a few main features
- List roles of typical users

### 2. Requirements, analysis and design

**Requirements analysis**
| Who | Determining not only the user of the system, but developers and stake holders. Who the systems affects directly and indirectly  | Who are the user? Who are the developers? Who are the stakeholders? |
|--|--|--|
| What | Establish the main areas of functionality required in a clear unambiguous manner | What does the system do? What are the main features?|
| Why | What is a problem the proposed system aims to address or solve? Without a clear understanding extra requirements will certainly be added. This will potentially help in defining KPIs, SLOs and SLAs | Why is the system needed? |
| When | Helps determine a realistic timeline and can help contain the scope | When do the users need and/or want the solution? When can the developers be done? |
| How | Helps determine non-functional requirements | How will the system work? How many users will there be? How much data will there be?  |

**Roles**
- Represet the goal of a user
- Are not people or job titles
	- People and roles have a many to many relationship
	- Should describe a users objective. What does the user want to do?
- For more important roles a **Persona** can be created
	- Is an imaginary representation of a user role
	- Personas tell a story of who they are
	- Describe a feature from the user's point of view
		- Give each story a title that describes its purpose
		- Write a short, one sentence description
		- Specify the user role, what they want to do, and why
		- Use the template: As a [role], I want to..., so that I can....
			- Alternative: Given...[context], When I do...., then .... should happen.
		- Ex. **As an** account holder, **I want to** check my available balance at any time of day **so** I am sure not to overdraw my account

**Invest Criteria for evaluating user stories**
- INVEST
	- **Independent**. Prevent problems with priorization and planning
	- **Negotiable**. Used to stimulate discussion between customer and developers until there is a clear agreement, they add collaboration.
	- **Valuable**. Stories should provide value to users. Think about outcome impact, not outputs and deliverables.
	- **Estimatable**. If is not estimatable, there are missing details or the story is too large.
	- **Small**. Keeps scope small and less ambiguous, supports fast feedback
	- **Testable**. This way developers can verify that the story has been implemented correctly and validate when requirement has been met/ is done.

**KPIs**
- Metrics that can be used to measure success
- Not the same as a goal or objective, the goal is the outcome or result wanted to be achieved, the KPI is a metric that indicates whether you are on track to achieve the goal
- For each KPI, define targets for what success looks like, allows readjustment based on monitoring and feedback
- To be must effective they should be accompanied by a goal
- Common Business KPIs
	- Return on Investment, ROI
	- Earnings before interest and taxes, EBIT
	- Employee turnover
	- Customer churn
- Common Software (Technical) KPIs
	- Page views
	- User registrations
	- Clickthroughs
	- Checkouts
- Must be SMART
	- Specific
	- Measurable. Monitoring can indicate if you're moving towards or away from the goal
	- Achievable
	- Relevant. Does it really matter to the user? Will it help achieve application goals?
	- Time-bound. Helps measing the KPI. Per year/month/day?

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzg1NzI2MjgyLDEzMzcwODUwNDUsLTE2OD
Q1NDk5OV19
-->