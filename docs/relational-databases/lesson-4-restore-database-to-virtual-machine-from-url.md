---
title: "4단원: URL에서 가상 컴퓨터로 데이터베이스 복원 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: ba793c8f-665a-4c46-b68d-f558a37906b2
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 31d30195b648f48b149021a7bf80aba2543a14ea
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-4-restore-database-to-virtual-machine-from-url"></a>4단원: URL에서 가상 컴퓨터로 데이터베이스 복원
이 단원에서는 Azure 가상 컴퓨터의 SQL Server 2016 인스턴스로 AdventureWorks2014 데이터베이스를 복원합니다.  
  
> [!NOTE]  
> 이 자습서에서는 간단한 설명을 위해 데이터베이스 백업에 사용한 것과 동일한 컨테이너를 데이터 및 로그 파일에 사용합니다. 프로덕션 환경에서는 여러 컨테이너를 사용할 가능성이 크며, 여러 데이터 파일을 사용하는 경우도 많습니다. SQL Server 2016에서는 큰 데이터베이스를 백업할 때 백업 성능을 향상시키기 위해 여러 blob에 백업을 스트라이핑할 수도 있습니다.  
  
Azure Blob Storage에서 Azure 가상 컴퓨터의 SQL Server 2016 인스턴스로 SQL Server 2014 데이터베이스를 복원하려면 다음 단계를 따르세요.  
  
1.  SQL Server Management Studio에 연결합니다.  
  
2.  새 쿼리 창을 열고 Azure 가상 컴퓨터에 있는 데이터베이스 엔진의 SQL Server 2016 인스턴스에 연결합니다.  
  
3.  다음 Transact-SQL 스크립트를 복사하여 쿼리 창에 붙여넣습니다. 1단원에서 지정한 컨테이너 및 저장소 계정 이름에 맞게 URL을 수정한 다음 이 스크립트를 실행합니다.  
  
    ```  
  
    -- Restore AdventureWorks2014 from URL to SQL Server instance using Azure blob storage for database files  
    RESTORE DATABASE AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_onprem.bak'   
       WITH  
          MOVE 'AdventureWorks2014_data' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_Data.mdf'  
         ,MOVE 'AdventureWorks2014_log' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_Log.ldf'  
    --, REPLACE  
  
    ```  
  
4.  개체 탐색기를 열고 Azure SQL Server 2016 인스턴스에 연결합니다.  
  
5.  개체 탐색기에서 데이터베이스 노드를 확장하고 AdventureWorks2014 데이터베이스가 복원되었는지 확인합니다(필요에 따라 노드 새로 고침).  
  
    ![가상 컴퓨터에서 SQL Server 2016으로 복원된 Adventure Works 2014 데이터베이스](../relational-databases/media/311f69a6-8443-4df5-8f30-3103c2472300.JPG "가상 컴퓨터에서 SQL Server 2016으로 복원된 Adventure Works 2014 데이터베이스")  
  
6.  개체 탐색기에서 AdventureWorks2014를 마우스 오른쪽 단추로 클릭하고 속성을 클릭합니다(완료되면 취소 클릭).  
  
7.  파일을 클릭하고 두 데이터베이스 파일의 경로가 Azure 블로그 컨테이너의 blob을 가리키는 URL인지 확인합니다.  
  
    ![논리적 데이터 파일의 파일 경로를 URL로 보여 주는 데이터베이스 속성](../relational-databases/media/cfeee576-6319-460e-9fa2-f0922e02ee23.JPG "논리적 데이터 파일의 파일 경로를 URL로 보여 주는 데이터베이스 속성")  
  
8.  개체 탐색기에서 Azure Storage에 연결합니다.  
  
9. 컨테이너를 확장하고 1단원에서 만든 컨테이너를 확장한 다음 위 3 단계의 AdventureWorks2014_Data.mdf 및 AdventureWorks2014_Log.ldf가 3단원의 백업 파일과 함께 이 컨테이너에 표시되는지 확인합니다(필요에 따라 노드 새로 고침).  
  
    ![Adventure Works 2014 데이터 및 로그 파일이 Azure 컨테이너에 blob으로 나타남](../relational-databases/media/156c7d73-44be-4754-9653-04cccb6c3066.JPG "Adventure Works 2014 데이터 및 로그 파일이 Azure 컨테이너에 blob으로 나타남")  
  
**다음 단원:**  
  
[5단원: 파일-스냅숏 백업을 사용하여 데이터베이스 백업](../relational-databases/lesson-5-backup-database-using-file-snapshot-backup.md)  
  
  
  

