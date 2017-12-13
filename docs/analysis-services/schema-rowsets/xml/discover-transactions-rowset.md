---
title: "DISCOVER_TRANSACTIONS 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 85789177-c5df-4336-a90c-c20d69277ab4
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4cc8bdd0f4c3a4b212661e4ac9363ce6bdefb64f
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="discovertransactions-rowset"></a>DISCOVER_TRANSACTIONS 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]시스템에서 보류 중인 트랜잭션의 현재 집합을 반환합니다.  
  
 **적용 대상:** 테이블 형식 모델, 다차원 모델  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_TRANSACTIONS** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|Description|  
|-----------------|--------------------|-----------------|  
|**TRANSACTION_ID**|**DBTYPE_WSTR**|GUID와 같은 트랜잭션 고유 식별자입니다.|  
|**TRANSACTION_SESSION_ID**|**DBTYPE_WSTR**|GUID와 같은 트랜잭션 세션 고유 식별자입니다.|  
|**TRANSACTION_START_TIME**|**DBTYPE_DBTIMESTAMP**|트랜잭션이 시작된 서버 UTC 날짜 및 시간입니다.|  
|**TRANSACTION_ELAPSED_TIME_MS**|**DBTYPE_I8**|트랜잭션이 시작된 이후에 경과된 시간(밀리초)입니다.|  
|**TRANSACTION_CPU_TIME_MS**|**DBTYPE_I8**|트랜잭션이 시작된 이후 모든 요청에 사용된 CPU 시간(밀리초)입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **DISCOVER_TRANSACTIONS** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|**열 이름**|**유형 표시기**|**제한 상태**|  
|---------------------|------------------------|---------------------------|  
|**ID**|**DBTYPE_WSTR**|(선택 사항)|  
|**SESSION_ID**|**DBTYPE_WSTR**|(선택 사항)|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>ADOMD.NET을 사용하여 행 집합 반환  
 ADOMD.NET 및 스키마 행 집합을 사용하여 메타데이터를 검색할 때 GUID 또는 문자열을 사용하여 GetSchemaDataSet 메서드의 스키마 행 집합 개체를 참조할 수 있습니다. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)을 참조하세요.  
  
 다음 표에서는 이 행 집합을 식별하는 GUID와 문자열 값을 제공합니다.  
  
|인수|값|  
|--------------|-----------|  
|GUID|a07ccd28-8148-11d0-87bb-00c04fc33942|  
|문자열|DISCOVER_TRANSACTIONS|  
  
## <a name="see-also"></a>관련 항목:  
 [XML for Analysis 스키마 행 집합](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
