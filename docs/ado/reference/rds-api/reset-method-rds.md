---
title: Reset 메서드 (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Reset method [ADO]
ms.assetid: 3957197a-f543-4d6b-9e11-67a77c2063b7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7fc769436a919a4d522fb48699c6fc6faa0d6e5c
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600053"
---
# <a name="reset-method-rds"></a>Reset 메서드(RDS)
클라이언트 쪽에서 정렬 또는 필터 실행 **레코드 집합** 지정 된 정렬 및 필터링 할 속성을 기반으로 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.Reset(value)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 나타내는 개체 변수는 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
 *value*  
 선택 사항입니다. A **부울** 값이 **True** "필터링된" 현재 행 집합에 필터를 적용 하려는 경우 (기본값). **False** 필터링 할 원래 행 집합에서 제거 하는 모든 이전 필터 옵션을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md)를 [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md)를 [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)를 [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md), 및 [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)정렬 및 필터링 기능 클라이언트 쪽 캐시에서 속성을 제공 합니다. 정렬 기능을 하나의 열 값으로 레코드를 정렬합니다. 필터링 기능을 표시 하는 동안 전체 찾기 조건에 따라 레코드 하위 집합만 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 캐시에 유지 됩니다. 합니다 **재설정** 메서드는 조건을 실행 하 고 현재 교체 **레코드 집합** 업데이트할 수 있는 사용 하 여 **레코드 집합**합니다.  
  
 전송 되지 않은 원래 데이터에 대 한 변경 내용이 있는지 여부를 **재설정** 메서드가 실패 합니다. 먼저 사용 하 여는 [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) 읽기/쓰기에서 변경 내용을 저장 하는 방법 **레코드 집합**를 사용 하 여를 **재설정** 메서드를 정렬 하거나 레코드를 필터링 합니다.  
  
 필터가 둘 이상인 행에서 수행 하려는 경우 사용할 수는 선택 사항 *부울* 인수에는 **재설정** 메서드. 다음 예제에서는이 작업을 수행 하는 방법을 보여 줍니다.  
  
```  
ADC.SQL = "Select au_lname from authors"  
ADC.Refresh    ' Get the new rowset.  
  
ADC.FilterColumn = "au_lname"  
ADC.FilterCriterion = "<"  
ADC.FilterValue = "'M'"  
ADC.Reset         ' Rowset now has all Last Names < "M".  
  
ADC.FilterCriterion = ">"  
ADC.FilterValue = "'F'"  
' Passing True is not necessary, because it is the   
' default filter on the current "filtered" rowset.  
ADC.Reset(TRUE)     ' Rowset now has all Last   
                    ' Names < "M" and > "F".  
  
ADC.FilterCriterion = ">"  
ADC.FilterValue = "'T'"  
' Filter on the original rowset, throwing out the  
' previous filter options.  
ADC.Reset(FALSE)   ' Rowset now has all Last Names > "T".  
```  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn 및 SortDirection 속성 및 Reset 메서드 예제 (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [SubmitChanges 메서드(RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)



