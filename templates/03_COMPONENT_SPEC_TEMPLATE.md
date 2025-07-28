# Component Specification: [ComponentName]

## 1. Purpose
*A brief, one-sentence description of what this component does and where it fits in the application.*

**Example:** "This component displays a single task item, including its text and a button to delete it."

## 2. Props (Inputs)
*Define the properties (props) the component will accept. Specify the name, type, and a description of what it's for.*

| Prop Name | Type     | Required | Description                                     |
| :-------- | :------- | :------- | :---------------------------------------------- |
| `task`    | `Object` | Yes      | The task object, e.g., `{ id: number, text: string }` |
|           |          |          |                                                 |

## 3. Emitted Events (Outputs)
*Define any events the component will emit to its parent. Specify the event name and the payload it carries.*

| Event Name    | Payload         | Description                               |
| :------------ | :-------------- | :---------------------------------------- |
| `delete-task` | `task.id` (number) | Emitted when the user clicks the delete button. |
|               |                 |                                           |

## 4. Behavioral Logic
*Describe the component's behavior in a step-by-step or rule-based manner.*

-   The component must display the `task.text`.
-   The component must render a "Delete" button.
-   When the "Delete" button is clicked, the component must emit the `delete-task` event, passing the `task.id` as the payload.
-   There is no internal state management within this component; it is purely presentational.

## 5. Acceptance Criteria
*A checklist to confirm the component is complete and correct.*

-   [ ] Renders the task text passed in via props.
-   [ ] Renders a "Delete" button.
-   [ ] Clicking the button emits the `delete-task` event with the correct task ID.
-   [ ] The component's visual style is minimal and clean.
