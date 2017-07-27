---
title: "외래 키 관계 수정 | Microsoft 문서"
ms.custom: 
ms.date: 07/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdtsql.chm:65538
- vdt.ppg.relationships
helpviewer_keywords:
- foreign keys [SQL Server], modifying
- modifying foreign keys
ms.assetid: 0c9ca80d-d79b-44c4-a21e-0fce39c398ec
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d938937ff7d4009ec874ebc9bbd33b2e87960def
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="modify-foreign-key-relationships"></a>외래 키 관계 수정
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 관계의 외래 키 측을 수정할 수 있습니다. 테이블의 외래 키를 수정하면 주 키 테이블의 열과 관련된 열이 변경됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **외래 키를 수정하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
 다음 경우를 제외하고 새 외래 키 열의 데이터 형식 및 크기는 관련된 기본 키 열의 데이터 형식 및 크기와 일치해야 합니다.  
  
-   **char** 열 또는 **sysname** 열은 **varchar** 열에 연결될 수 있습니다.  
  
-   **binary** 열은 **varbinary** 열에 연결될 수 있습니다.  
  
-   별칭 데이터 형식은 해당 기본 형식에 연결될 수 있습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-modify-a-foreign-key"></a>외래 키를 수정하려면  
  
1.  **개체 탐색기**에서 외래 키를 포함하는 테이블을 확장하고 **키**를 확장합니다.  
  
2.  수정할 외래 키를 마우스 오른쪽 단추로 클릭하고 **수정**을 클릭합니다.  
  
