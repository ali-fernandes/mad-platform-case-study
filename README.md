# Market Action Dynamics technical case study

Market Action Dynamics (MAD) brings market research, planning models, event timing, and private trading-result review into related workspaces. This case study explains the product decisions and technical architecture behind its invitation-stage implementation.

**Product lead:** Ali Fernandes, technology transformation leader and former CIO.

## Why I built it

Researching a market decision can mean moving between news, price charts, an economic calendar, personal notes, and trading records. I built MAD to bring those pieces into a connected workflow: research an opportunity, evaluate it against your criteria, see upcoming events, and review actual trading results.

The platform supports both short-term trading plans and longer-term investment research. Users can see which criteria have supporting data, where they need to add their own assessment, and what information is still missing. Imported trading results provide a separate record of what actually happened.

## What the platform includes

- Editorial publishing and contributor review workflows.
- A Decision Desk for trading models and planning.
- Forward Planning for ticker-specific investment theses.
- A time-aware calendar linking scheduled events and research.
- Owner-reviewed invitations and account lifecycle management.
- Read-only support sessions and administrative audit history.
- Private broker CSV imports and statement-aware journal analytics.
- A separate SwiftUI companion MVP with a REST service boundary.

## Architecture

| Layer | Technology | Responsibility |
| --- | --- | --- |
| Web interface | React, TypeScript, Next.js | Workspaces, forms, charts, and navigation |
| Application services | Next.js route handlers | Privileged operations and provider aggregation |
| Identity | Supabase Auth | User sessions and authentication |
| Account data | PostgreSQL through Supabase | Records, ownership policies, and audit history |
| Local thesis state | Browser storage | Thesis selections and evidence in the documented implementation |
| Delivery | GitHub and Vercel | Source review and deployment |
| iOS companion | SwiftUI | Native sample-data MVP and REST boundary |

Browser-local thesis state has different continuity and ownership properties from account-backed records. The mobile MVP's documented sample-data behavior is distinct from a fully connected production app.

## Engineering decisions

### Show coverage alongside scores

A high score based on a small amount of evidence should not imply a completed thesis. MAD separates available-evidence score, weighted coverage, and supported points. Qualitative criteria require a rating and a supporting note.

[Read the scoring example](docs/evidence-scoring.md).

### Enforce authorization beyond the entry gate

Invitation checks control application entry. Database policies control browser access to records. Privileged server routes require their own authorization. Support sessions are bounded, scoped, and read-only, with administrative audit records.

### Reconcile results before labeling them net

Gross P&L is not relabeled as net. Net results depend on matching statement scope and known fees or exact broker-reported daily figures. Filters can invalidate that scope. Trading-session dates are distinct from the original execution timestamps.

### Keep AI drafting reviewable

An optional editorial route contains OpenAI moderation and structured drafting. It returns draft content for editorial review. Code presence establishes an implemented integration; live activation and evaluation require separate evidence.

## How delivery was organized

The project release record includes scoped requirements, implementation changes, database migrations, targeted tests, build checks, and selected browser or HTTP verification. Technical handoffs preserve the difference between implemented behavior, deployment, verified flows, and remaining work.

The journal reconciliation example shows why product judgment matters: a missing fee record must change what the interface claims. The authorization example shows why a successful login alone is insufficient evidence of secure access.

## What this demonstrates

MAD connects product requirements to system behavior. It provides concrete material for explaining architecture, data boundaries, failure conditions, and release decisions to both builders and organizational leaders.

The next adoption case study can build on this foundation by documenting a real AI workflow, role-specific training, and measured use. Product delivery and organizational adoption are related accomplishments with different evidence.

## Evidence scope

This account draws on documented September 2026 releases and local source inspection in October 2026. It does not claim a new production audit, full-suite test pass, proven investment performance, or measured organizational AI adoption. Public examples use synthetic inputs.
