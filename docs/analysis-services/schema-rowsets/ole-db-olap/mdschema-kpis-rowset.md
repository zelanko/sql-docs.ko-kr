---
title: "MDSCHEMA_KPIS 행 집합 | Microsoft Docs"
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
apiname: MDSCHEMA_KPIS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_KPIS rowset
ms.assetid: 40fb5112-6a90-4455-82b3-8b6322490222
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 273adea0694ae9b59b2a49f26d04165c3fe948d4
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="mdschemakpis-rowset"></a>MDSCHEMA_KPIS 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]데이터베이스 내에서 핵심 성과 지표 (Kpi)에 대해 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **MDSCHEMA_KPIS** 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|원본 데이터베이스입니다.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|지원되지 않습니다.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|KPI의 부모 큐브입니다.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|KPI에 대해 연결된 측정값 그룹입니다.<br /><br /> 이 열을 사용하여 KPI의 차원을 확인할 수 있습니다. 경우 "**\<NULL >**", KPI에서 모든 측정값 그룹 차원이 결정 됩니다.<br /><br /> 기본값은 "**\<NULL >**"입니다.|  
|**KPI_NAME**|**DBTYPE_WSTR**|KPI의 이름입니다.|  
|**KPI_CAPTION**|**DBTYPE_WSTR**|KPI에 연결된 레이블 또는 캡션으로, 주로 표시 목적으로 사용됩니다. 캡션이 없는 경우 **KPI_NAME** 반환 됩니다.|  
|**KPI_DESCRIPTION**|**DBTYPE_WSTR**|사람이 읽을 수 있는 KPI 설명입니다.|  
|**KPI_DISPLAY_FOLDER**|**DBTYPE_WSTR**|클라이언트 응용 프로그램이 멤버를 표시하기 위해 사용하는 표시 폴더의 경로를 식별하는 문자열입니다. 폴더 수준 구분 기호는 클라이언트 응용 프로그램에서 정의합니다. 도구 및에서 제공 하는 클라이언트에 대 한 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], 백슬래시 (\\)가 수준 구분 기호입니다. 여러 표시 폴더를 제공 하려면 세미콜론 (;)를 사용 하 여 폴더를 구분 합니다.|  
|**KPI_VALUE**|**DBTYPE_WSTR**|KPI 값의 측정값 차원에 포함된 멤버의 고유 이름입니다.|  
|**KPI_GOAL**|**DBTYPE_WSTR**|KPI 목표의 측정값 차원에 포함된 멤버의 고유 이름입니다.<br /><br /> 반환 **NULL** 정의 된 목표가 없으면 합니다.|  
|**KPI_STATUS**|**DBTYPE_WSTR**|KPI 상태의 측정값 차원에 포함된 멤버의 고유 이름입니다.<br /><br /> 반환 **NULL** 정의 된 상태가 없는 경우.|  
|**KPI_TREND**|**DBTYPE_WSTR**|KPI 추세의 측정값 차원에 포함된 멤버의 고유 이름입니다.<br /><br /> 반환 **NULL** 정의 된 추세가 없으면 합니다.|  
|**KPI_STATUS_GRAPHIC**|**DBTYPE_WSTR**|KPI의 기본 그래픽 표현입니다.|  
|**KPI_TREND_GRAPHIC**|**DBTYPE_WSTR**|KPI의 기본 그래픽 표현입니다.|  
|**KPI_WEIGHT**|**DBTYPE_WSTR**|KPI 가중치의 측정값 차원에 포함된 멤버의 고유 이름입니다.|  
|**KPI_CURRENT_TIME_MEMBER**|**DBTYPE_WSTR**|KPI의 임시 컨텍스트를 정의하는 시간 차원에 포함된 멤버의 고유 이름입니다.<br /><br /> 반환 **NULL** 정의 된 시간 멤버가 없으면 합니다.|  
|**KPI_PARENT_KPI_NAME**|**DBTYPE_WSTR**|부모 KPI의 이름입니다.|  
|**범위**|**DBTYPE_I4**|KPI의 범위입니다. KPI는 세션 KPI 또는 전역 KPI일 수 있습니다.<br /><br /> 이 열 값은 다음 중 하나일 수 있습니다.<br /><br /> MDKPI_SCOPE_GLOBAL=1<br /><br /> MDKPI_SCOPE_SESSION=2|  
|**주석**|**DBTYPE_WSTR**|(선택 사항) XML 형식의 메모 집합입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **MDSCHEMA_KPIS** 행 집합은 다음 표에 나열 된 열에 제한 될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**CUBE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**KPI_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(선택 사항) 기본 제한 값은 **1**합니다. 유효한 값 중 하나를 사용 하는 비트맵.<br /><br /> **1** 큐브<br /><br /> **2** 차원|  
  
## <a name="see-also"></a>관련 항목:  
 [OLAP용 OLE DB 스키마 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
