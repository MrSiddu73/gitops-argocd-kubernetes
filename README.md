graph TD
    A[GitHub Repository]

    A --> B[apps]
    B --> B1[dev]
    B --> B2[stage]
    B --> B3[prod]

    B1 --> D1[deployment yaml dev 1 replica]
    B1 --> S1[service yaml dev]

    B2 --> D2[deployment yaml stage 2 replicas]
    B2 --> S2[service yaml stage]

    B3 --> D3[deployment yaml prod 3 replicas]
    B3 --> S3[service yaml prod]

    A --> C[argocd]
    C --> C1[guestbook dev application]
    C --> C2[guestbook stage application]
    C --> C3[guestbook prod application]

    C1 --> N1[k8s namespace dev]
    C2 --> N2[k8s namespace stage]
    C3 --> N3[k8s namespace prod]

    N1 --> P1[pods]
    N2 --> P2[pods]
    N3 --> P3[pods]

