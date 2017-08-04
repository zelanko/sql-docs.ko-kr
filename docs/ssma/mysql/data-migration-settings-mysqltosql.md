---
title: "데이터 마이그레이션 설정 (MySQLToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9c396df4-5676-4f32-9c57-70d4f15f9b7a
caps.latest.revision: 9
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 10658cfa7c181836aa823df7ff2fdb963ebdc795
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="data-migration-settings-mysqltosql"></a>데이터 마이그레이션 설정 (MySQLToSQL)
  
## <a name="data-migration-settings"></a>데이터 마이그레이션 설정  
**데이터 마이그레이션 설정** 데이터 마이그레이션에 대 한 사용자 지정 쿼리를 작성할 수 있습니다.  
  
-   이 탭은 사용할 수 있는 **확장 데이터 마이그레이션 옵션** 로 설정 되어 **표시** 설정을로 설정 된 경우 숨겨집니다 **숨기기** 프로젝트 설정에서 합니다. 프로젝트 마이그레이션 설정에 대 한 자세한 내용은 참조 [프로젝트 설정 (마이그레이션)](http://msdn.microsoft.com/en-us/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9) 합니다.  
  
-   구현 될 사용자 지정 SQL 문 구문 분석 **데이터 마이그레이션 설정** 테이블 노드를 탭 합니다.  
  
-   다음은 두 확인란을 사용할 수는 **데이터 마이그레이션 설정** viz.:  
  
    1.  SQL Server 테이블 잘라내기  
  
    2.  선택 사용 하 여 사용자 지정  
  
1.  **SQL Server 테이블을 자를:**  
     이 옵션에는 사용자를 데이터베이스에서 대상 데이터베이스로 마이그레이션된 데이터의 선명 명인 수 있습니다.  
  
    -   이 텍스트 상자는 기본적으로 선택 되어 있습니다.  
  
    -   이 텍스트 상자에 선택 하지 않으면 마이그레이션된 데이터는 대상 데이터베이스에 있는 기존 데이터에 추가 됩니다.  
  
2.  **사용 하 여 사용자 지정 선택:**  
     이 옵션을 사용 하면 수정 하는 **선택** 문이 있는 (**선택** 문은 데이터를 대상 데이터베이스에 표시를 선택할 수 있습니다).  
  
    1.  기본적으로이 텍스트 상자 선택 되지 않습니다.  
  
    2.  이 텍스트 상자 옵션을 선택 하 고 있으면 사용자가 수정할 수 있습니다는 **선택** 문을 제공 합니다.  
  
두 개의 존재 viz.:  
  
-   **적용:** 클릭 **적용** 변경 된 설정을 적용 합니다.  
  
-   **취소:** 클릭 **취소** 변경 되 고 되기 전의 있는 설정을 복원할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server/SQL Azure에 MySQL 데이터 마이그레이션](http://msdn.microsoft.com/en-us/a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82)  
  

