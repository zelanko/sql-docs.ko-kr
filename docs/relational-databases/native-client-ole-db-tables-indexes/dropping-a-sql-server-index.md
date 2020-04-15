---
title: SQL Server 인덱스 삭제 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
ms.assetid: add3ba14-10b1-4723-b7c0-3e83689e9fdd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3143dc794e3c75ec1473529ec018c476edd3e687
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303014"
---
# <a name="dropping-a-sql-server-index"></a>SQL Server 인덱스 삭제

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자는 **IIndexDefinition::DropIndex** 함수를 노출합니다. 이 함수를 사용하여 소비자는 인덱스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에서 제거할 수 있습니다.  
  
 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자는 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 키 및 고유 제약 조건을 인덱스로 노출합니다. 테이블 소유자, 데이터베이스 소유자 및 일부 관리 역할 멤버는 제약 조건을 삭제하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 수정할 수 있습니다. 기본적으로 테이블 소유자만 기존 인덱스를 삭제할 수 있습니다. 따라서 **DropIndex** 성공 또는 실패 여부는 애플리케이션 사용자의 액세스 권한뿐만 아니라 해당 인덱스의 유형에 따라서도 좌우됩니다.  
  
 소비자는 *pTableID* 매개 변수에서 *uName* 공용 구조체의 *pwszName* 멤버에 테이블 이름을 유니코드 문자열로 지정합니다. *pTableID*의 *eKind* 멤버는 DBKIND_NAME이어야 합니다.  
  
 소비자는 *pIndexID* 매개 변수에서 *uName* 공용 구조체의 *pwszName* 멤버에 인덱스 이름을 유니코드 문자열로 지정합니다. *pIndexID*의 *eKind* 멤버는 DBKIND_NAME이어야 합니다. 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자는 *pIndexID가* null일 때 테이블에 모든 인덱스를 삭제하는 OLE DB 기능을 지원하지 않습니다. *pIndexID*가 null이면 E_INVALIDARG가 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 및 인덱스](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)   
 [테이블 변경 &#40;거래 SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
  
