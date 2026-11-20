# Miami Black SUV MCP server

Miami Black SUV is a chauffeured SUV service in the Miami area. This remote MCP server lets an AI assistant read the service details, get a trip quote, and send a booking request.

This repository holds the public documentation and the registry entry. The server is hosted by the company. Its source code is not published here.

## Connect

| Item | Value |
|---|---|
| Endpoint | `https://blacksuvmiami.com/mcp` |
| Transport | Streamable HTTP |
| Sign-in | None |
| Registry name | `com.blacksuvmiami/miami-black-suv` |
| Documentation | https://blacksuvmiami.com/agents |

Claude Code:

```
claude mcp add --transport http miami-black-suv https://blacksuvmiami.com/mcp
```

Other clients: add a remote MCP server with the endpoint above and no authentication.

## Tools

| Tool | Type | What it does |
|---|---|---|
| `get_service_info` | Read | Lists service types, vehicles with passenger and bag limits, locations, add-ons, and booking terms. |
| `get_quote` | Read | Returns the website fare and the amount due for a trip, or says the trip is by request. |
| `create_booking` | Write | Submits a trip the user has confirmed and returns a Stripe-hosted payment link. The user pays on that page. |

The server never takes card details. A ride is reserved only after payment, subject to availability.

A quote-only endpoint with the two read tools is at `https://blacksuvmiami.com/mcp-quote`.

## Example prompts

- What services does Miami Black SUV offer, and what are the passenger and bag limits?
- Get a quote for 3 passengers and 3 bags from Miami International Airport to South Beach next Friday at 6 pm. I do not have the flight number yet.
- Quote a 4-hour Suburban rental starting in Brickell on Saturday at 10 am for 4 passengers and 2 bags.

## Limits

- Read tools: 60 calls per minute per client.
- Booking: 20 calls per hour per client, and 3 bookings per day per customer email or phone number.
- A call over a limit returns the code `RETRY_LATER`.

## Policies and contact

- Privacy: https://blacksuvmiami.com/policies/privacy
- Terms: https://blacksuvmiami.com/policies/terms
- Contact: bookings@blacksuvmiami.com, +1 305-745-7523
