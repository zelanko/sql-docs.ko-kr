---
title: '7단원: 데이터베이스를 특정 시점으로 복원 | Microsoft 문서'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: a9f99670-e1de-441e-972c-69faffcac17a
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3659e3be185c6148b7688a070fa162a877e56692
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32947158"
---
# <a name="lesson-7-restore-a-database-to-a-point-in-time"></a>7단원: 데이터베이스를 특정 시점으로 복원
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
이 단원에서는 두 트랜잭션 로그 백업 사이의 특정 시점으로 AdventureWorks2014 데이터베이스를 복원합니다.  
  
기존의 백업에서 특정 시점 복원을 수행하려면 전체 데이터베이스 백업, 차등 백업 및 복원하려는 시점 바로 다음까지의 모든 트랜잭션 로그 파일을 사용해야 합니다. 파일-스냅숏 백업을 사용할 경우 복원하려는 시간을 프레이밍하는 골대를 제공하는 두 개의 인접한 로그 백업 파일만 있으면 됩니다. 각 로그 백업이 각 데이터베이스 파일(각 데이터 파일 및 로그 파일)의 파일 스냅숏을 만들기 때문에 두 개의 로그 파일 스냅숏 백업 세트만 있으면 됩니다.  
  
파일 스냅숏 백업 세트에서 지정한 특정 시점으로 데이터베이스를 복원하려면 다음 단계를 따르세요.  
  
1.  SQL Server Management Studio에 연결합니다.  
  
2.  새 쿼리 창을 열고 Azure 가상 머신에 있는 데이터베이스 엔진의 SQL Server 2016 인스턴스에 연결합니다.  
  
3.  다음 Transact-SQL 스크립트를 복사하여 쿼리 창에 붙여넣은 다음 실행합니다. 5단계에서 더 적은 수의 행이 있는 특정 시점으로 복원하기 전에 Production.Location 테이블에 29,939개의 행이 있는지 확인합니다.  
  
    ```  
  
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location  
  
    ```  
  
    ![행 개수 29,939가 표시됨](../relational-databases/media/5e2f4229-1970-49c9-89b3-e96b6f7fde83.JPG "행 개수 29,939가 표시됨")  
  
4.  다음 Transact-SQL 스크립트를 복사하여 쿼리 창에 붙여넣습니다. 인접한 두 개의 로그 백업 파일을 선택하고 파일 이름을 이 스크립트에 필요한 날짜 및 시간으로 변환합니다. 1단원에서 지정한 컨테이너 및 저장소 계정 이름에 맞게 URL을 수정하고 첫 번째 및 두 번째 백업 파일 이름을 제공한 다음 "June 26, 2015 01:48 PM"의 형식으로 STOPAT 시간을 제공하고 이 스크립트를 실행합니다. 이 스크립트를 완료하려면 몇 분 정도 걸립니다.  
  
    ```  
  
    -- restore and recover to a point in time between the times of two transaction log backups, and then verify the row count  
    ALTER DATABASE AdventureWorks2014 SET SINGLE_USER WITH ROLLBACK IMMEDIATE;  
    RESTORE DATABASE AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<firstbackupfile>.bak'   
       WITH NORECOVERY,REPLACE;  
    RESTORE LOG AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<secondbackupfile>.bak'    
       WITH RECOVERY, STOPAT = 'June 26, 2015 01:48 PM';  
    ALTER DATABASE AdventureWorks2014 set multi_user;  
    -- get new count  
    SELECT COUNT (*) FROM AdventureWorks2014.Production.Location ;  
  
    ```  
  
5.  출력을 검토합니다. 복원 후 행 개수는 18,389개로, 로그 백업 5와 6 사이의 행 개수입니다(사용자 행 개수는 다를 수 있음).  
  
    ![특정 시점 복원 후 행 개수를 보여 주는 결과 창](../relational-databases/media/4a0c6d8b-e2ed-4e93-bd7a-ade22a4aecc6.JPG "특정 시점 복원 후 행 개수를 보여 주는 결과 창")  
  
**다음 단원:**  
  
[8단원. 로그 백업에서 새 데이터베이스로 복원](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)  
  
  
  
