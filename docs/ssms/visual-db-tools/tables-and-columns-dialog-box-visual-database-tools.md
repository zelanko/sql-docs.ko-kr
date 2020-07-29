---
title: 테이블 및 열 대화 상자
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.tablesandcolumns
ms.assetid: 8cf27be1-e66d-4735-a428-9ab4b33af4f5
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 21947fabfe87638f233639a8f18e81d0ce8a9965
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86004150"
---
# <a name="tables-and-columns-dialog-box-visual-database-tools"></a>테이블 및 열 대화 상자(Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
이 대화 상자를 사용하면 한 테이블의 기본 키를 다른 테이블의 외래 키에 매핑할 수 있습니다. 이 대화 상자를 열려면 **테이블 디자이너** 메뉴에서 **관계**를 클릭합니다. **외래 키 관계** 대화 상자에서 **테이블 및 열 사양** 필드를 클릭한 다음, 속성의 오른쪽에 있는 줄임표 **(...)** 를 클릭합니다.  
  
> [!NOTE]  
> 테이블이 복제용으로 게시된 경우 Transact-SQL 문 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 또는 SMO(SQL Server 관리 개체)를 사용하여 스키마를 변경해야 합니다. 테이블 디자이너 또는 데이터베이스 다이어그램 디자이너를 사용하여 스키마를 변경하면 테이블 삭제 및 재생성이 시도됩니다. 게시된 개체를 삭제할 수 없으므로 스키마가 변경되지 않습니다.  
  
## <a name="options"></a>옵션  
**관계 이름**  
관계의 이름을 표시합니다.  
  
**기본 키 테이블**  
데이터베이스의 테이블 목록이 표시됩니다. 관계의 기본 키 쪽에 사용할 테이블을 선택할 수 있습니다.  
  
**외래 키 테이블**  
관계의 외래 키 쪽 테이블을 표시합니다. 이 테이블은 테이블 디자이너에 현재 선택되어 있는 테이블입니다.  
  
**기본 키 테이블 아래의 표**  
**기본 키 테이블** 목록에서 선택한 테이블의 열이 나열됩니다. 해당 테이블의 기본 키로 사용되는 열을 입력할 수 있습니다.  
  
**외래 키 테이블 아래의 표**  
**외래 키 테이블** 목록에서 선택한 테이블의 열이 나열됩니다. 기본 키 열에 상응하는 외래 키 테이블의 외래 키 열을 입력할 수 있습니다.  
  
> [!NOTE]  
> 외래 키로 선택한 열의 데이터 형식은 상응하는 기본 키 열의 데이터 형식과 동일해야 합니다. 각 키 열의 수는 동일해야 합니다. 예를 들어 관계의 기본 키 쪽에 있는 테이블의 기본 키가 두 개의 열로 구성되어 있는 경우 이러한 열을 각각 관계의 외래 키 쪽에 있는 테이블의 열에 일치시켜야 합니다.  
  
## <a name="see-also"></a>참고 항목  
[방법: 테이블 간에 관계 만들기(https://msdn.microsoft.com/867a54b8-5be4-46e6-9702-49ae6dabf67c)  
  
