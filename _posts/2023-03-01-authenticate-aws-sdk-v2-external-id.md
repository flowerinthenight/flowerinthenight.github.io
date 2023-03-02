---
layout: post
title: "Authenticating Go AWS SDK v2 using external id"
location: "Japan"
tags: [golang, aws, sdk, v2, assume, roles, external-id]
---

For self reference:

Sample code as to how to authenticate [aws-sdk-go-v2](https://github.com/aws/aws-sdk-go-v2) using [external ids](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html):

{% gist 0b745685a95888084ceb7e47f56827f4 %}
