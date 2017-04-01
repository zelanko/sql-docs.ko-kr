---
title: "공간 인덱스 만들기, 수정 및 삭제 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-spatial"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "인덱스 [SQL Server], 만들기"
  - "공간 인덱스 [SQL Server], 삭제"
  - "공간 인덱스 [SQL Server], 만들기"
  - "인덱스 [SQL Server], 삭제"
  - "인덱스 [SQL Server], 수정"
  - "공간 인덱스 [SQL Server], 수정"
ms.assetid: 00c1b927-8ec5-44cf-87c2-c8de59745735
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# 공간 인덱스 만들기, 수정 및 삭제
  공간 인덱스는 **geometry** 또는 **geography** 데이터 형식의 열(*공간 열*)에서 특정 작업을 좀 더 효율적으로 수행할 수 있습니다. 하나의 공간 열에 두 개 이상의 공간 인덱스가 지정될 수 있습니다. 예를 들어 이 기능은 단일 열에 다른 공간 분할 매개 변수를 인덱싱할 경우에 유용합니다.  
  
 공간 인덱스를 만드는 작업에 대한 제한 사항이 많이 있습니다. 자세한 내용은 이 항목의 [공간 인덱스의 제한 사항](#restrictions) 을 참조하십시오.  
  
> [!NOTE]  
>  공간 인덱스와 파티션 및 파일 그룹의 관계에 대한 자세한 내용은 [CREATE SPATIAL INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)의 "주의" 섹션을 참조하세요.  
  
##  <a name="creating"></a> 공간 인덱스 만들기, 수정 및 삭제  
  
###  <a name="create"></a> 공간 인덱스를 만들려면  
 **Transact-SQL을 사용하여 공간 인덱스를 만들려면**  
 [CREATE SPATIAL INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)  
  
 **Management Studio의 새 인덱스 대화 상자를 사용하여 공간 인덱스를 만들려면**  
 ##### Management Studio에서 공간 인덱스를 만들려면  
  
1.  개체 탐색기에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 지정한 인덱스가 있는 테이블이 포함된 데이터베이스를 확장한 다음 **테이블**을 확장합니다.  
  
3.  인덱스를 만들 테이블을 확장합니다.  
  
4.  **인덱스**를 마우스 오른쪽 단추로 클릭하고 **새 인덱스**를 선택합니다.  
  
5.  **인덱스 이름** 필드에 인덱스의 이름을 입력합니다.  
  
6.  **인덱스 유형** 드롭다운 목록에서 **공간**을 선택합니다.  
  
7.  인덱싱하려는 공간 열을 지정하려면 **추가**를 클릭합니다.  
  
8.  *\<테이블 이름>***에서 열 선택** 대화 상자에서 해당 확인란을 선택하여 **geometry** 또는 **geography** 형식의 열을 선택합니다. 그러면 다른 공간 열이 편집할 수 없게 됩니다. 다른 공간 열을 선택하려면 먼저 현재 선택된 열의 선택을 취소해야 합니다. 완료되었으면 **확인**을 클릭합니다.  
  
9. **인덱스 키 열** 표에서 열 선택 사항을 확인합니다.  
  
10. **인덱스 속성** 대화 상자의 **페이지 선택** 창에서 **공간**을 클릭합니다.  
  
11. **공간** 페이지에서 인덱스의 공간 속성에 사용할 값을 지정합니다.  
  
     **geometry** 형식 열에서 인덱스를 만들 경우 경계 상자의 **(***X-min***,***Y-min***)** 및 **(***X-max***,***Y-max***)** 좌표를 지정해야 합니다. **geography** 형식 열의 인덱스의 경우 **지리 표** 공간 분할 구성표를 지정하면 지리 표 공간 분할이 경계 상자를 사용하지 않으므로 경계 상자 필드는 읽기 전용이 됩니다.  
  
     필요에 따라 공간 분할(tessellation) 구성표의 모든 수준에서 표 밀도 및 **개체당 셀 수** 필드에 대해 기본값이 아닌 값을 지정할 수 있습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 또는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상의 경우 개체당 기본 셀 수는 각각 16과 8이고, 기본 표 밀도는 **의 경우** 보통 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]입니다.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 공간 분할(tessellation) 구성표의 GEOMETRY_AUTO_GRID 또는 GEOGRAPHY_AUTO_GRID를 선택할 수 있습니다. GEOMETRY_AUTO_GRID 또는 GEOGRAPHY_AUTO_GRID를 선택한 경우 수준 1, 수준 2, 수준 3 및 수준 4 표 밀도 옵션은 사용할 수 없습니다.  
  
     이러한 속성에 대한 자세한 내용은 [Index Properties F1 Help](../../relational-databases/indexes/index-properties-f1-help.md)을 참조하십시오.  
  
12. **확인**을 클릭합니다.  
  
