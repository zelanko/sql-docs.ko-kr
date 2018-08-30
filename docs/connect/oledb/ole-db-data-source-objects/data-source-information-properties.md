---
title: 데이터 원본 정보 속성 | Microsoft Docs
description: 데이터 원본 정보 속성
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- information properties [OLE DB]
- OLE DB data source properties [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 06a6f4152876f123d1e7fc7ecaf009061d10aa59
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031956"
---
# <a name="data-source-information-properties"></a>데이터 원본 정보 속성
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  공급자별 속성 집합 DBPROPSET_SQLSERVERDATASOURCEINFO에서 SQL Server용 OLE DB 드라이버는 다음과 같은 데이터 원본 정보 속성을 정의합니다.  
  
|속성 ID|설명|  
|-----------------|-----------------|  
|SSPROP_COLUMNLEVELCOLLATION|형식: VT_BOOL<br /><br /> R/w: 읽기<br /><br /> 기본값: VARIANT_TRUE<br /><br /> 설명: 열 데이터 정렬이 지원되는지 확인하는 데 사용됩니다.<br /><br /> VARIANT_TRUE: 열 수준 데이터 정렬을 사용할 수 있습니다.<br /><br /> VARIANT_FALSE: 열 수준 데이터 정렬이 지원 되지 않습니다.|  
|SSPROP_UNICODELCID|형식: VT_I4 R/w: 읽기<br /><br /> 설명: 유니코드 로캘 id입니다.<br /><br /> 유니코드 데이터 정렬에 사용되는 로캘입니다.|  
|SSPROP_UNICODECOMPARISONSTYLE|형식: VT_I4 R/w: 읽기<br /><br /> 설명: 유니코드 비교 스타일입니다.<br /><br /> 유니코드 데이터 정렬에 사용되는 정렬 옵션입니다.|  
  
 공급자별 속성 집합 DBPROPSET_SQLSERVERSTREAM에서 SQL Server용 OLE DB 드라이버는 다음과 같은 추가 속성을 정의합니다.  
  
|속성 ID|설명|  
|-----------------|-----------------|  
|SSPROP_STREAM_XMLROOT|유형: VT_BSTR R/w: 읽기/쓰기<br /><br /> 설명: FOR XML 쿼리 결과가 올바른 형식의 문서가 아닐 수 있습니다. 이 속성을 지정 하는 경우, 결과 ' 선택... XML에 대 한 ' 쿼리는 올바른 형식의 XML 문서가 반환 하도록이 속성에 제공한 루트 태그에 래핑됩니다. 쿼리가 브라우저에서 실행되는 경우에는 결과를 로드할 때 브라우저에서 파서 오류가 표시될 수 있습니다. 오류를 방지하기 위해 SQL ISAPI는 ROOT 키워드를 지원합니다. 이 키워드는 SSPROP_STREAM_XMLROOT 속성에 매핑됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 원본 개체 &#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
