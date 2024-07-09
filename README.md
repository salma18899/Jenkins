## Jenkins Poll SCM vs Webhook

Both Jenkins Poll SCM and Webhook serve to trigger builds automatically in Jenkins, but they operate in different ways and have distinct advantages and disadvantages. Here’s a comparison to help you decide which is best suited for your use case:

| Feature       | Poll SCM                                   | Webhook                                     |
|---------------|--------------------------------------------|---------------------------------------------|
| **How it Works** | Jenkins periodically checks the SCM for changes and triggers a build if changes are detected. | The SCM system sends an HTTP POST request to Jenkins as soon as changes are pushed, triggering a build immediately. |
| **Pros**      | - Simple to set up within Jenkins without needing additional SCM configuration. <br> - Does not rely on external services to trigger builds. | - Triggers builds immediately when changes are made, eliminating the need for periodic polling. <br> - Reduces load on Jenkins by only reacting to actual changes. |
| **Cons**      | - Can be resource-intensive due to regular checks even if no changes occur. <br> - Potential delay between change and build, depending on polling interval. | - Requires configuration on both Jenkins and the SCM system (e.g., GitHub) to set up the webhook. <br> - Dependent on network and the availability of both Jenkins and the SCM system. If the webhook request fails, the build won't be triggered. |
| **Use Case Scenarios** | - Prefer straightforward setup without modifying SCM configuration. <br> - Prefer Jenkins to be entirely responsible for checking changes. <br> - Working in an environment where immediate build triggers are not critical. | - Need immediate build triggers upon SCM changes. <br> - Aim to reduce Jenkins load by avoiding unnecessary SCM checks. <br> - Comfortable with configuring webhooks on your SCM system. |

### Recommendations

For most modern CI/CD workflows, **webhooks** are generally preferred due to their efficiency and immediate response to changes. However, **Poll SCM** can be useful in scenarios where setting up webhooks is not feasible or when a simpler setup is needed.
