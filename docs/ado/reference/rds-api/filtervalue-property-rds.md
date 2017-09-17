---
title: "FilterValue 속성 (RDS) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- FilterValue property [ADO]
ms.assetid: 28f17186-b842-4cf9-b320-a9bb941c481b
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d5bc23370137719589a0642df9eca461043ba722
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="filtervalue-property-rds"></a>FilterValue 속성 (RDS)
레코드를 필터링 할 값을 나타냅니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.FilterValue = String  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 개체 변수를 나타내는 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
 *문자열*  
 A **문자열** 하는 레코드를 필터링 하는 데 사용할 데이터 값을 나타내는 값입니다 (예를 들어 `'Programmer'` 또는 `125`).  
  
## <a name="remarks"></a>주의  
 [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md), [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), **FilterValue**, [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md), 및 [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)속성 정렬 및 필터링 기능에서 클라이언트 쪽 캐시를 제공 합니다. 특정 열의 값으로 레코드의 순서 정렬 기능입니다. 전체 동안 찾기 조건에 따라 레코드의 하위 집합을 표시 하는 필터링 기능은 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 캐시에 유지 됩니다. [재설정](../../../ado/reference/rds-api/reset-method-rds.md) 메서드는 조건을 실행 하 고 현재 교체 **레코드 집합** 와 업데이트할 수 있는 **레코드 집합**합니다.  
  
 Null 값은 형식 불일치 오류가 생성 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목:  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn, 및 SortDirection 속성 및 Reset 메서드 예제 (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [FilterColumn 속성 (RDS)](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [FilterCriterion 속성 (RDS)](../../../ado/reference/rds-api/filtercriterion-property-rds.md)   
 [SortColumn 속성 (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection 속성(RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)























