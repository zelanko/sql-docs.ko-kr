---
title: FilterCriterion 속성 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FilterCriterion property [RDS]
ms.assetid: 24eb03ba-ccfd-4353-b6af-03586b2da6fd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 60f66b1ff2fa7ad7424342da6b92e7d44d0e6444
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712708"
---
# <a name="filtercriterion-property-rds"></a>FilterCriterion 속성(RDS)
필터 값에 사용할 계산 연산자를 나타냅니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.FilterCriterion = String  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 나타내는 개체 변수는 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
 *String*  
 A **문자열** 평가 운영자를 지정 하는 값을 [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md) 레코드입니다. 다음 중 하나일 수 있습니다: <, \<=, >, > =, =, 또는 <> 합니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md)를 [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md)를 [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)를 **FilterCriterion**, 및 [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)정렬 및 필터링 기능 클라이언트 쪽 캐시에서 속성을 제공 합니다. 정렬 기능을 하나의 열 값으로 레코드를 정렬합니다. 필터링 기능을 표시 하는 동안 전체 찾기 조건에 따라 레코드 하위 집합만 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 캐시에 유지 됩니다. 합니다 [재설정](../../../ado/reference/rds-api/reset-method-rds.md) 메서드는 조건을 실행 하 고 현재 교체 **레코드 집합** 업데이트할 수 있는 사용 하 여 **레코드 집합**합니다.  
  
 "! =" 연산자에 대해 올바르지 않습니다. **FilterCriterion**대신 "<>"를 사용 합니다.  
  
 필터 및 정렬 속성은 설정 하 고 호출 하는 **재설정** 행 집합은 먼저 필터링 된 메서드와 다음 정렬 됩니다. 오름차순 정렬, null 값이 맨; 맨 아래에 null 값은 정렬 (오름차순 것이 기본 동작).  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn 및 SortDirection 속성 및 Reset 메서드 예제 (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [FilterColumn 속성 (RDS)](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [FilterValue 속성 (RDS)](../../../ado/reference/rds-api/filtervalue-property-rds.md)   
 [SortColumn 속성 (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection 속성(RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)


