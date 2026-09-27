# LLM alt text linter skill prompt

The attached SKILL is for linting alt text. Audit these tags using the SKILL.md rules.

## Alt text linter test inputs

Please audit the following Markdown/HTML image tags against the attached SKILL.md and return a structured report showing the Status, Rule Violations, and Suggested Fix for each item:

1. Missing alt tag: <img src="dashboard_view.png">
2. Explicit placeholder text: <img src="mfa_setup.png" alt="TODO: add screenshot alt text before release">
3. Raw file name as alt text: ![fig_3_webhook_payload.png](fig_3_webhook_payload.png)
4. Generic single-word description: ![chart](sales_metrics.png)
5. Exceeding 125-character cap (overly verbose): <img src="api_rate_limits.png" alt="A screenshot displaying the API rate limit management dashboard in Vero Finto showing active quota usage, burst thresholds, remaining request tokens, and HTTP 429 error response configurations.">
6. Non-decorative image too short (<10 chars): <img src="error_modal.png" alt="An error.">
7. Proper empty string for decorative asset (should pass): <img src="divider_line.png" alt="">
8. Banned stock photo / non-technical image: <img src="office_team.jpg" alt="Photo of software engineers collaborating around a conference table.">
9. Banned generic prefix ("An image of"): <img src="token_generator.png" alt="An image of the API bearer token generation button in the developer console.">
10. Primary logo usage (should pass): <img src="verofinto_header_logo.png" alt="Vero Finto">
11. Functional button under 10 chars (should pass): <img src="btn_close.png" alt="Close.">
12. Clickable header logo (should enforce functional link precedence over static logo): <a href="/"><img src="verofinto_logo.png" alt="Vero Finto"></a>
13. Hybrid UI and chart screenshot (should test tie-breaker logic): <!-- Context: Tutorial on reading system throughput metrics --> <img src="metrics_dashboard.png" alt="A screenshot of the metrics dashboard showing system throughput spikes during peak hours.">

14. Hybrid screenshot with clear Markdown context (should pass):
## Reading your throughput metrics
The dashboard below plots request volume against latency so you can spot bottlenecks at a glance.
![A diagram of the throughput dashboard showing a latency spike correlated with a traffic surge at 2 PM.](metrics_dashboard.png)

---
At the conclusion of the audit, create a separate report evaluating any changes needed for the SKILL.md, the prompt, or the tags.