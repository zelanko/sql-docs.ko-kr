---
title: FilterCriterion 속성 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FilterCriterion property [RDS]
ms.assetid: 24eb03ba-ccfd-4353-b6af-03586b2da6fd
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: adc1d9d22b94ab3b6e03bddf37fa6058f4ccaca3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="filtercriterion-property-rds"></a>FilterCriterion 속성 (RDS)
필터 값에 사용 하는 계산 연산자를 나타냅니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.FilterCriterion = String  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 개체 변수를 나타내는 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
 *문자열*  
 A **문자열** 의 계산 연산자를 지정 하는 값은 [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md) 레코드에 있습니다. 다음 중 하나를 사용할 수 있습니다: <, \<=, >, > =, =, 또는 <> 합니다.  
  
## <a name="remarks"></a>주의  
 [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md), [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md), **FilterCriterion**, 및 [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)속성 정렬 및 필터링 기능에서 클라이언트 쪽 캐시를 제공 합니다. 특정 열의 값으로 레코드의 순서 정렬 기능입니다. 전체 동안 찾기 조건에 따라 레코드의 하위 집합을 표시 하는 필터링 기능은 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 캐시에 유지 됩니다. [재설정](../../../ado/reference/rds-api/reset-method-rds.md) 메서드는 조건을 실행 하 고 현재 교체 **레코드 집합** 와 업데이트할 수 있는 **레코드 집합**합니다.  
  
 "! =" 연산자에 대해 올바르지 않습니다. **FilterCriterion**대신 "<>"를 사용 합니다.  
  
 필터 및 정렬 속성이 설정 되 고 호출 하는 경우는 **재설정** 행 집합은 먼저 필터링 된 메서드와 다음 정렬 됩니다. 오름차순 정렬, null 값이 위쪽; 맨 아래에 null 값이 정렬 (오름차순 항목은 기본 동작).  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목:  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn, 및 SortDirection 속성 및 Reset 메서드 예제 (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [FilterColumn 속성 (RDS)](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [FilterValue 속성 (RDS)](../../../ado/reference/rds-api/filtervalue-property-rds.md)   
 [SortColumn 속성 (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection 속성(RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)


