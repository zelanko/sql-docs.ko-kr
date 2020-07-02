---
title: LINKEDSERVERS 행 집합(OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- LINKEDSERVERS rowset
- enumerating data sources [OLE DB]
ms.assetid: 2633fd8a-65e7-498d-9aed-8e4b1cca2381
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8e4d0c26821cfc9870dc2e5f01f7927257599fe4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787686"
---
# <a name="schema-rowsets---linkedservers-rowset"></a>스키마 행 집합 - LINKEDSERVERS 행 집합
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  **LINKEDSERVERS** 행 집합은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 분산 쿼리에 참여할 수 있는 조직 데이터 원본을 열거합니다.  
  
 **LINKEDSERVERS** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|설명|  
|-----------------|--------------------|-----------------|  
|SVR_NAME|DBTYPE_WSTR|연결된 서버의 이름입니다.|  
|SVR_PRODUCT|DBTYPE_WSTR|연결된 서버 이름이 나타내는 데이터 저장소 유형을 식별하는 제조업체 또는 기타 이름입니다.|  
|SVR_PROVIDERNAME|DBTYPE_WSTR|서버 데이터를 이용할 때 사용되는 OLE DB 공급자의 이름입니다.|  
|SVR_DATASOURCE|DBTYPE_WSTR|공급자의 데이터 원본을 가져올 때 사용되는 OLE DB DBPROP_INIT_DATASOURCE 문자열입니다.|  
|SVR_PROVIDERSTRING|DBTYPE_WSTR|공급자의 데이터 원본을 가져올 때 사용되는 OLE DB DBPROP_INIT_PROVIDERSTRING 값입니다.|  
|SVR_LOCATION|DBTYPE_WSTR|공급자의 데이터 원본을 가져올 때 사용되는 OLE DB DBPROP_INIT_LOCATION 문자열입니다.|  
  
 행 집합은 SRV_NAME을 기준으로 정렬되며 SRV_NAME에서 하나의 제한이 지원됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [스키마 행 집합 지원&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)  
  
  
