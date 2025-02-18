+++
date = '2025-01-25T10:55:07-08:00'
draft = false
title = 'Analytics'
weight = 4
+++

# Analytics
There’s a chance that the OKRs and KPIs your team is managing can be collected/measured programmatically. Collecting information can be important, especially as you continue to achieve virality.

## Vercel Analytics
Vercel already has a ton of analytics built into their platform, which you can check out [here](https://vercel.com/docs/analytics). Even with the plan our class has, you can track metrics such as the total number of visitors and views; [speed and latency](https://vercel.com/docs/speed-insights); and even build logs.

![Image of Vercel Analytics](https://vercel.com/_next/image?url=https%3A%2F%2Fassets.vercel.com%2Fimage%2Fupload%2Fv1736938669%2Ffront%2Fdocs%2Fanalytics%2Fvisitor-chart-dark.png&w=3840&q=75)

### Tracking Client and Server Side Events
You can also track more granular events, such as if a specific user clicked on a button. This [tutorial](https://vercel.com/docs/analytics/custom-events#tracking-a-client-side-event) gives a great example, and it seems like it takes just a few lines of code after installing `@vercel/analytics`:

```typescript
import { track } from '@vercel/analytics';
 
function SignupButton() {
  return (
    <button
      onClick={() => {
        track('Signup');
        // ... other logic
      }}
    >
      Sign Up
    </button>
  );
}
```

You can also track server side actions, which can help you determine when certain API endpoints are called/invoked. There also seems to be a corresponding [tutorial](https://vercel.com/changelog/track-server-side-custom-events-with-vercel-web-analytics) here:

```typescript
import { track } from '@vercel/analytics/server';

export default function FeedbackPage() {
  async function submitFeedback(data: FormData) {
    'use server';

    await track('Feedback', {
      message: data.get('feedback') as string,
    });
  }

  return (
    <form action={submitFeedback}>
      <input type="text" name="feedback" placeholder="Feedback" />
      <button type="submit">Submit Feedback</button>
    </form>
  );
}
```

The above should cover most of the relevant tracking you might need. For the backend, we suggest tools such as [PostHog](https://posthog.com/docs/getting-started/send-events), [Prometheus](https://prometheus.io/), and [Grafana](https://grafana.com/).