---
title: "Data Migration Assistant를 사용하여 Stretch Database용 데이터베이스 및 테이블 식별 | Microsoft Docs"
ms.custom: 
ms.date: 10/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: stretch-database
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, identifying databases
- Stretch Database, identifying tables
- identifying databases for Stretch Database
- identifying tables for Stretch Database
ms.assetid: 81bd93d8-eef8-4572-88d7-5c37ab5ac2bf
caps.latest.revision: "29"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3fe01369c0dc9ab2f8556cafd932d6c624ed9554
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="identify-databases-and-tables-for-stretch-database-with-data-migration-assistant"></a>Data Migration Assistant를 사용하여 Stretch Database용 데이터베이스 및 테이블 식별
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  잠재적인 차단 문제와 함께 Stretch Database의 후보인 데이터베이스 및 테이블을 식별하려면 Microsoft Data Migration Assistant를 다운로드하여 실행합니다.
  
## <a name="get-data-migration-assistant"></a>Data Migration Assistant 가져오기
 [여기](https://www.microsoft.com/download/details.aspx?id=53595)서 Data Migration Assistant를 다운로드하고 설치합니다. 이 도구는 SQL Server 설치 미디어에는 포함되지 않습니다.  
  
## <a name="run-data-migration-assistant"></a>Data Migration Assistant 실행  
  
1.  Microsoft Data Migration Assistant를 실행합니다.  

2.  **평가** 형식의 새 프로젝트를 만들고 이름을 지정합니다.

3.  **원본 서버 유형** 및 **대상 서버 유형** 둘 다로 **SQL Server**를 선택합니다.

4.  **만들기**를 선택합니다. 

5. **옵션** 페이지(1단계)에서 **새 기능 권장 사항**을 선택합니다. 필요에 따라 **호환성 문제**에 대한 선택을 해제합니다.

6.  **원본 선택** 페이지(2단계)에서 서버에 연결하고 데이터베이스를 선택한 후 **추가**를 선택합니다.

7.  **평가 시작**을 선택합니다.

## <a name="review-the-results"></a>결과 검토  
  
1.  분석이 완료되면 **결과 검토** 페이지(3단계)에서 **기능 권장 사항** 옵션을 선택한 다음 **저장소** 탭을 선택합니다.

2.  Stretch Database와 관련된 권장 사항을 검토합니다. 각 권장 사항에는 잠재적인 차단 문제와 함께 Stretch Database가 적절할 수 있는 테이블이 나열됩니다.

## <a name="historical-note"></a>기록 참고
Stretch Database Advisor는 이전의 SQL Server 2016 업그레이드 관리자 구성 요소였습니다. 이때는 Stretch Database Advisor를 별도의 작업으로 선택하고 실행해야 했습니다.

업그레이드 관리자를 대체하고 확장하는 Data Migration Assistant 릴리스로 Stretch Database Advisor의 기능이 이 새로운 도구에 통합됩니다. Stretch Database와 관련된 권장 사항을 얻기 위해 옵션을 선택할 필요가 없습니다. Data Migration Assistant에서 평가를 실행하면 Stretch Database와 관련된 결과가 **기능 권장 사항**의 **저장소** 탭에 나타납니다.
  
## <a name="next-step"></a>다음 단계  
 스트레치 데이터베이스를 사용하도록 설정합니다.  
  
-   **데이터베이스**에서 스트레치 데이터베이스를 사용하도록 설정하려면 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)을 참조하세요.  
  
-   다른 **테이블**에서 스트레치 데이터베이스를 사용하도록 설정하려면 [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)을 참조하세요. 
  
## <a name="see-also"></a>참고 항목  
 [스트레치 데이터베이스에 대한 제한 사항](../../sql-server/stretch-database/limitations-for-stretch-database.md)   
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [테이블에서 Stretch Database 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
