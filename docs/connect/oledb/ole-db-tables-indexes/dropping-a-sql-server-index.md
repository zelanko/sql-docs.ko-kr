---
title: SQL Server 인덱스 삭제 | Microsoft Docs
description: OLE DB Driver for SQL Server를 사용하여 SQL Server 인덱스 삭제
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 708deecefe451115ca0fca97075f88311dec2f5a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015247"
---
# <a name="dropping-a-sql-server-index"></a>SQL Server 인덱스 삭제
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server는 **IIndexDefinition::DropIndex** 함수를 노출합니다. 이 함수를 사용하여 소비자는 인덱스를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블에서 제거할 수 있습니다.  
  
 OLE DB Driver for SQL Server는 일부 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PRIMARY KEY 및 UNIQUE 제약 조건을 인덱스로 노출합니다. 테이블 소유자, 데이터베이스 소유자 및 일부 관리 역할 멤버는 제약 조건을 삭제하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블을 수정할 수 있습니다. 기본적으로 테이블 소유자만 기존 인덱스를 삭제할 수 있습니다. 따라서 **DropIndex** 성공 또는 실패 여부는 애플리케이션 사용자의 액세스 권한뿐만 아니라 해당 인덱스의 유형에 따라서도 좌우됩니다.  
  
 소비자는 *pTableID* 매개 변수에서 *uName* 공용 구조체의 *pwszName* 멤버에 테이블 이름을 유니코드 문자열로 지정합니다. *pTableID*의 *eKind* 멤버는 DBKIND_NAME이어야 합니다.  
  
 소비자는 *pIndexID* 매개 변수에서 *uName* 공용 구조체의 *pwszName* 멤버에 인덱스 이름을 유니코드 문자열로 지정합니다. *pIndexID*의 *eKind* 멤버는 DBKIND_NAME이어야 합니다. SQL Server용 OLE DB 드라이버는 *pIndexID*가 null인 경우 테이블의 모든 인덱스를 삭제하는 OLE DB 기능을 지원하지 않습니다. *pIndexID*가 null이면 E_INVALIDARG가 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 및 인덱스](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)   
 [DROP INDEX&#40;Transact-SQL&#41;](../../../t-sql/statements/drop-index-transact-sql.md)  
  
  
