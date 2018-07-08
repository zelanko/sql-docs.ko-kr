---
title: 세션 속성-SQL Server Native Client OLE DB 공급자 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 2498fbad-b3db-4bea-8fc6-fef5317d3eba
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ea5483a18ddd3bdb7735e0a2c04e347369240551
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37415532"
---
# <a name="session-properties---sql-server-native-client-ole-db-provider"></a>세션 속성-SQL Server Native Client OLE DB 공급자
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 OLE DB 세션 속성을 다음과 같이 해석 합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 함 수준 DBPROPVAL_TI_CHAOS 제외 하 고 모든 자동 커밋 트랜잭션 격리 수준을 지원 합니다.|  
  
 공급자별 속성 집합 DBPROPSET_SQLSERVERSESSION에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 다음과 같은 추가 세션 속성을 정의 합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|형식: VT_BOOL<br /><br /> R/w: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: Quoted 카탈로그 제한에서 허용 하는 식별자입니다.<br /><br /> VARIANT_TRUE: 따옴표 붙은 식별자는 분산된 쿼리 지원을 제공 하는 스키마 행 집합에 대 한 카탈로그 제한에 대 한 인식 됩니다.<br /><br /> VARIANT_FALSE: 따옴표 붙은 식별자는 분산된 쿼리 지원을 제공 하는 스키마 행 집합에 대 한 카탈로그 제한에 대 한 인식 되지 않습니다.<br /><br /> 분산된 쿼리 지원을 제공 하는 스키마 행 집합에 대 한 자세한 내용은 참조 하세요. [스키마 행 집합에서 분산 쿼리 지원](../../relational-databases/native-client/ole-db/schema-rowsets-distributed-query-support.md)합니다.|  
|SSPROP_ALLOWNATIVEVARIANT|형식: VT_BOOL<br /><br /> R/w: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: DBTYPE_VARIANT 또는 DBTYPE_SQLVARIANT로 인출 하는 데이터를 결정 합니다.<br /><br /> VARIANT_TRUE: 열 유형이 DBTYPE_SQLVARIANT로 반환 되는 경우 버퍼에 SSVARIANT 구조가 포함 됩니다.<br /><br /> VARIANT_FALSE: 열 유형이 DBTYPE_VARIANT로 반환 되 고 버퍼에 VARIANT 구조가 포함 됩니다.|  
|SSPROP_ASYNCH_BULKCOPY|비동기 모드를 사용하려면 BCPExec 메서드를 호출하기 전에 공급자별 세션 속성 SSPROP_ASYNCH_BULKCOPY를 VARIANT_TRUE로 설정합니다. 이 속성은 DBPROPSET_SQLSERVERSESSION 속성 집합에서 사용할 수 있습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 원본 개체 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
