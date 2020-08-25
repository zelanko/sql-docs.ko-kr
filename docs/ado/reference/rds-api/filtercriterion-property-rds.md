---
description: FilterCriterion 속성(RDS)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1b13b3f3dcdaa2bdd45dabedd5310dc4cdd3db86
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768222"
---
# <a name="filtercriterion-property-rds"></a>FilterCriterion 속성(RDS)
필터 값에 사용할 평가 연산자를 나타냅니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.FilterCriterion = String  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 RDS를 나타내는 개체 변수입니다 [. DataControl](./datacontrol-object-rds.md) 개체입니다.  
  
 *String*  
 레코드에 대 한 [Filtervalue](./filtervalue-property-rds.md) 의 평가 연산자를 지정 하는 **문자열** 값입니다. 는 다음 중 하나일 수 있습니다. <, \<=, > , >=, = 또는 <>.  
  
## <a name="remarks"></a>설명  
 [Sortcolumn](./sortcolumn-property-rds.md), [SortDirection](./sortdirection-property-rds.md), [filtervalue](./filtervalue-property-rds.md), **filtervalue**및 [filtervalue](./filtercolumn-property-rds.md) 속성은 클라이언트 쪽 캐시에 정렬 및 필터링 기능을 제공 합니다. 정렬 기능은 한 열의 값으로 레코드를 정렬 합니다. 필터링 기능은 찾기 조건에 따라 레코드의 하위 집합을 표시 하는 반면 전체 [레코드 집합](../ado-api/recordset-object-ado.md) 은 캐시에 유지 됩니다. [Reset](./reset-method-rds.md) 메서드는 조건을 실행 하 고 현재 **레코드 집합** 을 업데이트할 수 있는 **레코드 집합**으로 바꿉니다.  
  
 "! =" 연산자는 **Filtercriterion**에 사용할 수 없습니다. 대신 "<>"을 사용 합니다.  
  
 Filter 및 sort 속성이 모두 설정 되 고 **Reset** 메서드를 호출 하면 행 집합이 먼저 필터링 된 다음 정렬 됩니다. 오름차순 정렬의 경우 null 값이 맨 위에 있습니다. 내림차순 정렬의 경우 null 값이 아래쪽에 있습니다 (오름차순은 기본 동작 임).  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [FilterColumn, Filtercolumn, Filtercolumn, SortColumn 및 SortDirection 속성 및 Reset 메서드 예제 (VBScript)](./filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [FilterColumn 속성 (RDS)](./filtercolumn-property-rds.md)   
 [FilterValue 속성 (RDS)](./filtervalue-property-rds.md)   
 [SortColumn 속성 (RDS)](./sortcolumn-property-rds.md)   
 [SortDirection 속성(RDS)](./sortdirection-property-rds.md)