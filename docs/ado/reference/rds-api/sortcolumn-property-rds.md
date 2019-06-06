---
title: SortColumn 속성 (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SortColumn property [RDS]
ms.assetid: f6f80f67-f0fb-4e63-a5f5-8fdf312aac63
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 93b8bd226ca5b29af534c856e394c98b4466ec25
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697648"
---
# <a name="sortcolumn-property-rds"></a>SortColumn 속성(RDS)
레코드를 정렬 하려면 열을 나타냅니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.SortColumn = String  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 나타내는 개체 변수는 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
 *String*  
 A **문자열** 이름 또는 별칭 레코드를 정렬할 기준이 되는 열을 나타내는 값입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **SortColumn**를 [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md)를 [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)를 [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md), 및 [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)정렬 및 필터링 기능 클라이언트 쪽 캐시에서 속성을 제공 합니다. 정렬 기능을 하나의 열 값으로 레코드를 정렬합니다. 필터링 기능을 표시 하는 동안 전체 찾기 조건에 따라 레코드 하위 집합만 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 캐시에 유지 됩니다. 합니다 [재설정](../../../ado/reference/rds-api/reset-method-rds.md) 메서드는 조건을 실행 하 고 현재 교체 **레코드 집합** 업데이트할 수 있는 사용 하 여 **레코드 집합**합니다.  
  
 에 대해 정렬 하는 **레코드 집합**, 보류 중인 변경 내용을 먼저 저장 해야 합니다. 사용 중인 경우는 **rds. DataControl**를 사용할 수는 [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) 메서드. 예를 들어, 경우에 **rds. DataControl** 는 ADC1 라는 코드 것 `ADC1.SubmitChanges`입니다. ADO를 사용 하는 경우 **Recordset**를 사용할 수 있습니다 해당 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드. 사용 하 여 **UpdateBatch** 에 대 한 것이 좋지만 **레코드 집합** 사용 하 여 만든 개체를 [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md) 메서드. 예를 들어 코드 일 수 있습니다 `myRS.UpdateBatch` 또는 `ADC1.Recordset.UpdateBatch`합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn 및 SortDirection 속성 및 Reset 메서드 예제 (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Sort 속성](../../../ado/reference/ado-api/sort-property.md)   
 [SortDirection 속성(RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)





