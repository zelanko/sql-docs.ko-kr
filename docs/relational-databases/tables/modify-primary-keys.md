---
title: "기본 키 수정 | Microsoft 문서"
ms.custom: 
ms.date: 07/25/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying primary keys
- primary keys [SQL Server], modifying
ms.assetid: 8e2a15ba-1cd1-4408-b860-16c3ee37d635
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ee0f0825c66c10ba5412a2b5d8ffc3db23077970
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="modify-primary-keys"></a>기본 키 수정
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 기본 키를 수정할 수 있습니다. 열 순서, 인덱스 이름, 클러스터형 옵션 또는 채우기 비율을 변경하여 테이블의 기본 키를 수정할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [보안](#Security)  
  
-   **기본 키를 수정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-modify-a-primary-key"></a>기본 키를 수정하려면  
  
1.  수정하려는 기본 키가 포함된 테이블에 대한 테이블 디자이너를 열고 테이블 디자이너를 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **인덱스/키** 를 선택합니다.  
  
2.  **인덱스/키** 대화 상자의 **선택한 기본/고유 키 및 인덱스** 목록에서 기본 키 인덱스를 선택합니다.  
  
3.  다음 표의 동작을 수행합니다.  
  
    |수행할 작업|수행할 단계|  
    |--------|------------------------|  
    |기본 키 이름 바꾸기|**이름** 상자에 새 이름을 입력합니다. 새 이름은 **선택한 기본/고유 키 또는 인덱스** 목록의 다른 이름과 중복되지 않아야 합니다.|  
    |클러스터형 옵션 설정|기본 키에 대한 클러스터형 인덱스를 만들려면 **CLUSTERED로 만들기**를 선택하고 드롭다운 목록 상자에서 옵션을 선택합니다. 클러스터형 인덱스는 테이블마다 하나씩만 만들 수 있습니다. 인덱스에 이 옵션을 사용할 수 없는 경우 기존의 클러스터형 인덱스에 대해 이 설정을 먼저 해제해야 합니다.<br /><br /> 이 옵션을 선택하지 않으면 고유 비클러스터형 인덱스가 만들어집니다.|  
    |채우기 비율 정의|**채우기 사양** 범주를 확장하고 0에서 100 사이의 정수를 **채우기 비율** 상자에 입력합니다. 채우기 비율과 그 사용 방법은 [인덱스의 채우기 비율 지정](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)을 참조하세요.|  
    |열 순서 변경|**열**을 선택한 다음 속성의 오른쪽에 있는 줄임표 **(…)** 를 클릭합니다. **인덱스 열** 대화 상자에서 기본 키의 열을 제거합니다. 그런 다음 이 열을 원하는 순서로 다시 추가합니다. 키에서 열을 제거하려면 **열** 이름 목록에서 열 이름을 제거하기만 하면 됩니다.|  
  
4.  **파일** 메뉴에서 **저장***table name*을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **기본 키를 수정하려면**  
  
 Transact-SQL을 사용하여 PRIMARY KEY 제약 조건을 수정하려면 먼저 기존 PRIMARY KEY 제약 조건을 삭제하고 새로운 정의를 사용하여 다시 만들어야 합니다. 자세한 내용은 [Delete Primary Keys](../../relational-databases/tables/delete-primary-keys.md) 및 [Create Primary Keys](../../relational-databases/tables/create-primary-keys.md)를 참조하세요.  
  
###  <a name="TsqlExample"></a>  
