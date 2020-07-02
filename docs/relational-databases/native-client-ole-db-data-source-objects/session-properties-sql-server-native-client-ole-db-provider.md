---
title: 세션 속성 OLE DB
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 2498fbad-b3db-4bea-8fc6-fef5317d3eba
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a354a5b37c7c5ee275d51b0aab6571a6ebecac51
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85785532"
---
# <a name="session-properties---sql-server-native-client-ole-db-provider"></a>세션 속성 - SQL Server Native Client OLE DB 공급자
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 OLE DB 세션 속성을 다음과 같이 해석 합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 비정상 수준 DBPROPVAL_TI_CHAOS를 제외 하 고 모든 자동 커밋 트랜잭션 격리 수준을 지원 합니다.|  
|||

 공급자별 속성 집합 DBPROPSET_SQLSERVERSESSION에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 다음과 같은 추가 세션 속성을 정의 합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|유형: VT_BOOL<br /><br /> R/W: 읽기/쓰기<br /><br /> Default: VARIANT_FALSE<br /><br /> 설명: CATALOG 제한에서 허용되는 따옴표 붙은 식별자입니다.<br /><br /> VARIANT_TRUE: 따옴표 붙은 식별자는 분산 쿼리 지원을 제공하는 스키마 행 집합에 대한 카탈로그 제한에서 인식됩니다.<br /><br /> VARIANT_FALSE: 따옴표 붙은 식별자는 분산 쿼리 지원을 제공하는 스키마 행 집합에 대한 카탈로그 제한에서 인식되지 않습니다.<br /><br /> 분산 쿼리 지원을 제공하는 스키마 행 집합에 대한 자세한 내용은 [스키마 행 집합에서 분산 쿼리 지원](../../relational-databases/native-client/ole-db/schema-rowsets-distributed-query-support.md)을 참조하십시오.|  
|SSPROP_ALLOWNATIVEVARIANT|유형: VT_BOOL<br /><br /> R/W: 읽기/쓰기<br /><br /> Default: VARIANT_FALSE<br /><br /> 설명: 데이터가 DBTYPE_VARIANT 또는 DBTYPE_SQLVARIANT로 인출되는지를 결정합니다.<br /><br /> VARIANT_TRUE: 열 유형이 DBTYPE_SQLVARIANT로 반환되고, 이 경우 버퍼에 SSVARIANT 구조가 포함됩니다.<br /><br /> VARIANT_FALSE: 열 유형이 DBTYPE_VARIANT로 반환되고, 이 경우 버퍼에 VARIANT 구조가 포함됩니다.|  
|SSPROP_ASYNCH_BULKCOPY|비동기 모드를 사용하려면 BCPExec 메서드를 호출하기 전에 공급자별 세션 속성 SSPROP_ASYNCH_BULKCOPY를 VARIANT_TRUE로 설정합니다. 이 속성은 DBPROPSET_SQLSERVERSESSION 속성 집합에서 사용할 수 있습니다.|  
|||

## <a name="see-also"></a>참고 항목  
 [데이터 원본 개체 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
