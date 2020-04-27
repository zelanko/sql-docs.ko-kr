---
title: 원본 및 대상 데이터 형식 매핑 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- customizing data type mappings
- data types, mapping
- mapping, data types
- source data types
- target data types
ms.assetid: b362a075-16e7-423f-b63f-e1e9f02844a9
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: e0600778b938a7736ab1112f31bbe4828605cdaf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67907167"
---
# <a name="mapping-source-and-target-data-types-accesstosql"></a>원본 및 대상 데이터 형식 매핑 (AccessToSQL)
Access 데이터베이스 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 형식과 다릅니다. Access 데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체로 변환 하는 경우 access에서로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터 형식을 매핑하는 방법을 지정 해야 합니다. 기본 데이터 형식 매핑을 그대로 적용 하거나 다음 절차에 표시 된 대로 매핑을 사용자 지정할 수 있습니다.  
  
## <a name="default-mappings"></a>기본 매핑  
SSMA에는 기본 데이터 형식 매핑 집합이 있습니다. 기본 매핑 목록은 [프로젝트 설정 (형식 매핑)](https://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655)을 참조 하세요.  
  
## <a name="customizing-data-type-mappings"></a>데이터 형식 매핑 사용자 지정  
**프로젝트 설정** 대화 상자를 사용 하 여 프로젝트의 모든 데이터베이스 및 데이터베이스 개체에 대 한 형식이 매핑되는 방식을 사용자 지정할 수 있습니다. 프로젝트에 대 한 형식 매핑은 사용자 지정 형식 매핑이 없는 모든 데이터베이스와 데이터베이스 개체에 적용 됩니다.  
  
데이터베이스 또는 테이블 수준에서 데이터 형식 매핑을 사용자 지정할 수도 있습니다.  
  
다음 절차에서는 프로젝트, 데이터베이스 또는 데이터베이스 개체 수준에서 데이터 형식을 매핑하는 방법을 보여 줍니다.  
  
**데이터 형식을 매핑하려면**  
  
1.  전체 프로젝트에 대 한 데이터 형식 매핑을 사용자 지정 하려면 **프로젝트 설정** 대화 상자를 엽니다.  
  
    1.  **도구** 메뉴에서 **프로젝트 설정**을 선택 합니다.  
  
    2.  왼쪽 창에서 **형식 매핑**을 선택 합니다.  
  
        오른쪽 창에 형식 매핑 차트와 단추가 표시 됩니다.  
  
    또는 데이터베이스 또는 테이블 수준에서 데이터 형식 매핑을 사용자 지정 하려면 액세스 메타 데이터 탐색기 창에서 데이터베이스 또는 테이블을 선택 합니다.  
  
    1.  액세스 메타 데이터 탐색기 창에서 **access-메타 베이스**를 확장 한 다음 **데이터베이스**를 확장 합니다.  
  
    2.  데이터 형식 매핑을 사용자 지정 하려는 데이터베이스 또는 테이블을 선택 합니다.  
  
    3.  오른쪽 창에서 **형식 매핑**을 클릭 합니다.  
  
2.  새 매핑을 추가 하려면 다음을 수행 합니다.  
  
    1.  형식 매핑 창에서 **추가**를 클릭 합니다.  
  
    2.  **새 형식 매핑** 대화 상자의 **원본 유형**에서 매핑할 액세스 데이터 형식을 선택 합니다.  
  
    3.  형식에 길이가 필요 하면 **시작 및 시작** 확인란을 선택한 다음 **값을 입력** 하 여 매핑에 대 한 최소 및 최대 데이터 길이를 지정 합니다.  
  
        이렇게 하면 동일한 데이터 형식의 더 작고 큰 값에 대 한 데이터 매핑을 사용자 지정할 수 있습니다.  
  
    4.  **대상 유형**에서 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 선택 합니다.  
  
        일부 형식에는 대상 데이터 형식 길이가 필요 합니다. 필요한 경우 **바꿀 내용** 상자에 새 데이터 길이를 입력 한 다음 **확인**을 클릭 합니다.  
  
3.  데이터 형식 매핑을 편집 하려면 다음을 수행 합니다.  
  
    1.  형식 매핑 창에서 **편집**을 클릭 합니다.  
  
    2.  **유형 매핑 목록** 대화 상자의 **원본 유형**에서 매핑할 액세스 데이터 형식을 선택 합니다.  
  
    3.  형식에 길이가 필요 하면 **시작 및 시작** 확인란을 선택한 다음 **값을 입력** 하 여 매핑에 대 한 최소 및 최대 데이터 길이를 지정 합니다.  
  
        이렇게 하면 동일한 데이터 형식의 더 작고 큰 값에 대 한 데이터 매핑을 사용자 지정할 수 있습니다.  
  
    4.  **대상 유형**에서 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 선택 합니다.  
  
        일부 형식에는 대상 데이터 형식 길이가 필요 합니다. 필요한 경우 **바꿀 내용** 상자에 새 데이터 길이를 입력 한 다음 **확인**을 클릭 합니다.  
  
4.  데이터 형식 매핑을 제거 하려면 다음을 수행 합니다.  
  
    1.  형식 매핑 창의 제거 하려는 데이터 형식 매핑이 포함 된 형식 매핑 목록에서 행을 선택 합니다.  
  
    2.  **제거**를 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [access 데이터베이스 개체를 SQL Server 개체로 변환 하](converting-access-database-objects-accesstosql.md) 는 것입니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server로 Access 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
