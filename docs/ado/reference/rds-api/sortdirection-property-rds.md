---
title: SortDirection 속성 (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SortDirection property [RDS]
ms.assetid: 1d9d8715-e4ad-4ff3-bf7f-f1dc0532d8c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 28f0e247c29673fe4dfec507794ad8977b51fcc1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67963412"
---
# <a name="sortdirection-property-rds"></a>SortDirection 속성(RDS)
정렬 순서가 오름차순 인지 또는 내림차순 인지를 나타냅니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.SortDirection = value  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 RDS를 나타내는 개체 변수입니다 [. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
 *값*  
 **True**로 설정 된 경우 정렬 방향이 오름차순 임을 나타내는 **부울** 값입니다. **False** 는 내림차순을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 [Sortcolumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md), **SortDirection**, [filtervalue](../../../ado/reference/rds-api/filtervalue-property-rds.md), [filtervalue](../../../ado/reference/rds-api/filtercriterion-property-rds.md)및 [filtervalue](../../../ado/reference/rds-api/filtercolumn-property-rds.md) 속성은 클라이언트 쪽 캐시에 정렬 및 필터링 기능을 제공 합니다. 정렬 기능은 한 열의 값을 사용 하 여 레코드를 정렬 합니다. 필터링 기능은 찾기 조건에 따라 레코드의 하위 집합을 표시 하는 반면 전체 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 은 캐시에 유지 됩니다. [Reset](../../../ado/reference/rds-api/reset-method-rds.md) 메서드는 조건을 실행 하 고 현재 **레코드 집합** 을 업데이트할 수 있는 **레코드 집합**으로 바꿉니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [FilterColumn, Filtercolumn, Filtercolumn, SortColumn 및 SortDirection 속성 및 Reset 메서드 예제 (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Sort 속성](../../../ado/reference/ado-api/sort-property.md)   
 [SortColumn 속성(RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)


