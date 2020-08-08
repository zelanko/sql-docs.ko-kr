---
title: Oracle 및 SQL Server 데이터 형식 매핑 (OracleToSQL) | Microsoft Docs
description: Oracle 데이터 형식과 SQL Server 간의 Oracle 매핑을 사용자 지정 하는 방법에 대해 알아보고 기본값을 적용 합니다.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Type Mapping Inheritance
ms.assetid: 05da1495-63b9-47b7-86e2-6746394a2d8a
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 656132dafce39e6007601b75956fd73714638716
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934795"
---
# <a name="mapping-oracle-and-sql-server-data-types-oracletosql"></a>Oracle 및 SQL Server 데이터 형식 매핑(OracleToSQL)
Oracle 데이터베이스 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 형식과 다릅니다. Oracle 데이터베이스 개체를 개체로 변환 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 경우 oracle에서로 데이터 형식을 매핑하는 방법을 지정 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 기본 데이터 형식 매핑을 그대로 적용 하거나 다음 섹션에 표시 된 대로 매핑을 사용자 지정할 수 있습니다.  
  
## <a name="default-mappings"></a>기본 매핑  
SSMA에는 기본 데이터 형식 매핑 집합이 있습니다. 기본 매핑 목록은 [프로젝트 설정 &#40;형식 매핑&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)을 참조 하세요.  
  
## <a name="type-mapping-inheritance"></a>형식 매핑 상속  
프로젝트 수준, 개체 범주 수준 (예: 모든 저장 프로시저) 또는 개체 수준에서 형식 매핑을 사용자 지정할 수 있습니다. 낮은 수준에서 재정의 되지 않는 한 설정은 상위 수준에서 상속 됩니다. 예를 들어 프로젝트 수준에서 **smallmoney** 를 **money** 에 매핑하면 개체 또는 범주 수준에서 매핑을 사용자 지정 하지 않는 한 프로젝트의 모든 개체가이 매핑을 사용 합니다.  
  
SSMA에서 **형식 매핑** 탭을 보면 상속 된 형식 매핑을 보여 주기 위해 배경이 색으로 구분 됩니다. 형식 매핑의 배경은 상속 된 형식 매핑의 경우 노란색이 고 현재 수준에서 지정 된 매핑의 경우에는 흰색입니다.  
  
## <a name="customizing-data-type-mappings"></a>데이터 형식 매핑 사용자 지정  
다음 절차에서는 프로젝트, 데이터베이스 또는 개체 수준에서 데이터 형식을 매핑하는 방법을 보여 줍니다.  
  
**데이터 형식을 매핑하려면**  
  
1.  전체 프로젝트에 대 한 데이터 형식 매핑을 사용자 지정 하려면 **프로젝트 설정** 대화 상자를 엽니다.  
  
    1.  **도구** 메뉴에서 **프로젝트 설정**을 선택 합니다.  
  
    2.  왼쪽 창에서 **형식 매핑**을 선택 합니다.  
  
        오른쪽 창에 형식 매핑 차트와 단추가 표시 됩니다.  
  
    또는 데이터베이스, 테이블, 뷰 또는 저장 프로시저 수준에서 데이터 형식 매핑을 사용자 지정 하려면 Oracle 메타 데이터 탐색기에서 데이터베이스, 개체 범주 또는 개체를 선택 합니다.  
  
    1.  Oracle 메타 데이터 탐색기에서 사용자 지정할 폴더나 개체를 선택 합니다.  
  
    2.  오른쪽 창에서 **형식 매핑** 탭을 클릭 합니다.  
  
2.  새 매핑을 추가 하려면 다음을 수행 합니다.  
  
    1.  **추가**를 클릭합니다.  
  
    2.  **원본 유형**에서 매핑할 Oracle 데이터 형식을 선택 합니다.  
  
    3.  형식에 길이가 필요한 경우 **시작** 상자에 매핑의 최소 데이터 길이를 지정 하 고 **대상** 상자에 최대 데이터 길이를 지정 합니다.  
  
        이렇게 하면 동일한 데이터 형식의 더 작고 큰 값에 대 한 데이터 매핑을 사용자 지정할 수 있습니다.  
  
    4.  **대상 유형**에서 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 선택 합니다.  
  
        일부 형식에는 대상 데이터 형식 길이가 필요 합니다. 필요한 경우 **바꿀 내용** 상자에 새 데이터 길이를 입력 합니다.  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  데이터 형식 매핑을 수정 하려면 다음을 수행 합니다.  
  
    1.  **편집**을 클릭합니다.  
  
    2.  **원본 유형**에서 매핑할 Oracle 데이터 형식을 선택 합니다.  
  
    3.  형식에 길이가 필요한 경우 **시작** 상자에 매핑의 최소 데이터 길이를 지정 하 고 **대상** 상자에 최대 데이터 길이를 지정 합니다.  
  
        이렇게 하면 동일한 데이터 형식의 더 작고 큰 값에 대 한 데이터 매핑을 사용자 지정할 수 있습니다.  
  
    4.  **대상 유형**에서 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 선택 합니다.  
  
        일부 형식에는 대상 데이터 형식 길이가 필요 합니다. 필요한 경우 **바꿀 내용** 상자에 새 데이터 길이를 입력 한 다음[!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  사용자 지정 데이터 형식 매핑을 제거 하려면 다음을 수행 합니다.  
  
    1.  제거 하려는 데이터 형식 매핑이 포함 된 형식 매핑 목록에서 행을 선택 합니다.  
  
    2.  **제거**를 클릭합니다.  
  
        상속 된 매핑은 제거할 수 없습니다. 그러나 상속 된 매핑은 특정 개체 또는 개체 범주에 대 한 사용자 지정 매핑에 의해 재정의 됩니다.  
  
## <a name="next-steps"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [평가 보고서를 만들거나](assessing-oracle-schemas-for-conversion-oracletosql.md) [Oracle 데이터베이스 개체를 SQL Server 구문으로 변환](converting-oracle-schemas-oracletosql.md)하는 것입니다. 평가 보고서를 만드는 경우 Oracle 개체는 평가 중에 자동으로 변환 됩니다.  
  
## <a name="see-also"></a>참고 항목  
[Oracle 데이터베이스를 SQL Server &#40;OracleToSQL&#41;로 마이그레이션](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