3.  **외래 키 관계** 대화 상자에서 다음과 같은 사항을 수정할 수 있습니다.  
  
     **선택한 관계**  
     기존 관계를 나열합니다. 관계를 선택하면 오른쪽 표에 해당 속성이 표시됩니다. 목록이 비어 있는 경우 테이블에 정의된 관계가 없음을 의미합니다.  
  
     **추가**  
     새 관계를 만듭니다. 관계를 유효하게 만들려면 **테이블 및 열 사양** 을 먼저 설정해야 합니다.  
  
     **Delete**  
     **선택한 관계** 목록에서 선택한 관계를 삭제합니다. 관계 추가를 취소하려면 이 단추를 사용하여 관계를 제거합니다.  
  
     **일반 범주**  
     확장하여 **만들거나 다시 활성화할 때 기존 데이터 검사** 와 **테이블 및 열 사양**을 표시합니다.  
  
     **Check Existing Data on Creation or Re-Enabling**  
     제약 조건을 만들거나 다시 활성화하기 전부터 테이블에 있던 모든 데이터를 제약 조건에 대해 검사합니다.  
  
     **테이블 및 열 사양 범주**  
     확장하여 어떠한 테이블의 어떠한 열이 관계에서 외래 키와 기본 키(또는 고유 키)로 사용되는지에 대한 정보를 표시합니다. 이러한 값을 편집하거나 정의하려면 속성 필드의 오른쪽에 있는 줄임표 단추(**...**)를 클릭합니다.  
  
     **외래 키 기본 테이블**  
     선택한 관계에서 외래 키로 사용되는 열이 포함된 테이블을 표시합니다.  
  
     **외래 키 열**  
     선택한 관계에서 외래 키로 사용되는 열을 표시합니다.  
  
     **Primary/Unique 키 기본 테이블**  
     선택한 관계에서 기본 키(또는 고유 키)로 사용되는 열이 포함된 테이블을 표시합니다.  
  
     **Primary/Unique 키 열**  
     선택한 관계에서 기본 키(또는 고유 키)로 사용되는 열을 표시합니다.  
  
     **ID 범주**  
     확장하여 **이름** 및 **설명**에 대한 속성 필드를 표시합니다.  
  
     **이름**  
     관계의 이름을 표시합니다. 새 관계를 만들면 **테이블 디자이너**의 활성 창에 있는 테이블을 기반으로 한 기본 이름이 새 관계에 지정됩니다. 언제든지 이름을 변경할 수 있습니다.  
  
     **설명**  
     관계에 대해 설명합니다. 자세한 설명을 기록하려면 **설명** 을 클릭한 다음 속성 필드의 오른쪽에 있는 줄임표 **(...)** 를 클릭합니다. 이렇게 하면 텍스트를 쓸 수 있는 더 큰 영역이 제공됩니다.  
  
     **테이블 디자이너 범주**  
     확장하여 **만들거나 다시 활성화할 때 기존 데이터 검사** 와 **복제에 적용**에 대한 정보를 표시합니다.  
  
     **Enforce For Replication**  
     복제 에이전트가 이 테이블에서 삽입, 업데이트 또는 삭제를 수행할 때 제약 조건을 적용할지 여부를 나타냅니다.  
  
     **외래 키 제약 조건 적용**  
     관계를 맺고 있는 열의 데이터를 변경할 때 외래 키 관계의 무결성 제약 조건을 위반하게 되는 경우 이러한 데이터를 변경할 수 있는지 여부를 지정합니다. 이러한 변경을 허용하지 않으려면 **예** 를 선택하고, 이를 허용하려면 **아니요** 를 선택합니다.  
  
     **INSERT 및 UPDATE 사양 범주**  
     확장하여 관계의 **삭제 규칙** 및 **업데이트 규칙** 에 대한 정보를 표시합니다.  
  
     **삭제 규칙**  
     외래 키 관계를 맺고 있는 데이터가 포함된 행을 사용자가 삭제하려 할 때 적용할 결과를 지정합니다.  
  
    -   **동작 안 함** 삭제가 허용되지 않고 DELETE가 롤백된다는 오류 메시지가 나타납니다.  
  
    -   **계단식 배열** 외래 키 관계에 관련된 데이터가 포함된 모든 행을 삭제합니다. 논리적 레코드를 사용하는 병합 게시에 테이블이 포함되는 경우 CASCADE를 지정하지 마세요.  
  
    -   **Null 설정** 테이블의 모든 외래 키 열에 Null 값을 사용할 수 있으면 값을 Null로 설정합니다.  
  
    -   **기본값 설정** 테이블의 모든 외래 키 열에 기본값이 정의되어 있으면 열에 정의된 기본값으로 값을 설정합니다.  
  
     **업데이트 규칙**  
     외래 키 관계를 맺고 있는 데이터가 포함된 행을 사용자가 업데이트하려 할 때 적용할 결과를 지정합니다.  
  
    -   **동작 안 함** 업데이트가 허용되지 않고 UPDATE가 롤백된다는 오류 메시지가 나타납니다.  
  
    -   **계단식 배열** 외래 키 관계에 관련된 데이터가 포함된 모든 행을 업데이트합니다. 논리적 레코드를 사용하는 병합 게시에 테이블이 포함되는 경우 CASCADE를 지정하지 마세요.  
  
    -   **Null 설정** 테이블의 모든 외래 키 열에 Null 값을 사용할 수 있으면 값을 Null로 설정합니다.  
  
    -   **기본값 설정** 테이블의 모든 외래 키 열에 기본값이 정의되어 있으면 열에 정의된 기본값으로 값을 설정합니다.  
  
4.  **파일** 메뉴에서 **저장***table name*을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **외래 키를 수정하려면**  
  
 Transact-SQL을 사용하여 FOREIGN KEY 제약 조건을 수정하려면 먼저 기존 FOREIGN KEY 제약 조건을 삭제하고 새로운 정의를 사용하여 다시 만들어야 합니다. 자세한 내용은 [Delete Foreign Key Relationships](../../relational-databases/tables/delete-foreign-key-relationships.md) 및 [Create Foreign Key Relationships](../../relational-databases/tables/create-foreign-key-relationships.md)를 참조하세요.  
  
###  <a name="TsqlExample"></a>  
