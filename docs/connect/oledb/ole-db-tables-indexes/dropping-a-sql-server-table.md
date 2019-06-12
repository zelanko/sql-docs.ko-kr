---
title: SQL Server 테이블 삭제 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버를 사용 하 여 SQL Server 테이블 삭제
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- deleting tables
- OLE DB Driver for SQL Server, tables
- removing tables
- dropping tables
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: f743194d0036d338ad39594d7c7f00665d83a224
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66766234"
---
# <a name="dropping-a-sql-server-table"></a>SQL Server 테이블 삭제
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 노출 합니다 **ITableDefinition::DropTable** 제거 하는 함수는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스의에서 테이블입니다.  
  
 소비자는 *pTableID* 매개 변수에서 *uName* 공용 구조체의 *pwszName* 멤버에 테이블 이름을 유니코드 문자열로 지정합니다. *pTableID*의 *eKind* 멤버는 DBKIND_NAME이어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 및 인덱스](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
