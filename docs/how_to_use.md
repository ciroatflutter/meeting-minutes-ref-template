# Meeting minutes

This repository is using GitHub issues to manage meeting minutes.

## Configuration

1. Go to `Settings > Actions` and update the **Workflow permissions** to **Read and write permissions**
1. Go to `Secrets and variables > Actions` (_Required only if you want the Slack integration_)

- Add a _repository variable_ named `MEETING_NAME` with the value being what you want to call this meeting (e.g. Team Retro)
- Add a secret named `SLACK_WEBHOOK_URL` with the Slack workflow webhook URL. It will be in the form `https://hooks.slack.com/workflows/....`

## Issues for meeting minutes

In the `.github/workflows` folder you can find two GitHub Actions Workflows.

| Workflow | Description | Trigger |
|----------|-------------|---------|
| Meeting Notes - Agenda Open | Creates an issue from a Meeting Notes template | Manual or on a schedule |
| Meeting Notes - Meeting Finished | Archives the issue content and comments when the issue is closed | Event based |

### Creating a new issue

You can create a new issue by manually triggering the `Meeting Notes - Agenda Open` workflow or by configuring the cron schedule in the [workflow yaml file](.github/workflows/meeting_agenda_open.yml).

The issue will be created with content from the [template](config/meeting_minutes_template.md).

Each issue is created with the purpose of documenting the meeting minutes for a forum meeting.

### Closing an issue

When closing an issue, both the issue content and comments are archived in a meeting notes file stored in the folder [meetings](/meetings).

This allows you to take all the notes with you in the event you decide to move away from GitHub Issues.

### Slack Integration

Both workflows integrate with Slack using a secret: `SLACK_WEBHOOK_URL`. When this secret is configured messages are sent to the webhook.

| Message | Description | Trigger (Workflow) |
|----------|-------------|---------|
| [Agenda Open](config/messages/agenda_open.json) | When the agenda is openned it sends a message with the issue link | Meeting Notes - Agenda Open |
| [Meeting Finished](config/messages/meeting_finished.json) | Archives the issue content and comments when the issue is closed | Meeting Notes - Meeting Finished |


## Slack Workflow Builder (Optional)

If you want the automated workflows to send messages to slack you need to create a workflow using the Slack Workflow Builder.

https://slack.com/help/articles/360053571454-Set-up-a-workflow-in-Slack
