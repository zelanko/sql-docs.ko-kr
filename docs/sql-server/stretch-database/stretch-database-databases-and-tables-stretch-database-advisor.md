---
title: "Stretch Database 데이터베이스 및 테이블 - Stretch Database 관리자 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/14/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, identifying databases
- Stretch Database, identifying tables
- identifying databases for Stretch Database
- identifying tables for Stretch Database
ms.assetid: 81bd93d8-eef8-4572-88d7-5c37ab5ac2bf
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 603226ee369f6e557bae19e80211677f92fe7cd7
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="stretch-database-databases-and-tables---stretch-database-advisor"></a>Stretch Database 데이터베이스 및 테이블 - Stretch Database 관리자
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Stretch Database에 사용 가능한 데이터베이스와 테이블을 식별하려면 SQL Server 2016 업그레이드 관리자를 다운로드한 다음 Stretch Database 관리자를 실행합니다. Stretch Database 관리자는 차단 문제도 식별합니다.  
  
## <a name="download-and-install-upgrade-advisor"></a>업그레이드 관리자 다운로드 및 설치  
 [여기](https://www.microsoft.com/en-us/download/details.aspx?id=53595)서 업그레이드 관리자를 다운로드하여 설치하세요. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 설치 미디어에는 이 도구가 포함되어 있지 않습니다.  
  
## <a name="run-the-stretch-database-advisor"></a>Stretch Database 관리자 실행  
  
1.  업그레이드 관리자를 실행합니다.  
  
2.  **시나리오**를 선택하고 **Stretch Database 관리자 실행**을 선택합니다.  
  
3.  **Stretch Database 관리자 실행** 블레이드에서 **분석할 데이터베이스 선택**을 클릭합니다.  
  
4.  **데이터베이스 선택** 블레이드에서 서버 이름 및 인증 정보를 입력하거나 선택합니다. **연결**을 클릭합니다.

5.  선택한 서버에 대한 데이터베이스 목록이 표시됩니다. 분석할 데이터베이스를 선택합니다. **선택**을 클릭합니다.  
  
6.  **Stretch Database 관리자 실행** 블레이드에서 **실행**을 클릭합니다.  분석이 실행됩니다.  
  
## <a name="review-the-results"></a>결과 검토  
  
1.  분석이 완료되면 **분석 데이터베이스** 블레이드에서 분석한 데이터베이스 중 하나를 선택하여 **분석 결과** 블레이드를 표시합니다.  
  
     **분석 결과** 블레이드에는 선택한 데이터베이스에서 기본 권장 기준과 일치하는 권장 테이블이 나열됩니다. 
  
2.  **분석 결과** 블레이드의 테이블 목록에서 권장 테이블 중 하나를 선택하여 **테이블 결과** 블레이드를 표시합니다.  
  
     차단 문제가 있는 경우 **테이블 결과** 블레이드에 선택한 테이블에 대한 차단 문제가 나열됩니다. Stretch Database 관리자가 검색하는 차단 문제에 대한 자세한 내용은 [Stretch Database에 대한 제한 사항](../../sql-server/stretch-database/limitations-for-stretch-database.md)을 참조하세요.  
  
3.  **테이블 결과** 블레이드의 차단 문제 목록에서 한 항목을 선택하면 선택한 문제 및 완화 단계에 대한 자세한 내용이 표시됩니다. 선택한 테이블을 Stretch Database용으로 구성하려면 제안된 완화 단계를 구현합니다.  
  
## <a name="next-step"></a>다음 단계  
 Stretch Database를 사용하도록 설정합니다.  
  
-   **데이터베이스**에서 Stretch Database를 사용하도록 설정하려면 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)을 참조하세요.  
  
-   다른 **테이블**에서 Stretch Database를 사용하도록 설정하려면 [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)을 참조하세요. 
  
## <a name="see-also"></a>참고 항목  
 [Stretch Database에 대한 제한 사항](../../sql-server/stretch-database/limitations-for-stretch-database.md)   
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [테이블에서 Stretch Database 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  

