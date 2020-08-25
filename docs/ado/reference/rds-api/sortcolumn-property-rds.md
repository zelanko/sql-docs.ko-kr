---
description: SortColumn 속성(RDS)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1cb2c1ba329537acd5b9ffe2008f334b34a45c2f
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767482"
---
# <a name="sortcolumn-property-rds"></a>SortColumn 속성(RDS)
레코드를 정렬 하는 기준이 되는 열을 나타냅니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.SortColumn = String  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 RDS를 나타내는 개체 변수입니다 [. DataControl](./datacontrol-object-rds.md) 개체입니다.  
  
 *String*  
 레코드를 정렬 하는 기준이 되는 열의 이름 또는 별칭을 나타내는 **문자열** 값입니다.  
  
## <a name="remarks"></a>설명  
 **Sortcolumn**, [SortDirection](./sortdirection-property-rds.md), [filtervalue](./filtervalue-property-rds.md), [filtervalue](./filtercriterion-property-rds.md)및 [filtervalue](./filtercolumn-property-rds.md) 속성은 클라이언트 쪽 캐시에 정렬 및 필터링 기능을 제공 합니다. 정렬 기능은 한 열의 값으로 레코드를 정렬 합니다. 필터링 기능은 찾기 조건에 따라 레코드의 하위 집합을 표시 하는 반면 전체 [레코드 집합](../ado-api/recordset-object-ado.md) 은 캐시에 유지 됩니다. [Reset](./reset-method-rds.md) 메서드는 조건을 실행 하 고 현재 **레코드 집합** 을 업데이트할 수 있는 **레코드 집합**으로 바꿉니다.  
  
 **레코드 집합**을 정렬 하려면 먼저 보류 중인 변경 내용을 저장 해야 합니다. RDS를 사용 하는 경우 ** SubmitChanges 메서드를 사용할**수 있습니다 [SubmitChanges](./submitchanges-method-rds.md) . 예를 들어, RDS 인 경우 ** DataControl** 은 이름이 ADC1 이며 코드는 `ADC1.SubmitChanges` 입니다. ADO **레코드 집합**을 사용 하는 경우 해당 [UpdateBatch](../ado-api/updatebatch-method.md) 메서드를 사용할 수 있습니다. [CreateRecordset](./createrecordset-method-rds.md) 메서드를 사용 하 여 만든 **레코드 집합** 개체의 경우 **UpdateBatch** 를 사용 하는 것이 좋습니다. 예를 들어 코드는 또는 일 수 있습니다 `myRS.UpdateBatch` `ADC1.Recordset.UpdateBatch` .  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [FilterColumn, Filtercolumn, Filtercolumn, SortColumn 및 SortDirection 속성 및 Reset 메서드 예제 (VBScript)](./filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Sort 속성](../ado-api/sort-property.md)   
 [SortDirection 속성(RDS)](./sortdirection-property-rds.md)