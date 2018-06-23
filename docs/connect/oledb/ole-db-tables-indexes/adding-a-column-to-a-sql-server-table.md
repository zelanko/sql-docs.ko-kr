---
title: SQL Server 테이블에 열 추가 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버를 사용 하 여 SQL Server 테이블에 열 추가
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- AddColumn function
- OLE DB Driver for SQL Server, columns
- adding columns
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 3e68b78a72657648320f4948646e4685cfbad388
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/16/2018
ms.locfileid: "35690296"
---
# <a name="adding-a-column-to-a-sql-server-table"></a>SQL Server 테이블에 열 추가
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 노출 된 **ITableDefinition::AddColumn** 함수입니다. 이렇게 하면 소비자가 열을 추가할 수는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블입니다.  
  
 열을 추가 하는 경우는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블 OLE DB Driver SQL Server 소비자가 다음과 같이 제한 됩니다.  
  
-   DBPROP_COL_AUTOINCREMENT가 VARIANT_TRUE이면 DBPROP_COL_NULLABLE은 VARIANT_FALSE여야 합니다.  
  
-   사용 하 여 열이 정의 하는 경우는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **타임 스탬프** 데이터 형식, dbprop_col_nullable은 VARIANT_FALSE 여야 합니다.  
  
-   다른 모든 열 정의에서 DBPROP_COL_NULLABLE은 VARIANT_TRUE여야 합니다.  
  
 소비자의 유니코드 문자열에서 테이블 이름을 지정는 *pwszName* 의 멤버는 *uName* 공용 구조체는 *pTableID* 매개 변수입니다. *eKind* 소속 *pTableID* DBKIND_NAME 이어야 합니다.  
  
 새 열 이름에 유니코드 문자열로 지정는 *pwszName* 의 멤버는 *uName* 공용 구조체는 *dbcid* DBCOLUMNDESC매개변수는멤버*pColumnDesc*합니다. *eKind* 멤버는 DBKIND_NAME 이어야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 및 인덱스](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)  
  
  
