---
title: '3 단원: SQL Server 자격 증명 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 29e57ebd-828f-4dff-b473-c10ab0b1c597
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7178e1fb1e405dd013387ef97a6a670a0a5c3474
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48211583"
---
# <a name="lesson-3-create-a-sql-server-credential"></a>3단원: SQL Server 자격 증명 만들기
  이 단원에서는 Windows Azure 저장소 계정에 액세스하는 데 사용하는 보안 정보를 저장하는 자격 증명을 만듭니다.  
  
 SQL Server 자격 증명은 SQL Server 외부의 리소스에 연결하는 데 필요한 인증 정보를 저장하는 데 사용되는 개체입니다. 자격 증명에는 저장소 컨테이너의 URI 경로와 공유 액세스 서명 키 값이 저장됩니다. 데이터 또는 로그 파일에서 사용하는 각 저장소 컨테이너에 대해 컨테이너 경로와 일치하는 이름의 SQL Server 자격 증명을 만들어야 합니다.  
  
 자격 증명에 대 한 일반적인 정보를 참조 하세요 [자격 증명 &#40;데이터베이스 엔진&#41;](security/authentication-access/credentials-database-engine.md)합니다.  
  
> [!IMPORTANT]  
>  아래에 설명 된 SQL Server 자격 증명을 만들기 위한 요구 사항은 합니다 [Windows Azure의 SQL Server 데이터 파일](databases/sql-server-data-files-in-microsoft-azure.md) 기능입니다. Azure storage에 백업 프로세스에 대 한 자격 증명을 만드는 방법에 대 한 정보를 참조 하세요 [단원 2: Create a SQL Server Credential](../tutorials/lesson-2-create-a-sql-server-credential.md)합니다.  
  
 SQL Server 자격 증명을 만들려면 다음 단계를 수행합니다.  
  
1.  SQL Server Management Studio에 연결합니다.  
  
2.  개체 탐색기에서 설치된 데이터베이스 엔진의 인스턴스에 연결합니다.  
  
3.  표준 도구 모음에서 새 쿼리를 클릭합니다.  
  
4.  다음 예를 복사하여 쿼리 창에 붙여 넣고 필요한 대로 수정합니다. 다음 문은 저장소 컨테이너의 공유 액세스 인증서를 저장하기 위해 SQL Server 자격 증명을 만듭니다.  
  
    ```tsql  
  
    USE master  
    CREATE CREDENTIAL credentialname – this name should match the container path and it must start with https.   
       WITH IDENTITY='SHARED ACCESS SIGNATURE', -- this is a mandatory string and do not change it.   
       SECRET = 'sharedaccesssignature' –- this is the shared access signature key that you obtained in Lesson 2.   
    GO  
  
    ```  
  
     자세한 내용은 [CREATE CREDENTIAL &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-credential-transact-sql) SQL Server 온라인 설명서의 합니다.  
  
5.  사용할 수 있는 모든 자격 증명을 보려면 쿼리 창에서 다음 문을 실행합니다.  
  
    ```tsql  
    SELECT * from sys.credentials  
    ```  
  
     Sys.credentials에 대 한 자세한 내용은 참조 하세요. [sys.credentials &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql) SQL Server 온라인 설명서의 합니다.  
  
 **다음 단원:**  
  
 [4단원: Windows Azure Storage에서 데이터베이스 만들기](lesson-3-database-backup-to-url.md)  
  
  
