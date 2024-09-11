

|  **Attribute**  |  **Definition**  |  **Details**  |  **Release Version**  | 
|  --- |  --- |  --- |  --- | 
| ContainsUserData | type: “boolean”, required: true, defaultValue: false | true, if response to the question contains user personal information. All such responses will not be indexed into druid and will be available as data exhaust (for a configured duration). | R3.4 | 
| SetType | type: “string”, required: true, “enum”: \[“materialised”, “dynamic”], defaultValue: “materialised“ | <ul><li>materialised - all questions in the set are fixed and added by the creator

</li><li>dynamic - questions in the set are dynamically fetched using a criteria

</li></ul>R3.4 Scope: “materialised“ sets only | R3.4 | 
| SetCriteria | type: “json”, required: false | Criteria to be used when the set type is dynamic. |  | 
| Feedback | type: “json”, required: false, format: {“id1”: {“language_1“: “feedback_html“}, “id2”: “feedback_html“} | Feedback shown to the users after response processing. Feedback is a JSON object in key-value format, keys in the JSON are the identifiers of different feedbacks for the question set and values are HTML snippet to be shown to the user. After the response processing, the QuML player renders the feedback HTML mapped to the value that is set to the FEEDBACK outcome variable.Similar to “body”, feedback in different languages can be configured. |  | 
| NavigationMode | type: “string”, required: true, enum: \["linear", "non-linear"],  defaultValue: “non-linear“ | <ul><li>A question set in linear mode restricts the user to attempt each question in turn. Once the user moves on they are not permitted to return.

</li><li>A question set in nonlinear mode removes this restriction - user is free to navigate to any question in the question set at any time.

</li></ul> | R3.4 | 
| AllowSkip | type: “boolean”, required: true, defaultValue: true | Allows the user to skip a question or question set within the question set. |  | 
| QuestionSet Structure |  | QuestionSet template to control types of questions, behaviour, default configurations for editors. |  | 
| Questions | { ”identifier”: “identifier of the member question“, ”index”: “sequence index“, ”required”: true/false, ”weightage”: “defaults to 1. if 0, this question is skipped while computing the overall score“, ”objectType”: “Question“ } | Questions associated with the question set.R3.4 scope: - required: false - weightage: out of scope | R3.4 | 
| QuestionSets | { ”identifier”: “identifier of the member question set“, ”index”: “sequence index“, ”required”: true/false, ”weightage”: “weightage for this question set in the overall score. if 0, this question set is skipped while computing the overall score“, ”shuffle”: “true/false - if questions in the member question set should be shuffled or not when presented to the user”, ”totalQuestions”: “total number of questions in the member question set“, ”maxQuestions”: “number of questions in the member question set that should be used in one session“, ”preConditions”: “conditions to be validated before rendering the question set. generally depends on the outcomes of question sets presented earlier in the session“, ”branchRules”: Evaluated after question set is complete and jumps forward to the specified target, ”objectType”: “QuestionSet“ } | Question Sets associated with the current set.MVP Scope: “preConditions” and “branchRules” are not in R3.4 scope | R3.4 | 
| children | type: “list”, “required”: true | Questions and Question Sets will actually be part of the “children” attribute of the parent question set. They are listed separately in this document for detailing their individual structures.In future, other object types like Asset and Content can also be added into a question set. | R3.3 | 
| OutcomeProcessing | “eval”: “custom outcome processing logic using javascript”– OR – ”template”: "SUM_OF_SCORES", "AVG_OF_SCORES" ”ignoreNullValues”: true/false ”mappingConfig”: “Configuration to set additional outcome variables (other than SCORE)“ | Outcome processing rules of a question set can be defined using custom evaluation logic or use one of the existing outcome processing templates. | R3.4 | 
| RequiresSubmit | type: “boolean”, required”: true, defaultValue: false | If user has to explicitly submit to record an attempt or the attempt is automatically recorded on exit or completion (i.e. reached end page). | R3.4 | 
| SummaryType |  **V1** type: “string”, required”: false, enum: \[“Complete”, “Score”, “Duration”, “Score & Duration”] Complete: My Score / Total Score + Duration **V2 (future)** Summary:<ul><li>My score: Y/N

</li><li>Total score: Y/N

</li><li>Duration: Y/N

</li><li>Question level performance: Y/N

</li><li>Report card: Y/N

</li></ul>Note: How do Reference (Subjective) question show up in question level summary & how do they contribute to Score is yet to be defined.  |  **V1** Complete: Show My Score out of Total Score and DurationScore: Show only My ScoreDuration: Show only DurationScore & Duration: Show My Score and Duration onlyThis is show on the END PAGE after Submit. Type of summary to be displayed for the question set. **End Page Summary** Duration only (Default): Show duration. Hide the score obtained & total marksMy Score only: Only Score obtainedMy Score out of Total: Shows Score obtained out of Total scoreReport card: Show Correct, Incorrect, Skipped, and Total question count. Viewed, Skipped for reference questionsDetailed (Question level performance): See marks and result for each questionFor system evaluated questions - attempted, skipped, correct, incorrectFor reference questions (not evaluated on system) - viewed, skippedIn case of Shuffle & MaxQuestions (Show x/y Qs) → Summary should show total score as per MaxQuestions (not TotalQuestions)TBD: summary types to be defined properly and finalise the scope for MVP. |  | 
| Shuffle | type: “boolean”, required”: true, defaultValue: true | If questions in the question set have to be shuffled or presented in the same order as added by the creator. | R3.4 | 
| TotalQuestions | type: “integer”, required”: true | Total number of questions in the question set. | R3.4 | 
| MaxQuestions | type: “integer”, required”: true | Number of questions in the question set that should be used in one session. | R3.4 | 
| ShowFeedback | type: “boolean”, required”: true, defaultValue: false | If feedback should be shown or not while consuming the question set. | R3.4 | 
| ShowSolutions | type: “boolean”, required”: true, defaultValue: false |  | R3.4 | 
| ShowHints | type: “boolean”, required”: true, defaultValue: false | If hints should be shown or not while consuming the question set. |  | 
| QuMLVersion | type: “string”, required: true | Version of the QuML specification using which the question set is created. | R3.4 | 
| TimeLimits | type: “json”, required: false | The time limits (if any) for a question set can be defined as  **timeLimits**  data. Both minimum and maximum time constraints can be provided for the complete set and/or for one question as well. This configuration is used by QuML players to impose time limits (both minimum and maximum) for attempting a question set.Along with time limits, there can be Warning time as well. At warning time, the timer turns red & blinks. Time unit: seconds |  | 
| ShowTimer | type: “boolean”, required: false | Show or hide timer when playing this question set. | R3.4 | 
| DifficultyLevel | “easy”, “medium”, “hard” |  |  | 
| BloomsLevel | type: “string”, required: false, enum: \[“remember”, “understand”, “apply”, “analyse”, “evaluate”, “create”] | Cognitive processes involved to answer the question set. |  | 
| Purpose | recall, explore, sense, assess, teach, revise |  |  | 
| maxAttempts |  | Up to Max Attempts:<ul><li>Show which attempt I am playing 

</li><li>Requires submit

</li><li>Visibility outside collection is turned off (parent only)

</li></ul>After Max Attempts:<ul><li> …?

</li></ul> | R3.5 | 





*****

[[category.storage-team]] 
[[category.confluence]] 
