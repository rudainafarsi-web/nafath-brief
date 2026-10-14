Version: NAFATH-V2
Track: Networking

## Overview
When emergency responders rely on a 5G service, losing connectivity can delay critical communication and coordination. Keeping the service reliable requires several technical areas to work together. Software design must handle failed requests and retries without accidentally repeating actions. AI can help predict network congestion, but the model must be tested against unseen data. Mobile applications should save essential information while offline and synchronize it when connectivity returns. Networking can prioritize critical traffic and separate service requirements when demand rises. Cybersecurity teams need a clear process to detect, contain, recover from, and learn from attacks. Data systems should organize usage records so managers can review performance across regions and days. Together, these practices support a more dependable service and help teams identify weaknesses before they affect responders.

## Software

In HTTP, GET, HEAD, OPTIONS and TRACE are safe methods: they are intended for reading information without requesting changes. All safe methods are also idempotent, meaning repeating a request has the same intended effect as sending it once. PUT and DELETE are idempotent too, although not safe. If a connection drops, retrying an idempotent request is generally possible. Automatically retrying POST can duplicate an emergency action unless the application prevents duplication.

Resource: RFC 9110 - HTTP Semantics - https://www.rfc-editor.org/rfc/rfc9110.html

## AI

Overfitting happens when a congestion prediction model learns patterns or noise specific to its training records and performs poorly on new network traffic. Cross-validation helps detect this by repeatedly evaluating the model on data not used in that training round. A large gap between training and validation performance may signal overfitting. Because network measurements arrive over time, time-aware splits should train on earlier periods and validate on later ones to avoid unrealistic results.

Resource: scikit-learn - Cross-validation: evaluating estimator performance - https://scikit-learn.org/stable/modules/cross_validation.html

## Mobile

An emergency response app should remain useful when the 5G connection is lost. It can display previously downloaded instructions, store field reports locally, and clearly show which updates are waiting to be sent. When service returns, a background queue should upload pending records with careful retries and download newer information. The app must handle conflicting edits and prevent repeated submissions. Urgent requests that cannot reach the server should be visibly marked as undelivered.

Resource: Android Developers - Build an offline-first app - https://developer.android.com/topic/architecture/data-layer/offline-first

## Networking
5G network slicing lets an operator configure multiple logical networks, called slices, with different service and performance requirements over a 5G system. For emergency responders, the operator could assign an authorized public-safety slice with suitable priority, capacity, latency policies and reliability targets. This helps manage emergency traffic requirements during congestion. However, slicing alone cannot restore coverage if a radio site or its backhaul is completely unavailable.

Resource: ETSI TS 122 261 - Service requirements for the 5G system - https://www.etsi.org/deliver/etsi_ts/122200_122299/122261/16.13.00_60/ts_122261v161300p.pdf

## Cybersecurity
According to NIST's updated incident response model, preparation involves Govern, Identify and Protect activities such as assigning responsibilities, finding critical assets and strengthening defenses. During Detect, the operator monitors suspicious traffic and confirms incidents. During Respond, the security team analyzes impact, contains malicious activity and removes the threat. During Recover, engineers restore trusted network services and verify their operation. Lessons learned are used continuously to improve procedures, controls and resilience.

Resource: NIST - Incident Response - https://csrc.nist.gov/projects/incident-response

## Data
A star schema stores usage measurements in a central fact table linked directly to dimension tables such as Date, Region and Service. In a snowflake schema, dimensions are normalized into additional related tables, which reduces duplication but introduces extra joins. For daily 5G service-usage reporting by region, a star schema is usually simpler: managers can group facts by date and region, filter quickly and build clear dashboards without navigating many relationships.

Resource: Microsoft Learn - Understand star schema and the importance for Power BI - https://learn.microsoft.com/en-us/power-bi/guidance/star-schema/

## Misconception in My Track

## Open Question
