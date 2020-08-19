---
description: FetchOptions 속성(RDS)
title: FetchOptions 속성 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FetchOptions property [ADO]
ms.assetid: 7b2e254a-9354-4541-bc98-bb185276388f
author: rothja
ms.author: jroth
ms.openlocfilehash: 2d00dd737f6b775d9d46bfb6af96a5ce76aa3a8e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439025"
---
# <a name="fetchoptions-property-rds"></a>FetchOptions 속성(RDS)
비동기 인출의 유형을 나타냅니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="setting-and-return-values"></a>값 설정 및 반환  
 다음 값 중 하나를 설정 하거나 반환 합니다.  
  
|상수|설명|  
|--------------|-----------------|  
|**adcFetchUpFront**|응용 프로그램에 컨트롤을 반환 하기 전에 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 의 모든 레코드를 인출 합니다. 응용 프로그램에서 모든 작업을 수행할 수 있도록 하기 전에 전체 **레코드 집합** 을 인출 합니다.|  
|**adcFetchBackground**|첫 번째 일괄 처리 레코드가 인출 되는 즉시 제어가 응용 프로그램으로 돌아갈 수 있습니다. 첫 번째 일괄 처리에서 인출 되지 않은 레코드에 대 한 액세스를 시도 하는 **레코드 집합** 의 후속 읽기는 검색 된 레코드가 실제로 인출 될 때까지 지연 되며,이 시점에서 컨트롤이 응용 프로그램으로 반환 됩니다.|  
|**adcFetchAsync**|기본값 백그라운드에서 레코드를 인출 하는 동안 컨트롤은 응용 프로그램에 즉시 반환 됩니다. 응용 프로그램이 아직 인출 되지 않은 레코드를 읽으려고 하는 경우 검색 된 레코드에 가장 가까운 레코드를 읽고,이 레코드를 즉시 반환 하 여 **레코드 집합** 의 현재 끝에 도달 했음을 나타냅니다. 예를 들어, [MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) 를 호출 하면 더 많은 레코드에서 레코드 **집합**을 계속 채울 수 있는 경우에도 현재 레코드 위치가 실제로 인출 된 마지막 레코드로 이동 합니다.|  
  
> [!NOTE]
>  이러한 상수를 사용 하는 각 클라이언트 쪽 실행 파일은 이러한 상수에 대 한 선언을 제공 해야 합니다. RDS 라이브러리의 기본 설치 폴더에 있는 Adcvbs. inc. 파일에서 원하는 상수 선언을 잘라내어 붙여 넣을 수 있습니다.  
  
## <a name="remarks"></a>설명  
 웹 응용 프로그램에서는 일반적으로 더 나은 성능을 제공 하므로 **Adcfetchasync** (기본값)를 사용 하는 것이 좋습니다. 컴파일된 클라이언트 응용 프로그램에서는 일반적으로 **Adcfetchbackground**를 사용 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [ExecuteOptions 및 FetchOptions 속성 예제 (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel 메서드(RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


