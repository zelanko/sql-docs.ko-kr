---
title: 테이블 추가 대화 상자(쿼리 및 뷰 디자이너)(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vdt.dlgbox.query.addtable
- vdtsql.chm:65565
ms.assetid: fce7adcc-4cf5-4a52-9203-11c13d1ecf08
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 87f58c4a1162c061bc62e797ca0ce8cd204edadf
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="add-table-dialog-box-query-and-view-designers-visual-database-tools"></a>테이블 추가 대화 상자(쿼리 및 뷰 디자이너)(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
이 대화 상자를 사용하여 쿼리나 뷰에 테이블, 뷰, 사용자 정의 함수 또는 동의어를 추가할 수 있습니다.  
  
> [!NOTE]  
> 테이블이 복제용으로 게시된 경우 Transact-SQL 문 [ALTER TABLE](http://msdn.microsoft.com/en-us/f1745145-182d-4301-a334-18f799d361d1) 또는 SMO(SQL Server 관리 개체)를 사용하여 스키마를 변경해야 합니다. 테이블 디자이너 또는 데이터베이스 다이어그램 디자이너를 사용하여 스키마를 변경하면 테이블 삭제 및 재생성이 시도됩니다. 게시된 개체를 삭제할 수 없으므로 스키마가 변경되지 않습니다.  
  
## <a name="options"></a>변수  
**테이블**  
**다이어그램** 창에 추가할 수 있는 테이블을 나열합니다. 테이블을 추가하려면 테이블을 선택하고 **추가**를 클릭합니다. 여러 테이블을 한번에 추가하려면 원하는 테이블을 모두 선택하고 **추가**를 클릭합니다.  
  
**뷰**  
**다이어그램** 창에 추가할 수 있는 뷰를 나열합니다. 뷰를 추가하려면 뷰를 선택하고 **추가**를 클릭합니다. 여러 뷰를 한번에 추가하려면 원하는 뷰를 모두 선택하고 **추가**를 클릭합니다.  
  
**함수**  
**다이어그램** 창에 추가할 수 있는 사용자 정의 함수를 나열합니다. 함수를 추가하려면 함수를 선택하고 **추가**를 클릭합니다. 여러 함수를 한번에 추가하려면 원하는 함수를 모두 선택하고 **추가**를 클릭합니다.  
  
**동의어**  
**다이어그램** 창에 추가할 수 있는 동의어를 나열합니다. 동의어를 추가하려면 동의어를 선택하고 **추가**를 클릭합니다. 여러 동의어를 한번에 추가하려면 원하는 동의어를 모두 선택하고 **추가**를 클릭합니다.  
  
**새로 고침**  
목록을 마지막으로 가져온 후에 데이터베이스에서 변경된 내용을 모두 포함하도록 목록을 업데이트합니다.  
  
**추가**  
선택한 하나 이상의 항목을 추가합니다.  
  
## <a name="see-also"></a>참고 항목  
[쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
