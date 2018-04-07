---
title: 매핑 소스 및 대상 데이터 형식 (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- customizing data type mappings
- data types, mapping
- mapping, data types
- source data types
- target data types
ms.assetid: b362a075-16e7-423f-b63f-e1e9f02844a9
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a76e26e753ae431d1f4649b05c159d4526358d4a
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="mapping-source-and-target-data-types-accesstosql"></a>매핑 소스 및 대상 데이터 형식 (AccessToSQL)
액세스 데이터베이스 형식이 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 유형입니다. Access 데이터베이스 개체를 변환 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 개체에 대 한 액세스의 데이터 형식을 매핑하는 방법을 지정 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 기본 데이터 형식 매핑을 그대로 사용 하거나 다음 절차에 나와 있는 것 처럼 매핑을 사용자 지정할 수 있습니다.  
  
## <a name="default-mappings"></a>기본 매핑  
SSMA에 기본 데이터 형식 매핑 집합이 있습니다. 기본 매핑 목록이 참조 [프로젝트 설정 (유형 매핑)](http://msdn.microsoft.com/en-us/b87b9683-abed-4677-8c50-18bdba704655)합니다.  
  
## <a name="customizing-data-type-mappings"></a>사용자 정의 데이터 형식 매핑  
사용 하 여는 **프로젝트 설정** 대화 상자에서 모든 데이터베이스 및 프로젝트의 데이터베이스 개체에 대 한 형식이 매핑되는 방법을 사용자 지정할 수 있습니다. 프로젝트에 대 한 형식 매핑을 모든 데이터베이스 및 사용자 지정 형식 매핑이 없는 데이터베이스 개체에 적용 됩니다.  
  
데이터베이스 또는 테이블 수준에서 데이터 형식 매핑을 사용자 지정할 수도 있습니다.  
  
다음 절차에는 프로젝트, 데이터베이스 또는 데이터베이스 개체 수준에서의 데이터 형식을 매핑하는 방법을 보여 줍니다.  
  
**데이터 형식을 매핑할**  
  
1.  전체 프로젝트에 대 한 데이터 형식 매핑을 사용자 지정 하려면 열에서 **프로젝트 설정** 대화 상자:  
  
    1.  에 **도구** 메뉴 선택 **프로젝트 설정**합니다.  
  
    2.  왼쪽된 창에서 선택 **유형 매핑**합니다.  
  
        형식 매핑 차트 및 단추 오른쪽 창에 나타납니다.  
  
    또는 데이터베이스 또는 테이블 수준에서 데이터 형식 매핑을 사용자 지정 하려면 데이터베이스 또는 테이블 창에서 선택 액세스 메타 데이터 탐색기:  
  
    1.  액세스 메타 데이터 탐색기 창에서 확장 **액세스 메타 베이스**을 펼친 다음 **데이터베이스**합니다.  
  
    2.  데이터 형식 매핑을 사용자 지정 하려는 데이터베이스 또는 테이블을 선택 합니다.  
  
    3.  오른쪽 창에서 클릭 **유형 매핑**합니다.  
  
2.  새 매핑을 추가 하려면 다음을 수행 합니다.  
  
    1.  유형 매핑 창을 클릭 **추가**합니다.  
  
    2.  에 **새 유형 매핑** 대화 상자의 **소스 형식**를 매핑할 Access 데이터 형식을 선택 합니다.  
  
    3.  형식 길이 필요한 경우 선택 하 여 매핑에 대 한 최소 및 최대 데이터 길이 지정 된 **에서** 및 **를** 확인란을 선택한 다음 값을 입력 합니다.  
  
        이렇게 하면 동일한 데이터 형식의 크기가 작고 더 큰 값에 대 한 데이터 매핑을 사용자 지정할 수 있습니다.  
  
    4.  아래 **대상 유형**, 대상을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식입니다.  
  
        일부 형식은 대상 데이터 형식의 길이가 필요합니다. 필요한 경우 입력에 새 데이터 길이 **바꿀 내용** 상자를 선택한 다음 클릭 **확인**합니다.  
  
3.  데이터 형식 매핑을 편집 하려면 다음을 수행 합니다.  
  
    1.  유형 매핑 창을 클릭 **편집**합니다.  
  
    2.  에 **형식 매핑 목록** 대화 상자의 **소스 형식**를 매핑할 Access 데이터 형식을 선택 합니다.  
  
    3.  형식 길이 필요한 경우 선택 하 여 매핑에 대 한 최소 및 최대 데이터 길이 지정 된 **에서** 및 **를** 확인란을 선택한 다음 값을 입력 합니다.  
  
        이렇게 하면 동일한 데이터 형식의 크기가 작고 더 큰 값에 대 한 데이터 매핑을 사용자 지정할 수 있습니다.  
  
    4.  아래 **대상 유형**, 대상을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식입니다.  
  
        일부 형식은 대상 데이터 형식의 길이가 필요합니다. 필요한 경우 입력에 새 데이터 길이 **바꿀 내용** 상자를 선택한 다음 클릭 **확인**합니다.  
  
4.  데이터 형식 매핑을 제거 하려면 다음을 수행 합니다.  
  
    1.  형식 매핑 창에서 제거 하려는 데이터 형식 매핑을 포함 하는 형식 매핑 목록에서 행을 선택 합니다.  
  
    2.  **제거**를 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [SQL Server 개체에 액세스 데이터베이스 개체를 변환 합니다.](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
