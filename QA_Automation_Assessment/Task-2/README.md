# Task 2 – Crypto Morning Brief Workflow

## Overview

For this task, I created an automated cryptocurrency monitoring workflow using n8n. The workflow runs on a scheduled interval, retrieves cryptocurrency market data, filters the top 5 cryptocurrencies, checks Bitcoin's 24-hour price change percentage, and sends a notification to Discord based on a predefined threshold.

## APIs Used

### CoinGecko API

I used the CoinGecko public API because it provides real-time cryptocurrency market data without requiring authentication.

Endpoints used:

* `/coins/markets`

  * Retrieves cryptocurrency market information.
  * Used to obtain the top cryptocurrencies by market capitalization.

* `/coins/bitcoin`

  * Retrieves detailed Bitcoin market information.
  * Used to check Bitcoin's 24-hour price change percentage.

### Discord Webhook API

I used a Discord webhook to send automated notifications directly to a Discord channel. This allows the workflow to deliver market updates without manual intervention.

## Data Transformation

After retrieving the cryptocurrency data, I used a JavaScript Code node to:

* Extract only the required fields:

  * Coin Name
  * Symbol
  * Current Price
  * 24-Hour Change Percentage
  * Market Cap Rank

* Filter the API response to keep only the Top 5 cryptocurrencies.

This makes the data cleaner and easier to process in later workflow steps.

## Conditional Logic

An IF node checks whether Bitcoin's 24-hour price change percentage is greater than 5%.

### True Branch

If Bitcoin's price change exceeds 5%, the workflow is configured to send a High Alert message to Discord indicating strong market movement.

### False Branch

During testing, Bitcoin's price change was below 5%, so the False branch executed successfully and sent a normal Crypto Morning Brief message to Discord.

## Error Handling

For both CoinGecko API requests, I enabled the "Continue On Error" option.

If an API request fails:

* The workflow does not stop immediately.
* The execution continues and the error can be reviewed in the n8n execution logs.
* This prevents a single API failure from completely breaking the workflow.

## Result

The workflow successfully:

* Retrieves cryptocurrency market data.
* Filters the Top 5 cryptocurrencies.
* Monitors Bitcoin market movement.
* Uses conditional logic to determine the notification path.
* Sends automated notifications to Discord.

The workflow meets all assignment requirements, including scheduling, API integration, data transformation, conditional branching, notification delivery, and error handling.
