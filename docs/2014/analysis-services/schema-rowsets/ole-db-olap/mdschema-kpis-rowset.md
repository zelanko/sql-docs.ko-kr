---
title: MDSCHEMA_KPIS 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MDSCHEMA_KPIS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_KPIS rowset
ms.assetid: 40fb5112-6a90-4455-82b3-8b6322490222
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 28a5f4af179c058f822a773dc691383dbee028fd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185946"
---
# <a name="mdschemakpis-rowset"></a>MDSCHEMA_KPIS 행 집합
  데이터베이스 내의 KPI(핵심 성과 지표)를 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `MDSCHEMA_KPIS` 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||원본 데이터베이스입니다.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||지원되지 않습니다.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||KPI의 부모 큐브입니다.|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`||KPI에 대해 연결된 측정값 그룹입니다.<br /><br /> 이 열을 사용하여 KPI의 차원을 확인할 수 있습니다. 경우 "**\<NULL >**", KPI에서 모든 측정값 그룹 차원이 결정 됩니다.<br /><br /> 기본값은 "**\<NULL >**"입니다.|  
|`KPI_NAME`|`DBTYPE_WSTR`||KPI의 이름입니다.|  
|`KPI_CAPTION`|`DBTYPE_WSTR`||KPI에 연결된 레이블 또는 캡션으로, 주로 표시 목적으로 사용됩니다. 캡션이 없는 경우 `KPI_NAME`이 반환됩니다.|  
|`KPI_DESCRIPTION`|`DBTYPE_WSTR`||사람이 읽을 수 있는 KPI 설명입니다.|  
|`KPI_DISPLAY_FOLDER`|`DBTYPE_WSTR`||클라이언트 응용 프로그램이 멤버를 표시하기 위해 사용하는 표시 폴더의 경로를 식별하는 문자열입니다. 폴더 수준 구분 기호는 클라이언트 응용 프로그램에서 정의합니다. 도구 및에서 제공 하는 클라이언트에 대 한 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], 백슬래시 (\\)가 수준 구분 기호입니다. 여러 표시 폴더를 제공 하려면 세미콜론 (;)를 사용 하 여 폴더를 구분 합니다.|  
|`KPI_VALUE`|`DBTYPE_WSTR`||KPI 값의 측정값 차원에 포함된 멤버의 고유 이름입니다.|  
|`KPI_GOAL`|`DBTYPE_WSTR`||KPI 목표의 측정값 차원에 포함된 멤버의 고유 이름입니다.<br /><br /> 정의된 목표가 없으면 `NULL`을 반환합니다.|  
|`KPI_STATUS`|`DBTYPE_WSTR`||KPI 상태의 측정값 차원에 포함된 멤버의 고유 이름입니다.<br /><br /> 정의된 상태가 없으면 `NULL`을 반환합니다.|  
|`KPI_TREND`|`DBTYPE_WSTR`||KPI 추세의 측정값 차원에 포함된 멤버의 고유 이름입니다.<br /><br /> 정의된 추세가 없으면 `NULL`을 반환합니다.|  
|`KPI_STATUS_GRAPHIC`|`DBTYPE_WSTR`||KPI의 기본 그래픽 표현입니다.|  
|`KPI_TREND_GRAPHIC`|`DBTYPE_WSTR`||KPI의 기본 그래픽 표현입니다.|  
|`KPI_WEIGHT`|`DBTYPE_WSTR`||KPI 가중치의 측정값 차원에 포함된 멤버의 고유 이름입니다.|  
|`KPI_CURRENT_TIME_MEMBER`|`DBTYPE_WSTR`||KPI의 임시 컨텍스트를 정의하는 시간 차원에 포함된 멤버의 고유 이름입니다.<br /><br /> 정의된 시간 멤버가 없으면 `NULL`을 반환합니다.|  
|`KPI_PARENT_KPI_NAME`|`DBTYPE_WSTR`||부모 KPI의 이름입니다.|  
|`SCOPE`|`DBTYPE_I4`||KPI의 범위입니다. KPI는 세션 KPI 또는 전역 KPI일 수 있습니다.<br /><br /> 이 열 값은 다음 중 하나일 수 있습니다.<br /><br /> -MDKPI_SCOPE_GLOBAL = 1<br />-MDKPI_SCOPE_SESSION = 2|  
|`ANNOTATIONS`|`DBTYPE_WSTR`||(선택 사항) XML 형식의 메모 집합입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 `MDSCHEMA_KPIS` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`CUBE_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`KPI_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|다음 유효 값 중 하나가 포함된 비트맵입니다(선택 사항).<br /><br /> -   `1` 큐브<br />-   `2` 차원<br /><br /> 기본 제한 값은 `1`입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [OLAP용 OLE DB 스키마 행 집합](ole-db-for-olap-schema-rowsets.md)  
  
  