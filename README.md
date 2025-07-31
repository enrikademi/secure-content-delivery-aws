# Secure Content Delivery on AWS Using CloudFront, MediaPackage, and Secrets Manager

This project demonstrates how to securely deliver media content using AWS services such as CloudFront, Elemental MediaPackage, IAM, and Secrets Manager. It enhances security by validating incoming requests through custom headers and secret validation, ensuring only authorized clients can access protected content.

## 📦 Architecture Overview

The solution uses the following AWS services:

- **AWS CloudFront**: Acts as the CDN layer to serve content with low latency and high availability.
- **AWS Elemental MediaPackage**: Serves as the origin for media content and enforces request validation.
- **AWS Secrets Manager**: Stores and manages secrets (tokens/identifiers) securely.
- **AWS IAM**: Manages permissions between services to ensure secure secret access.

### 🔒 Secure Workflow

1. A **playback device** initiates a content request through **CloudFront**.
2. CloudFront forwards the request to **MediaPackage**, including a custom HTTP header like: X-MediaPackage-CDNIdentifier: <Secret-Identifier>

3. MediaPackage retrieves the corresponding secret from **Secrets Manager** via **IAM** authorization.
4. MediaPackage **verifies** the secret matches the header value.
5. If valid, it responds with the requested media content (`HTTP 200 OK`). Otherwise, access is denied.

> 🔐 This pattern ensures that only clients presenting a valid secret can stream the content.



## This is the process we'll achieve.
![cdn_auth](https://github.com/user-attachments/assets/5dedbe7f-6b0e-408e-b93f-ceed49996ac3)
