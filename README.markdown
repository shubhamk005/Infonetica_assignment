# Simple Workflow Engine

This is a simple app for the Infonetica assignment. It lets you make workflows, start them, do actions, and check what's happening.

## How to Run
1. Install .NET 8 SDK from the .NET website.
2. Clone this repo: `git clone <repo-url>`
3. Go to the folder: `cd SimpleWorkflow`
4. Run the app: `dotnet run`
5. The app runs at `https://localhost:5001`.

## API
- `POST /workflow`: Make a new workflow with states and actions.
- `GET /workflow/{id}`: See a workflow's details.
- `POST /workflow/{id}/start`: Start a new instance of a workflow.
- `POST /instance/{id}/action`: Do an action (send `{ "ActionId": "id" }` in the body).
- `GET /instance/{id}`: Check the current state and history of an instance.

## Example
Create a workflow:
```bash
curl -X POST https://localhost:5001/workflow -H "Content-Type: application/json" -d '{
  "States": [
    {"Id": "s1", "Name": "Start", "IsInitial": true, "IsFinal": false, "Enabled": true},
    {"Id": "s2", "Name": "Done", "IsInitial": false, "IsFinal": true, "Enabled": true}
  ],
  "Actions": [
    {"Id": "a1", "Name": "Finish", "Enabled": true, "FromStates": ["s1"], "ToState": "s2"}
  ]
}'
```

## Notes
- Everything is stored in memory, so data disappears when the app stops.
- Checks for basic errors like missing start state or wrong actions.
- Didn't have time to add tests or save data to a file.
- Could make it better with more time, like adding more checks or features.