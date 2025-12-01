# Exotic Pets Retailing Platform — Presentation Script

Use this content to build the 6-slide deck (6 minutes) plus demo guidance.

## Slide 1 — Company Introduction
- **Business:** Digital storefront for exotic pets, habitats, and care supplies (reptiles, amphibians, small mammals, specialty enclosures, climate control kits, and vetted nutrition bundles).
- **Primary customer:** Enthusiasts aged 18–45; skews toward hobbyists of all genders in urban/suburban areas; interests include herpetology, responsible breeding, and curated habitat design.
- **Competitive edge:** Welfare-first sourcing with veterinary screening, bundled habitat kits that simplify setup, fast shipping with temperature-stable packaging, and 24/7 exotic-vet chat for post-purchase support.

## Slide 2 — Team Introduction
- **Avery Chen — Product & UX (Presenter photo)**
  - Defines customer journeys, oversees accessibility-first design, and owns roadmap prioritization.
- **Jordan Malik — Engineering Lead**
  - Architects the platform, owns cloud infrastructure, and champions API reliability/SLOs.
- **Priya Desai — Data & Ops**
  - Manages inventory analytics, fraud/risk rules, and fulfillment instrumentation.

## Slide 3 — Architecture Overview Diagram
```
[Web/App Client]
      |
      v  HTTPS (REST/GraphQL)
[API Gateway]
      |
      v  HTTP (JSON)
[Order Service] --->(AMQP)----> [Event Bus] ----> [Notification Service]
      |                                     \
      |                                      \--> [Analytics Pipeline]
      |---> [Inventory Service] --HTTP--> [Catalog DB]
      |---> [Payment Service] --HTTPS--> [Payment Processor]
      '---> [User Service] --HTTP--> [User DB]
```
- Arrows show dependencies (caller ➜ callee). Async paths labeled via event bus.

## Slide 4 — Technology Stack Overview
- **Front End:** React + Vite, Tailwind CSS, browser-based accessibility testing (axe).
- **API & Services:** Node.js/Express services for Order, Inventory, Payment adapter, and User.
- **Data:** PostgreSQL for orders/users, document store for catalog (e.g., MongoDB/Atlas), Redis cache for product availability.
- **Messaging & Integration:** RabbitMQ (AMQP) for events, webhooks to third-party payment processor.
- **Infra & Observability:** Dockerized services on Kubernetes or ECS; API Gateway with WAF; OpenTelemetry tracing; Prometheus + Grafana dashboards; S3 for media assets.

## Slide 5 — Top 3 Takeaways
1. Welfare-focused commerce builds trust—vetting and care content uplift conversion.
2. Pre-bundled habitats cut buyer friction and reduce post-purchase support volume.
3. Event-driven integrations decouple payment, inventory, and notifications for resilience.

## Slide 6 — Top 3 Challenges
1. Temperature-controlled logistics and live-arrival guarantees constrained carrier choices.
2. Fraud prevention for high-value animals required adaptive rules and manual reviews.
3. Real-time inventory accuracy demanded cache invalidation and idempotent order flows.

## Demo Flow (for 2-minute recorded video)
1. **Home page:** Brief value proposition (“Ethically sourced exotic pets with habitat kits and vet support”). Highlight featured species and care guides.
2. **Purchase/order entry:** Select a pet + habitat bundle, show availability badge; enter buyer details and delivery window.
3. **Confirmation:** Display order summary, delivery safeguards, and link to care resources; note post-purchase vet chat.
