---
description: Reset 메서드(RDS)
title: Reset 메서드 (RDS) | Microsoft Docs
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: fcebd112b389fe98b69b25852ef0504e88890261
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724262"
---
# <a name="reset-method-rds"></a>Reset 메서드(RDS)
지정 된 정렬 및 필터 속성을 기반으로 클라이언트 쪽 **레코드 집합** 에서 정렬 또는 필터를 실행 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](/dotnet/framework/wcf/)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.Reset(value)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 RDS를 나타내는 개체 변수입니다 [. DataControl](./datacontrol-object-rds.md) 개체입니다.  
  
 *value*  
 선택 사항입니다. 현재 "필터링 된" 행 집합을 필터링 하려는 경우 **부울** **값 (기본값)입니다.** **False** 는 원래 행 집합을 필터링 하 고 이전 필터 옵션을 제거 함을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 [Sortcolumn](./sortcolumn-property-rds.md), [SortDirection](./sortdirection-property-rds.md), [filtervalue](./filtervalue-property-rds.md), [filtervalue](./filtercriterion-property-rds.md)및 [filtervalue](./filtercolumn-property-rds.md) 속성은 클라이언트 쪽 캐시에 정렬 및 필터링 기능을 제공 합니다. 정렬 기능은 한 열의 값으로 레코드를 정렬 합니다. 필터링 기능은 검색 조건에 따라 레코드의 하위 집합을 표시 하는 반면 전체 [레코드 집합](../ado-api/recordset-object-ado.md) 은 캐시에 유지 됩니다. **Reset** 메서드는 조건을 실행 하 고 현재 **레코드 집합** 을 업데이트할 수 있는 **레코드 집합**으로 바꿉니다.  
  
 전송 되지 않은 원본 데이터에 변경 내용이 있으면 **Reset** 메서드가 실패 합니다. 먼저 [SubmitChanges](./submitchanges-method-rds.md) 메서드를 사용 하 여 읽기/쓰기 **레코드 집합**의 변경 내용을 저장 한 다음 **Reset** 메서드를 사용 하 여 레코드를 정렬 하거나 필터링 합니다.  
  
 행 집합에서 필터를 두 개 이상 수행 하려는 경우에는 선택적 *부울* 인수를 **Reset** 메서드와 함께 사용할 수 있습니다. 다음 예제에 이 작업을 수행하는 방법이 나와 있습니다.  
  
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
 [DataControl 개체(RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [FilterColumn, Filtercolumn, Filtercolumn, SortColumn 및 SortDirection 속성 및 Reset 메서드 예제 (VBScript)](./filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [SubmitChanges 메서드(RDS)](./submitchanges-method-rds.md)