---
title: UNIQUE 제약 조건 수정 | Microsoft 문서
ms.custom: ''
ms.date: 10/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- modifying constraints
- UNIQUE constraints [SQL Server], modifying
- constraints [SQL Server], modifying
- constraints [SQL Server], unique
ms.assetid: fddbdc9e-958b-4614-8e88-6ca205d64a4e
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 77ee0d93640041f75dd615128406025a47d98368
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43085336"
---
# <a name="modify-unique-constraints"></a>UNIQUE 제약 조건 수정
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 UNIQUE 제약 조건을 수정할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **UNIQUE 제약 조건을 수정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-modify-a-unique-constraint"></a>UNIQUE 제약 조건을 수정하려면  
  
1.  **개체 탐색기**에서 UNIQUE 제약 조건이 포함된 테이블을 마우스 오른쪽 단추로 클릭한 다음 **디자인**을 클릭합니다.  
  
2.  **테이블 디자이너** 메뉴에서 **인덱스/키...** 를 클릭합니다.  
  
3.  **인덱스/키** 대화 상자의 **선택한 기본/고유 키 및 인덱스**아래에서 편집하려는 제약 조건을 선택합니다.  
  
4.  다음 표의 동작을 수행합니다.  
  
    |수행할 작업|수행할 단계|  
    |--------|------------------------|  
    |제약 조건이 연결된 열 변경|1) **(일반)** 아래의 표에서 **열** 을 클릭한 후 속성 오른쪽에 있는 줄임표 **(…)** 를 클릭합니다.<br /><br /> 2) **인덱스 열** 대화 상자에서 인덱스에 대해 새 열 또는 정렬 순서 또는 두 가지 옵션을 모두 지정합니다.|  
    |제약 조건 이름 바꾸기|**ID**아래의 표에서 **이름** 상자에 새 이름을 입력합니다. 새 이름은 **선택한 기본/고유 키 또는 인덱스** 목록의 다른 이름과 중복되지 않아야 합니다.|  
    |클러스터형 옵션 설정|**테이블 디자이너**아래의 표에서 **클러스터형으로 만들기** 를 선택한 다음 클러스터형 인덱스를 만들려면 드롭다운에서 예를 선택하고 비클러스터형 인덱스를 만들려면 아니요를 선택합니다. 클러스터형 인덱스는 테이블마다 하나씩만 만들 수 있습니다. 클러스터형 인덱스가 이미 이 테이블에 있는 경우 원본 인덱스에 대해 이 설정을 먼저 해제해야 합니다.|  
    |채우기 비율 정의|**테이블 디자이너**아래의 표에서 **파일 사양** 범주를 확장하고 0에서 100 사이의 정수를 **채우기 비율** 상자에 입력합니다.|  
  
5.  **파일** 메뉴에서 *****테이블 이름 저장*을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> **UNIQUE 제약 조건을 수정하려면**  
  
 Transact-SQL을 사용하여 UNIQUE 제약 조건을 수정하려면 먼저 기존 UNIQUE 제약 조건을 삭제하고 새로운 정의를 사용하여 다시 만들어야 합니다. 자세한 내용은 [Delete Unique Constraints](../../relational-databases/tables/delete-unique-constraints.md) 및 [Create Unique Constraints](../../relational-databases/tables/create-unique-constraints.md)를 참조하세요.  
  
###  <a name="TsqlExample"></a>  
