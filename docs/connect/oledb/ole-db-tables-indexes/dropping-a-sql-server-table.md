---
title: SQL Server 테이블 삭제 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버를 사용 하 여 SQL Server 테이블 삭제
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
- tables [OLE DB]
- deleting tables
- OLE DB Driver for SQL Server, tables
- removing tables
- dropping tables
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bd9dd493a114475e9f0ca5c14cd32a9418931b9b
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="dropping-a-sql-server-table"></a>SQL Server 테이블 삭제
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB Driver for SQL Server 노출는 **ITableDefinition::DropTable** 함수를 제거 하는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스의에서 테이블입니다.  
  
 유니코드 문자열에서 테이블 이름을 지정는 *pwszName* 의 멤버는 *uName* 공용 구조체는 *pTableID* 매개 변수입니다. *eKind* 소속 *pTableID* DBKIND_NAME 이어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 및 인덱스](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
