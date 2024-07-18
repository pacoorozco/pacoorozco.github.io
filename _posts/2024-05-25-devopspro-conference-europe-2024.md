---
title:  "Talk: Learning from errors or how the team replaced the YAMS API gateway"
tags: [errors, learning, cost reduction, scalability]
category: talk
date:   2024-05-25
excerpt: "At the DevOps Pro Europe conference, Paco Orozco presented on the Edge team's work replacing an API gateway at Adevinta, doubling traffic while improving performance and reducing costs."
---

![Paco at DevOps Pro Europe](/assets/img/Paco_at_DevOps_Pro_Europe_2024.jpg){: .align-center}

Yesterday, I was speaking at the [DevOps Pro Europe Conference](https://devopspro.lt/). It was an **awesome experience** to attend, speak up and visit the beautiful city of Vilnius, Lithuania, where the conference took place.

I presented *"Growing at the edge: Doubling traffic while changing the API gateway"* ([slides](https://es.slideshare.net/slideshow/2024-devops-pro-europe-growing-at-the-edge/269290859)) or how the Edge team at [Adevinta](https://adevinta.com) successfully **replaced the *YAMS* (Your Adevinta Media Service) API gateway while doubling traffic**. YAMS provides transformation tools like resizing, cropping, blurring images, converting documents to PDF, and processing videos on the fly for all the marketplaces of the company.

The existing 5-year-old Zuul API gateway had several issues: missing log correlation, low test coverage, high maintenance costs, obsolete technology, missing HTTP method support, and performance issues causing high CPU spikes.

In June 2021, the assessment was made to replace the gateway as eBay marketplaces started integrating with YAMS, increasing traffic.

The fetch gateway replacement went through a robust releasing pipeline. However, **there were multiple rollbacks** due to issues like missing headers, CORS problems, high CPU usage and retry failures. For the management gateway replacement, **there were 4 more failed deployments** due to misconfigured timeouts, authentication issues and other bugs before successfully deploying. 

Despite the challenges, the new gateways provided significant improvements:

- 10x better performance handling more requests with same infrastructure
- *Request id* correlation and consistent logging
- Higher test coverage and up-to-date codebase
- Less CPU usage leading to cost savings
- Better documentation reducing support requests
- Shared knowledge within the team reducing silos

The key takeaways were to **assess problems bravely, improve testing, communicate changes well, ensure proper logging/monitoring, and work as a team to overcome roadblocks**.

On the funny side of the story, one of my team colleagues shared this question which I had to reply.

![Funny question](/assets/img/Paco_at_DevOps_Pro_Europe_2024.jpg){: .align-center}

Overall, it was a successful migration that doubled traffic while modernizing the API gateway, thanks to the Edge team's preparation and perseverance.

