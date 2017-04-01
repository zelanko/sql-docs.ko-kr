---
title: "2단원: 공유 액세스 서명을 사용하여 SQL Server 자격 증명 만들기 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "02/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 29e57ebd-828f-4dff-b473-c10ab0b1c597
caps.latest.revision: 17
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 17
---
# 2단원: 공유 액세스 서명을 사용하여 SQL Server 자격 증명 만들기
이 단원에서는 [1단원: Azure 컨테이너에 저장된 액세스 정책 및 공유 액세스 서명 만들기](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)에서 만든 Azure 컨테이너에 쓰고 읽을 때 SQL Server에서 사용할 보안 정보를 저장하기 위해 자격 증명을 만듭니다.  
  
SQL Server 자격 증명은 SQL Server 외부의 리소스에 연결하는 데 필요한 인증 정보를 저장하는 데 사용되는 개체입니다. 자격 증명에는 저장소 컨테이너의 URI 경로와 이 컨테이너에 대한 공유 액세스 서명이 저장됩니다.  
  
> [!NOTE]  
> SQL Server 2012 SP1 CU2 이상 데이터베이스 또는 SQL Server 2014 데이터베이스를 이 Azure 컨테이너에 백업하려는 경우 여기에 문서화된 [사용되지 않는 구문](https://technet.microsoft.com/en-US/library/dn435916(v=sql.120).aspx)을 통해 저장소 계정 키를 기반으로 하는 SQL Server 자격 증명을 만들 수 있습니다.  
  
## SQL Server 자격 증명 만들기  
SQL Server 자격 증명을 만들려면 다음 단계를 수행합니다.  
  
1.  SQL Server Management Studio에 연결합니다.  
  
2.  새 쿼리 창을 열고 온-프레미스 환경에 있는 데이터베이스 엔진의 SQL Server 2016 인스턴스에 연결합니다.  
  
3.  새 쿼리 창에서 1단원의 공유 액세스 서명을 사용하는 CREATE CREDENTIAL 문을 붙여넣고 해당 스크립트를 실행합니다.  
  
    스크립트는 다음 코드와 같습니다.  
  
    ```Transact-SQL  
  
    USE master  
    CREATE CREDENTIAL 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>' – this name must match the container path, start with https and must not contain a forward slash.  
       WITH IDENTITY='SHARED ACCESS SIGNATURE' -- this is a mandatory string and do not change it.   
       , SECRET = 'sharedaccesssignature' –- this is the shared access signature key that you obtained in Lesson 1.   
    GO  
  
    ```  
  
4.  사용할 수 있는 모든 자격 증명을 보려면 인스턴스에 연결된 쿼리 창에서 다음 문을 실행합니다.  
  
    ```Transact-SQL  
    SELECT * from sys.credentials  
    ```  
  
5.  새 쿼리 창을 열고 Azure 가상 컴퓨터에 있는 데이터베이스 엔진의 SQL Server 2016 인스턴스에 연결합니다.  
  
6.  새 쿼리 창에서 1단원의 공유 액세스 서명을 사용하는 CREATE CREDENTIAL 문을 붙여넣고 해당 스크립트를 실행합니다.  
  
7.  Azure 컨테이너에 액세스할 수 있게 하려는 추가 SQL Server 2016 인스턴스에 대해 5단계와 6단계를 반복합니다.  
  
**다음 단원:**  
  
[3단원: URL에 데이터베이스 백업](../relational-databases/lesson-3-database-backup-to-url.md)  
  
## 참고 항목  
[자격 증명&#40;데이터베이스 엔진&#41;](../relational-databases/security/authentication-access/credentials-database-engine.md)  
[CREATE CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-credential-transact-sql.md)  
[sys.credentials&#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
