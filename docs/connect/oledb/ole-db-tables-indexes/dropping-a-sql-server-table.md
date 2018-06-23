---
title: SQL Server 테이블 삭제 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버를 사용 하 여 SQL Server 테이블 삭제
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
- tables [OLE DB]
- deleting tables
- OLE DB Driver for SQL Server, tables
- removing tables
- dropping tables
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: b035e65082cc15db2af6f06b636adb0ff388f4ec
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689756"
---
# <a name="dropping-a-sql-server-table"></a>SQL Server 테이블 삭제
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 노출는 **ITableDefinition::DropTable** 함수를 제거 하는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스의에서 테이블입니다.  
  
 유니코드 문자열에서 테이블 이름을 지정는 *pwszName* 의 멤버는 *uName* 공용 구조체는 *pTableID* 매개 변수입니다. *eKind* 소속 *pTableID* DBKIND_NAME 이어야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 및 인덱스](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
