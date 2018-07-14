---
title: HumanResources.myTeam 예제 테이블(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: data-movement
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- myTeam sample table [SQL Server]
- bulk importing [SQL Server], examples
- bulk exporting [SQL Server], examples
ms.assetid: 27da45a0-c1f4-4bf4-ab24-6196e80d3834
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 12919f045d5e4295859f70aede7d62ee667a5887
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246819"
---
# <a name="humanresourcesmyteam-sample-table-sql-server"></a>HumanResources.myTeam 예제 테이블(SQL Server)
  [대량 데이터 가져오기 및 내보내기](bulk-import-and-export-of-data-sql-server.md) 의 코드 예제에는 **myTeam**이라는 특별한 용도의 테스트 테이블이 필요한 경우가 많습니다. 예제를 실행하기 전에 **데이터베이스의** HumanResources **스키마에서** myTeam [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 테이블을 만들어야 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 샘플 데이터베이스 중 하나입니다.  
  
 **myTeam** 테이블에는 다음 열이 있습니다.  
  
|Column|데이터 형식|Null 허용 여부|Description|  
|------------|---------------|-----------------|-----------------|  
|**EmployeeID**|`smallint`|Null이 아님|행의 기본 키. 팀 멤버의 직원 ID|  
|**이름**|`nvarchar(50)`|Null이 아님|팀 멤버의 이름|  
|**Title**|`nvarchar(50)`|Null 허용|팀 직원의 직함|  
|**배경**|`nvarchar(50)`|Null이 아님|행이 마지막으로 업데이트된 날짜와 시간 (기본값)|  
  
 **HumanResources.myTeam을 만들려면**  
  
-   다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용합니다.  
  
    ```  
    --Create HumanResources.MyTeam:   
    USE AdventureWorks;  
    GO  
    CREATE TABLE HumanResources.myTeam   
    (EmployeeID smallint NOT NULL,  
    Name nvarchar(50) NOT NULL,  
    Title nvarchar(50) NULL,  
    Background nvarchar(50) NOT NULL DEFAULT ''  
    );  
    GO  
    ```  
  
 **HumanResources.myTeam을 채우려면**  
  
-   다음 `INSERT` 문을 실행하여 테이블을 두 행으로 채웁니다.  
  
    ```  
    USE AdventureWorks;  
    GO  
    INSERT INTO HumanResources.myTeam(EmployeeID,Name,Title,Background)  
       VALUES(77,'Mia Doppleganger','Administrative Assistant','Microsoft Office');  
    GO  
    INSERT INTO HumanResources.myTeam(EmployeeID,Name,Title,Background)  
       VALUES(49,'Hirum Mollicat','I.T. Specialist','Report Writing and Data Mining');  
    GO  
    ```  
  
    > [!NOTE]  
    >  이 문은 4번째 열 `Background`를 건너뜁니다. 이 열에는 기본값이 있습니다. 이 열을 건너뛰면 이 `INSERT` 문에서 이 열을 비워 두게 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 대량 가져오기 및 내보내기&#40;SQL Server&#41;](bulk-import-and-export-of-data-sql-server.md)  
  
  
