---
title: 원본 및 대상 데이터 형식 (AccessToSQL) 매핑 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
ms.openlocfilehash: 4868bbe408b96c95a44c82516ce9bb6c9035397e
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979605"
---
# <a name="mapping-source-and-target-data-types-accesstosql"></a>원본 및 대상 데이터 형식 (AccessToSQL) 매핑
액세스 데이터베이스 형식에서 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 형식입니다. Access 데이터베이스 개체를 변환 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 개체에 대 한 액세스에서 데이터 형식을 매핑하는 방법을 지정 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 기본 데이터 형식 매핑을 그대로 사용 하거나 다음 절차에 표시 된 대로 매핑을 사용자 지정할 수 있습니다.  
  
## <a name="default-mappings"></a>기본 매핑  
SSMA에 기본 데이터 형식 매핑 집합이 있습니다. 기본 매핑 목록을 참조 하세요 [프로젝트 설정 (형식 매핑)](http://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655)합니다.  
  
## <a name="customizing-data-type-mappings"></a>사용자 지정 데이터 형식 매핑  
사용 하 여 합니다 **프로젝트 설정** 대화 상자에서 모든 데이터베이스 및 프로젝트의 데이터베이스 개체에 대 한 형식이 매핑되는 방법을 사용자 지정할 수 있습니다. 프로젝트에 대 한 형식 매핑을 모든 데이터베이스 및 사용자 지정 형식 매핑 되지 않은 데이터베이스 개체에 적용 됩니다.  
  
또한 데이터베이스 또는 테이블 수준에서 데이터 형식 매핑을 사용자 지정할 수 있습니다.  
  
다음 절차에는 프로젝트, 데이터베이스 또는 데이터베이스 개체 수준에서의 데이터 형식을 매핑하는 방법을 보여 줍니다.  
  
**데이터 형식을 매핑할**  
  
1.  전체 프로젝트에 대 한 데이터 형식 매핑 사용자 지정을 하려면 엽니다는 **프로젝트 설정** 대화 상자:  
  
    1.  에 **도구** 메뉴에서 **프로젝트 설정을**합니다.  
  
    2.  왼쪽된 창에서 선택 **형식 매핑**합니다.  
  
        형식 매핑 차트 및 단추를 오른쪽 창에 나타납니다.  
  
    또는 데이터베이스 또는 테이블 수준에서 데이터 형식 매핑 사용자 지정 선택 데이터베이스 또는 테이블 액세스 메타 데이터 탐색기 창에서:  
  
    1.  액세스 메타 데이터 탐색기 창에서 확장 **액세스-메타 베이스**를 차례로 확장 하 고 **데이터베이스**합니다.  
  
    2.  데이터 형식 매핑 사용자 지정 하려는 데이터베이스 또는 테이블을 선택 합니다.  
  
    3.  오른쪽 창에서 클릭 **형식 매핑**합니다.  
  
2.  새 매핑을 추가 하려면 다음을 수행 합니다.  
  
    1.  형식 매핑 창에서 클릭 **추가**합니다.  
  
    2.  에 **새 형식 매핑** 대화 상자의 **원본 유형**를 매핑할 액세스 데이터 유형을 선택 합니다.  
  
    3.  형식에서 길이가 필요한 경우 선택 하 여 매핑에 대 한 최소 및 최대 데이터 길이 지정 합니다 **에서** 및 **에** 확인란을 선택한 다음 값을 입력 합니다.  
  
        이렇게 하면 동일한 데이터 형식의 작고 큰 값 데이터 매핑을 사용자 지정할 수 있습니다.  
  
    4.  아래 **대상 유형**, 대상을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식입니다.  
  
        일부 유형의 대상 데이터 형식의 길이 해야합니다. 필요한 경우 새 데이터 길이 입력 합니다 **바꿀 내용** 상자를 선택한 다음 클릭 **확인**합니다.  
  
3.  데이터 형식 매핑을 편집 하려면 다음을 수행 합니다.  
  
    1.  형식 매핑 창에서 클릭 **편집**합니다.  
  
    2.  에 **형식 매핑 목록** 대화 상자의 **원본 유형**를 매핑할 액세스 데이터 유형을 선택 합니다.  
  
    3.  형식에서 길이가 필요한 경우 선택 하 여 매핑에 대 한 최소 및 최대 데이터 길이 지정 합니다 **에서** 및 **에** 확인란을 선택한 다음 값을 입력 합니다.  
  
        이렇게 하면 동일한 데이터 형식의 작고 큰 값 데이터 매핑을 사용자 지정할 수 있습니다.  
  
    4.  아래 **대상 유형**, 대상을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식입니다.  
  
        일부 유형의 대상 데이터 형식의 길이 해야합니다. 필요한 경우 새 데이터 길이 입력 합니다 **바꿀 내용** 상자를 선택한 다음 클릭 **확인**합니다.  
  
4.  데이터 형식 매핑을 제거 하려면 다음을 수행 합니다.  
  
    1.  형식 매핑 창에서 제거 하려는 데이터 형식 매핑을 포함 하는 형식 매핑 목록에서 행을 선택 합니다.  
  
    2.  **제거**를 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [SQL Server 개체에 access 데이터베이스 개체 변환](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>관련 항목  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
