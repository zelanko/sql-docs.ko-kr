---
title: 테이블 업데이트 대화 상자
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.updatetable
- vdtsql.chm:69643
ms.assetid: 174c7275-5b15-42a9-b172-5ff30de575a1
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 19251316d4674ad7632c6f220f85e2178f4365ca
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86004126"
---
# <a name="update-table-dialog-box-visual-database-tools"></a>테이블 업데이트 대화 상자(Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 대화 상자를 사용하면 업데이트할 테이블을 지정할 수 있습니다.

이 대화 상자는 다이어그램 창에 두 개 이상의 테이블이 표시되어 있는 상태에서 쿼리 형식을 업데이트 쿼리로 변경하는 경우에 나타납니다.  

업데이트하려는 테이블을 선택한 다음, **확인**을 선택합니다.

> [!NOTE]
> 테이블이 복제용으로 게시된 경우 Transact-SQL 문 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 또는 SMO(SQL Server 관리 개체)를 사용하여 스키마를 변경해야 합니다. 테이블 디자이너 또는 데이터베이스 다이어그램 디자이너를 사용하여 스키마를 변경하면 테이블 삭제 및 재생성이 시도됩니다. 게시된 개체를 삭제할 수 없으므로 스키마가 변경되지 않습니다.

## <a name="see-also"></a>참고 항목

[업데이트 쿼리 만들기](../../ssms/visual-db-tools/create-update-queries-visual-database-tools.md)