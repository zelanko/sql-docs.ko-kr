---
title: 데이터 원본 정보 속성 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- information properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 7fd80e47-5bd9-41e2-a3d3-091a7c8c5f2b
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1a272a93d0148524da2def06fb8b4bbc121a9b0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68128689"
---
# <a name="data-source-information-properties"></a>데이터 원본 정보 속성
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 공급자별 속성 집합 DBPROPSET_SQLSERVERDATASOURCEINFO에 다음과 같은 데이터 원본 정보 속성을 정의합니다.  
  
|속성 ID|설명|  
|-----------------|-----------------|  
|SSPROP_COLUMNLEVELCOLLATION|형식: VT_BOOL<br /><br /> R/W: 읽기<br /><br /> 기본값: VARIANT_TRUE<br /><br /> 설명: 열 데이터 정렬이 지원 되는지 확인 하는 데 사용 합니다.<br /><br /> VARIANT_TRUE: 열 수준 데이터 정렬을 사용할 수 있습니다.<br /><br /> VARIANT_FALSE: 열 수준 데이터 정렬이 지원 되지 않습니다.|  
|SSPROP_UNICODELCID|형식: VT_I4 R/W: 읽기<br /><br /> 설명: 유니코드 로캘 id입니다.<br /><br /> 유니코드 데이터 정렬에 사용되는 로캘입니다.|  
|SSPROP_UNICODECOMPARISONSTYLE|형식: VT_I4 R/W: 읽기<br /><br /> 설명: 유니코드 비교 스타일입니다.<br /><br /> 유니코드 데이터 정렬에 사용되는 정렬 옵션입니다.|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 공급자별 속성 집합 DBPROPSET_SQLSERVERSTREAM에 다음과 같은 추가 속성을 정의합니다.  
  
|속성 ID|설명|  
|-----------------|-----------------|  
|SSPROP_STREAM_XMLROOT|형식: VT_BSTR R/W: 읽기/쓰기<br /><br /> 설명: FOR XML 쿼리 결과 올바른 형식의 문서를 사용할 수 없습니다. 이 속성이 지정되면 ‘select ... for XML’ 쿼리의 결과가 이 속성에서 제공한 루트 태그에 래핑되어 올바른 형식의 XML 문서가 반환됩니다. 쿼리가 브라우저에서 실행되는 경우에는 결과를 로드할 때 브라우저에서 파서 오류가 표시될 수 있습니다. 오류를 방지하기 위해 SQL ISAPI는 ROOT 키워드를 지원합니다. 이 키워드는 SSPROP_STREAM_XMLROOT 속성에 매핑됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 원본 개체 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
