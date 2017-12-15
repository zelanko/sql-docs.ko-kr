---
title: "3단원: URL에 데이터베이스 백업 | Microsoft 문서"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: a9ae1501-b614-49d3-b975-6569da8350b2
caps.latest.revision: "16"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f63e84d8c22b5c88214cc4d85a6bebf572c41430
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-3-database-backup-to-url"></a>3단원: URL에 데이터베이스 백업
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 단원에서는 온-프레미스 SQL Server 2016 인스턴스의 AdventureWorks2014 데이터베이스를 [1단원: Azure 컨테이너에 저장된 액세스 정책 및 공유 액세스 서명 만들기](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)에서 만든 Azure 컨테이너에 백업합니다.  
  
> [!NOTE]  
> SQL Server 2012 SP1 CU2 이상 데이터베이스 또는 SQL Server 2014 데이터베이스를 이 Azure 컨테이너에 백업하려는 경우 [여기](https://technet.microsoft.com/en-US/library/dn435916(v=sql.120).aspx) 에 문서화된 사용되지 않는 구문을 통해 WITH CREDENTIAL 구문을 사용하여 URL에 백업할 수 있습니다.  
  
Blob Storage에 데이터베이스를 백업하려면 다음 단계를 따르세요.  
  
1.  SQL Server Management Studio에 연결합니다.  
  
2.  새 쿼리 창을 열고 Azure 가상 컴퓨터에 있는 데이터베이스 엔진의 SQL Server 2016 인스턴스에 연결합니다.  
  
3.  다음 Transact-SQL 스크립트를 복사하여 쿼리 창에 붙여넣습니다. 1단원에서 지정한 컨테이너 및 저장소 계정 이름에 맞게 URL을 수정한 다음 이 스크립트를 실행합니다.  
  
    ```  
  
    -- To permit log backups, before the full database backup, modify the database to use the full recovery model.  
    USE master;  
    ALTER DATABASE AdventureWorks2014  
       SET RECOVERY FULL;  
  
    -- Back up the full AdventureWorks2014 database to the container that you created in Lesson 1  
    BACKUP DATABASE AdventureWorks2014   
       TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_onprem.bak'  
  
    ```  
  
4.  개체 탐색기를 열고 저장소 계정 및 계정 키를 사용하여 Azure Storage에 연결합니다.  
  
5.  컨테이너를 확장하고 1단원에서 만든 컨테이너를 확장한 다음 위 3단계의 백업이 이 컨테이너에 표시되는지 확인합니다.  
  
    ![온-프레미스 백업 파일이 Azure 컨테이너에 blob으로 나타남](../relational-databases/media/0d060e51-012f-4c61-ab8d-16d461d0ffad.JPG "온-프레미스 백업 파일이 Azure 컨테이너에 blob으로 나타남")  
  
**다음 단원:**  
  
[4단원: URL에서 가상 컴퓨터로 데이터베이스 복원](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)  
  
