---
title: SQL Server 인덱스를 삭제 하는 중 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버를 사용 하 여 sql server 인덱스 삭제
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b16b3ece0b28951beee1800216897468e21e87ab
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="dropping-a-sql-server-index"></a>SQL Server 인덱스 삭제

  OLE DB Driver for SQL Server 노출 된 **iindexdefinition:: Dropindex** 함수입니다. 이렇게 하면 인덱스를 제거 하려면 소비자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블입니다.  
  
 일부는 OLE DB Driver for SQL Server 노출 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인덱스와 PRIMARY KEY 및 UNIQUE 제약 조건입니다. 테이블 소유자, 데이터베이스 소유자 및 일부 관리 역할 멤버를 수정할 수는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블, 제약 조건 삭제 합니다. 기본적으로 테이블 소유자만 기존 인덱스를 삭제할 수 있습니다. 따라서 **DropIndex** 표시 된 인덱스의 형식에도 응용 프로그램 사용자의 액세스 권한 뿐만 아니라에 따라 달라 집니다 성공 또는 실패 합니다.  
  
 소비자의 유니코드 문자열에서 테이블 이름을 지정는 *pwszName* 의 멤버는 *uName* 공용 구조체는 *pTableID* 매개 변수입니다. *eKind* 소속 *pTableID* DBKIND_NAME 이어야 합니다.  
  
 인덱스 이름을 유니코드 문자열에으로 지정 하는 소비자는 *pwszName* 의 멤버는 *uName* 공용 구조체의 *pIndexID* 매개 변수. *eKind* 소속 *pIndexID* DBKIND_NAME 이어야 합니다. OLE DB Driver for SQL Server 테이블에서 모든 인덱스를 삭제의 OLE DB 기능을 지원 하지 않으면 때 *pIndexID* null입니다. 경우 *pIndexID* 가 null 이면 E_INVALIDARG가 반환 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 및 인덱스](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)   
 [DROP INDEX&#40;Transact-SQL&#41;](../../../t-sql/statements/drop-index-transact-sql.md)  
  
  
