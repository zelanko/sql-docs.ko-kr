---
title: 세션 속성 - SQL Server용 OLE DB 드라이버 | Microsoft Docs
description: 세션 속성 - SQL Server용 OLE DB 드라이버
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- OLE DB Driver for SQL Server, sessions
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 5e92d569c3a370e24765b80f9c873a50e16d8fda
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86004918"
---
# <a name="session-properties---ole-db-driver-for-sql-server"></a>세션 속성 - SQL Server용 OLE DB 드라이버
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server는 OLE DB 세션 속성을 다음과 같이 해석합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|SQL Server용 OLE DB 드라이버는 격리 안 함 수준 DBPROPVAL_TI_CHAOS를 제외하고 모든 자동 커밋 트랜잭션 격리 수준을 지원합니다.|  
  
 SQL Server용 OLE DB 드라이버는 공급자별 속성 집합 DBPROPSET_SQLSERVERSESSION에서 다음과 같은 추가 세션 속성을 정의합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|유형: VT_BOOL<br /><br /> R/W: 읽기/쓰기<br /><br /> Default: VARIANT_FALSE<br /><br /> 설명: CATALOG 제한에서 허용되는 따옴표 붙은 식별자입니다.<br /><br /> VARIANT_TRUE: 따옴표 붙은 식별자는 분산 쿼리 지원을 제공하는 스키마 행 집합에 대한 카탈로그 제한에서 인식됩니다.<br /><br /> VARIANT_FALSE: 따옴표 붙은 식별자는 분산 쿼리 지원을 제공하는 스키마 행 집합에 대한 카탈로그 제한에서 인식되지 않습니다.<br /><br /> 분산 쿼리 지원을 제공하는 스키마 행 집합에 대한 자세한 내용은 [스키마 행 집합에서 분산 쿼리 지원](../../oledb/ole-db/schema-rowsets-distributed-query-support.md)을 참조하십시오.|  
|SSPROP_ALLOWNATIVEVARIANT|유형: VT_BOOL<br /><br /> R/W: 읽기/쓰기<br /><br /> Default: VARIANT_FALSE<br /><br /> 설명: 데이터가 DBTYPE_VARIANT 또는 DBTYPE_SQLVARIANT로 페치되는지를 결정합니다.<br /><br /> VARIANT_TRUE: 열 유형이 DBTYPE_SQLVARIANT로 반환되고, 이 경우 버퍼에 SSVARIANT 구조체가 포함됩니다.<br /><br /> VARIANT_FALSE: 열 형식이 DBTYPE_VARIANT로 반환되고, 이 경우 버퍼에 VARIANT 구조가 포함됩니다.|  
|SSPROP_ASYNCH_BULKCOPY|비동기 모드를 사용하려면 BCPExec 메서드를 호출하기 전에 공급자별 세션 속성 SSPROP_ASYNCH_BULKCOPY를 VARIANT_TRUE로 설정합니다. 이 속성은 DBPROPSET_SQLSERVERSESSION 속성 집합에서 사용할 수 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 원본 개체 &#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
