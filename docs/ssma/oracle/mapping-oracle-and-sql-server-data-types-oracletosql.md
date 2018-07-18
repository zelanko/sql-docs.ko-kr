---
title: Oracle 및 SQL Server 데이터 형식 (OracleToSQL) 매핑 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Type Mapping Inheritance
ms.assetid: 05da1495-63b9-47b7-86e2-6746394a2d8a
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 54b67cbb38c9884afc19f6da6283bfda99f93e88
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979326"
---
# <a name="mapping-oracle-and-sql-server-data-types-oracletosql"></a>매핑 Oracle 및 SQL Server 데이터 형식 (OracleToSQL)
Oracle 데이터베이스 형식에서 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 형식입니다. Oracle 데이터베이스 개체를 변환 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 개체에 Oracle에서 데이터 형식을 매핑하는 방법을 지정 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 기본 데이터 형식 매핑을 그대로 사용 하거나 다음 섹션에 표시 된 대로 매핑을 사용자 지정할 수 있습니다.  
  
## <a name="default-mappings"></a>기본 매핑  
SSMA에 기본 데이터 형식 매핑 집합이 있습니다. 기본 매핑 목록을 참조 하세요 [프로젝트 설정 &#40;형식 매핑&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)합니다.  
  
## <a name="type-mapping-inheritance"></a>형식 상속 매핑  
프로젝트 수준, 개체 범주 수준 (예: 모든 저장된 프로시저) 또는 개체 수준에서 형식 매핑을 사용자 지정할 수 있습니다. 하위 수준에서 재정의 되지 않으면 설정이 더 높은 수준에서 상속 됩니다. 예를 들어, 매핑하는 경우 **smallmoney** 에 **money** 프로젝트 수준에서 프로젝트의 모든 개체 개체나 범주 수준에서 매핑을 사용자 지정 하지 않으면이 매핑을 사용 합니다.  
  
보면 합니다 **형식 매핑** SSMA 백그라운드에서에서 탭은 상속 되는 형식 매핑을 표시할 색으로 구분 합니다. 형식 매핑의 배경이 노란색 상속 된 형식 매핑 및 현재 수준에서 지정 된 모든 매핑에 대 한 백서입니다.  
  
## <a name="customizing-data-type-mappings"></a>사용자 지정 데이터 형식 매핑  
다음 절차에는 프로젝트, 데이터베이스 또는 개체 수준에서의 데이터 형식을 매핑하는 방법을 보여 줍니다.  
  
**데이터 형식을 매핑할**  
  
1.  전체 프로젝트에 대 한 데이터 형식 매핑 사용자 지정을 하려면 엽니다는 **프로젝트 설정** 대화 상자:  
  
    1.  에 **도구** 메뉴에서 **프로젝트 설정을**합니다.  
  
    2.  왼쪽된 창에서 선택 **형식 매핑**합니다.  
  
        형식 매핑 차트 및 단추를 오른쪽 창에 나타납니다.  
  
    또는 데이터 형식에 맞게 매핑 데이터베이스, 테이블, 뷰 또는 저장된 프로시저 수준에서 데이터베이스, 개체 범주 또는 개체 탐색기에서 선택 Oracle 메타 데이터:  
  
    1.  Oracle 메타 데이터 탐색기에서 폴더 또는 사용자 지정 하는 개체를 선택 합니다.  
  
    2.  오른쪽 창에서을 클릭 합니다 **형식 매핑** 탭 합니다.  
  
2.  새 매핑을 추가 하려면 다음을 수행 합니다.  
  
    1.  **추가**를 클릭합니다.  
  
    2.  아래 **원본 유형**를 매핑할 Oracle 데이터 형식을 선택 합니다.  
  
    3.  형식에서 길이가 필요한 경우의 매핑에 대 한 최소한의 데이터 길이 지정 합니다 **에서** 상자 및 최대 데이터 길이 **를** 상자입니다.  
  
        이렇게 하면 동일한 데이터 형식의 작고 큰 값 데이터 매핑을 사용자 지정할 수 있습니다.  
  
    4.  아래 **대상 유형**, 대상을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식입니다.  
  
        일부 유형의 대상 데이터 형식의 길이 해야합니다. 필요한 경우 새 데이터 길이 입력 합니다 **바꿉니다** 상자입니다.  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
3.  데이터 형식 매핑을 수정 하려면 다음을 수행 합니다.  
  
    1.  **편집**을 클릭합니다.  
  
    2.  아래 **원본 유형**를 매핑할 Oracle 데이터 형식을 선택 합니다.  
  
    3.  형식에서 길이가 필요한 경우의 매핑에 대 한 최소한의 데이터 길이 지정 합니다 **에서** 상자 및 최대 데이터 길이 **를** 상자입니다.  
  
        이렇게 하면 동일한 데이터 형식의 작고 큰 값 데이터 매핑을 사용자 지정할 수 있습니다.  
  
    4.  아래 **대상 유형**, 대상을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식입니다.  
  
        일부 유형의 대상 데이터 형식의 길이 해야합니다. 필요한 경우 새 데이터 길이 입력 합니다 **바꿉니다** 상자에서 다음 [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
4.  사용자 지정 데이터 형식 매핑을 제거 하려면 다음을 수행 합니다.  
  
    1.  제거 하려는 데이터 형식 매핑을 포함 하는 형식 매핑 목록에서 행을 선택 합니다.  
  
    2.  **제거**를 클릭합니다.  
  
        상속 된 매핑을 제거할 수 없습니다. 그러나 상속된 매핑 사용자 지정 매핑을 특정 개체 또는 개체 범주에 의해 재정의 됩니다.  
  
## <a name="next-steps"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는가 중 하나로 [평가 보고서를 만드는](http://msdn.microsoft.com/4de9bcf6-1346-4740-87f9-7f24a8226357) 또는 [SQL Server 구문에 Oracle 데이터베이스 개체를 변환](http://msdn.microsoft.com/e021182d-31da-443d-b110-937f5db27272)합니다. 평가 보고서를 만드는 경우 Oracle 개체를 평가 하는 동안 자동으로 변환 됩니다.  
  
## <a name="see-also"></a>관련 항목  
[SQL Server로 데이터베이스 마이그레이션 Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
