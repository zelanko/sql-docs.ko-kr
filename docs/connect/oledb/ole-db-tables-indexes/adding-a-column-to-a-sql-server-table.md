---
title: SQL Server 테이블에 열 추가 | Microsoft Docs
description: OLE DB Driver for SQL Server를 사용하여 SQL Server 테이블에 열 추가
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- AddColumn function
- OLE DB Driver for SQL Server, columns
- adding columns
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 2c6cd539e499f80342a30371d047c9870c4fda08
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67994098"
---
# <a name="adding-a-column-to-a-sql-server-table"></a>SQL Server 테이블에 열 추가
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server는 **ITableDefinition::AddColumn** 함수를 노출합니다. 소비자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블에 열을 추가할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블에 열을 추가하는 경우 OLE DB Driver for SQL Server 소비자는 다음과 같이 제한됩니다.  
  
-   DBPROP_COL_AUTOINCREMENT가 VARIANT_TRUE이면 DBPROP_COL_NULLABLE은 VARIANT_FALSE여야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**timestamp** 데이터 형식을 사용하여 열을 정의하는 경우 DBPROP_COL_NULLABLE은 VARIANT_FALSE여야 합니다.  
  
-   다른 모든 열 정의에서 DBPROP_COL_NULLABLE은 VARIANT_TRUE여야 합니다.  
  
 소비자는 *pTableID* 매개 변수에서 *uName* 공용 구조체의 *pwszName* 멤버에 테이블 이름을 유니코드 문자열로 지정합니다. *pTableID*의 *eKind* 멤버는 DBKIND_NAME이어야 합니다.  
  
 새로운 열 이름은 DBCOLUMNDESC 매개 변수 *pColumnDesc*의 *dbcid* 멤버에 있는 *uName* 공용 구조체의 *pwszName* 멤버에서 유니코드 문자열로 지정됩니다. *eKind* 멤버는 DBKIND_NAME이어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 및 인덱스](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)  
  
  
