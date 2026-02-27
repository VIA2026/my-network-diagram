```mermaid
graph TD
    subgraph sase [Cato Cloud / Zscaler Zero Trust Exchange]
        FWaaS[fa:fa-shield-alt FWaaS / SWG]
        CASB[fa:fa-lock CASB / DLP]
        ZTNA[fa:fa-key ZTNA]
    end

    subgraph branch [東京/名古屋/大阪/九州拠点]
        Edge[fa:fa-server Cato Socket / Branch Connector]
        Users[fa:fa-users 社内ユーザー]
        Devices[fa:fa-print 複合機 / IoT]
        Users --> Edge
        Devices --> Edge
    end

    subgraph remote [那覇空港現場 / 自宅]
        RemoteUser[fa:fa-laptop リモートユーザー<br>Cato Client / ZCC]
    end

    subgraph datacenter [オービッククラウド / 社内システム]
        App[fa:fa-database 業務アプリケーション]
        Connector[fa:fa-plug IPsec / App Connector]
        Connector --> App
    end

    subgraph internet [インターネット・SaaS]
        SaaS[fa:fa-cloud M365 / Adobe CC / ホットプロファイル]
        Web[fa:fa-globe 一般Webサイト]
    end

    Edge == インターネット回線 / 暗号化トンネル === FWaaS
    RemoteUser == クライアントVPN === ZTNA
    FWaaS --> SaaS
    FWaaS --> Web
    ZTNA === Connector
    
    classDef cloud_style fill:#e1f5fe,stroke:#01579b,stroke-width:2px;
    classDef premise_style fill:#fff3e0,stroke:#e65100,stroke-width:2px;
    
    class sase cloud_style;
    class branch,remote,datacenter premise_style;
```
