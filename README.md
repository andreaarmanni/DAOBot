# OceanDAO Bot

This bot pipes data from a few different sources, so we can efficiently report DAO-Related informaiton.
- Make sure you have `node` and `npm`
- `npm install`
- Create a `.env` file with the following envs:
```
AIRTABLE_API_KEY=KEY_HERE
AIRTABLE_BASEID=ID_HERE
INFURA_API_KEY=KEY_HERE
ETH_PRIVATE_KEY=KEY_HERE
SNAPSHOT_HUB_URL=https://hub.snapshot.page
```
## OceanDAO Airtable Data
Anyone can access the historical data for OceanDAO.

You can view the [Proposals Airtable through this link](https://airtable.com/shrd5s7HSXc2vC1iC)

You can use our [Airtable API Endpoint via this link](https://airtable.com/appVer8ccYGnqSm2H/api/docs#javascript/introduction) and access it via `curl`.

This bot sits on a cron, and updates Airtable to display a voting Leaderboard.
Run the sync_airtable.js script using `node` inside the CLI.

`user@vm:in/your/cli/DAOBot/$ node src/airtable/sync_airtable_active_proposal_votes.js >> log_sync_airtable_active_proposal_votes.csv`

## Airtable - Configure DAOBot to use your Airtable 

Configure your AIRTABLE_API_KEY + AIRTABLE_BASEID to execute the airtable/db sync.
- Then simply run src/airtable/sync_airtable_active_proposal_votes.js 

## GSheets - Point DAOBot to GSheet, get Vote Results
You can use DAOBot to dump votes from Snapshot, onto GSheets.
You can [instantly setup your GSheet, to render inside Notion.](https://www.notion.vip/charts/)

This bot also connects with GSheets.
- Copy your credentials.json into DAOBot/ root
- user@vm:in/your/cli/DAOBot/$node src/gsheets/index.js
- Follow cli prompts. token.json should be generated 
- user@vm:in/your/cli/DAOBot/$node src/gsheets/sync_gsheets_active_proposal_votes.js >> log_sync_gsheets_active_proposal_votes.csv

## RUN/CRON - DAOBot Main entry points

These are the scripts that you should run to execute DAOBt.
More Coming... Read each script for more details.
- src/airtable/sync_airtable_active_proposal_votes.js
- src/gsheets/sync_gsheets_active_proposal_votes.js
- src/snapshot/submit_snapshot_accepted_proposals.js

## CRON - Configure DAOBOT Crontab

The bash scripts located in the root `/DAOBot/` directory should allow you to run the node sync-scripts, from cron.

Instructions  
- From the command line enter: crontab -e
- Execute your cron scripts relative to your `/DAOBot/` path. 
- Your local node installation may be in a different path than what's inside the .sh scripts. Use `which node`.

Example Crontab - Sync every 2 minutes 
```
*/2 * * * * sh /DAOBot/cron_sync_votes_airtable.sh 2>&1
*/2 * * * * sh /DAOBot/cron_sync_votes_gsheets.sh 2>&1
```