> [!NOTE]  
>  같은 공간 열 또는 다른 공간 열에 공간 인덱스를 더 만들려면 위 단계를 반복하십시오.  
  
 [항목 내용](#TOP)  
  
 **Management Studio의 테이블 디자이너를 사용하여 공간 인덱스를 만들려면**  
 ##### 테이블 디자이너에서 공간 인덱스를 만들려면  
  
1.  개체 탐색기에서 공간 인덱스를 만들려는 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 클릭합니다.  
  
     테이블 디자이너에서 테이블이 열립니다.  
  
2.  인덱스에 대해 **geometry** 또는 **geography** 열을 선택합니다.  
  
3.  **테이블 디자이너** 메뉴에서 **공간 인덱스**를 클릭합니다.  
  
4.  **공간 인덱스** 대화 상자에서 **추가**를 클릭합니다.  
  
5.  **선택한 공간 인덱스** 목록에서 새 인덱스를 선택하고 오른쪽에 있는 표에서 공간 인덱스의 속성을 설정합니다. 속성에 대한 자세한 내용은 [공간 인덱스 대화 상자&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/spatial-indexes-dialog-box-visual-database-tools.md)를 참조하세요.  
  
 [항목 내용](#TOP)  
  
###  <a name="alter"></a> 공간 인덱스를 변경하려면  
  
-   [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
    > [!IMPORTANT]  
    >  공간 인덱스에 지정된 옵션(예: BOUNDING_BOX 또는 GRID)을 변경하려면 DROP_EXISTING = ON을 지정하는 CREATE SPATIAL INDEX 문을 사용하거나 해당 공간 인덱스를 삭제하고 새로 만들 수 있습니다. 예제를 보려면 [CREATE SPATIAL INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)를 참조하세요.  
  
-   [인덱스 수정](../../relational-databases/indexes/modify-an-index.md)  
  
-   [다른 파일 그룹으로 기존 인덱스 이동](../../relational-databases/indexes/move-an-existing-index-to-a-different-filegroup.md)  
  
 [항목 내용](#TOP)  
  
###  <a name="drop"></a> 공간 인덱스를 삭제하려면  
 **Transact-SQL을 사용하여 공간 인덱스를 삭제하려면**  
 [DROP INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
 **Management Studio를 사용하여 인덱스를 삭제하려면**  
 [인덱스 삭제](../../relational-databases/indexes/delete-an-index.md)  
  
 **Management Studio의 테이블 디자이너를 사용하여 공간 인덱스를 삭제하려면**  
 ##### 테이블 디자이너에서 공간 인덱스를 삭제하려면  
  
1.  개체 탐색기에서 삭제하려는 공간 인덱스가 포함된 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 클릭합니다.  
  
     테이블 디자이너에서 테이블이 열립니다.  
  
2.  **테이블 디자이너** 메뉴에서 **공간 인덱스**를 클릭합니다.  
  
     **공간 인덱스** 대화 상자가 나타납니다.  
  
3.  **선택한 공간 인덱스** 열에서 삭제하려는 인덱스를 클릭합니다.  
  
4.  **삭제**를 클릭합니다.  
  
 [항목 내용](#TOP)  
  
##  <a name="restrictions"></a> 공간 인덱스의 제한 사항  
 공간 인덱스는 **기하학** 또는 **지리**유형의 열에서만 만들 수 있습니다.  
  
### 테이블 및 뷰 제한 사항  
 공간 인덱스는 기본 키가 있는 테이블에서만 정의할 수 있습니다. 테이블의 최대 기본 키 열 수는 15개입니다.  
  
 인덱스 키 레코드의 최대 크기는 895바이트입니다. 크기가 더 커지면 오류가 발생합니다.  
  
> [!NOTE]  
>  테이블에 공간 인덱스가 정의되는 동안 기본 키 메타데이터를 변경할 수 없습니다.  
  
 공간 인덱스는 인덱싱된 뷰에 지정할 수 없습니다.  
  
### 여러 공간 인덱스 제한 사항  
 지원되는 테이블의 공간 열에 공간 인덱스를 249개까지 만들 수 있습니다. 예를 들면 동일한 공간 열에 공간 인덱스를 한 개 이상 만드는 것이 하나의 열에 있는 서로 다른 공간 분할 매개 변수를 인덱싱하는 데 유용할 수 있습니다.  
  
 공간 인덱스는 한 번에 하나씩만 만들 수 있습니다.  
  
### 공간 인덱스 및 프로세스 병렬 처리  
 인덱스 작성 작업은 사용 가능한 프로세스 병렬 처리를 사용할 수 있습니다.  
  
### 버전 제한 사항  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 에 도입된 공간 분할(tessellation)은 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 또는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]로 복제할 수 없습니다. [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 또는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 데이터베이스와의 호환성이 요구되는 경우 공간 인덱스에는 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 또는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 공간 분할을 사용해야 합니다.  
  
 [항목 내용](#TOP)  
  
## 참고 항목  
 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  