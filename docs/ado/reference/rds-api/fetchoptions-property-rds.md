---
title: FetchOptions 속성 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FetchOptions property [ADO]
ms.assetid: 7b2e254a-9354-4541-bc98-bb185276388f
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b73931acd678871f05e5aa4022153ded86a830e4
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35288136"
---
# <a name="fetchoptions-property-rds"></a>FetchOptions 속성 (RDS)
비동기 인출의 유형을 나타냅니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="setting-and-return-values"></a>설정 및 반환 값  
 설정 하거나 다음 값 중 하나를 반환 합니다.  
  
|상수|Description|  
|--------------|-----------------|  
|**adcFetchUpFront**|모든 레코드는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 응용 프로그램에 제어 기능이 회복 인출 합니다. 전체 **레코드 집합** 함께 어떤 작업을 응용 프로그램이 허용 되기 전에 인출 됩니다.|  
|**adcFetchBackground**|컨트롤은 레코드의 첫 번째 일괄 처리를 가져온 되는 즉시 응용 프로그램에 반환할 수 있습니다. 후속 읽기는 **레코드 집합** 첫 번째 일괄 처리에서 반입 되지 않은 레코드에 액세스 하려고는 검색된 된 레코드는 실제로 인출 될 때까지 지연 됩니다, 이때 컨트롤은 응용 프로그램에 반환 합니다.|  
|**adcFetchAsync**|기본. 제어는 레코드는 백그라운드에서 가져오므로 하는 동안 응용 프로그램에 즉시 반환 됩니다. 아직 페치 하지 않은 레코드를 읽는 응용 프로그램이 만들려고 할 경우, 검색된 된 레코드에 가장 가까운 레코드 읽 및 제어는 즉시 결과 반환 하는지 여부를 나타내는의 현재 끝에서 **레코드 집합** 에 도달 했습니다. 에 대 한 호출 예를 들어 [MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) 더 많은 레코드를 채우는 계속 하는 경우에 현재 레코드 위치 실제로 인출 된 마지막 레코드로 이동는 **레코드 집합**합니다.|  
  
> [!NOTE]
>  이러한 상수를 사용 하는 각 클라이언트 실행 파일에 대 한 선언을 제공 해야 합니다. 잘라내기 및 RDS 라이브러리에 대 한 기본 설치 폴더에 있는 파일, Adcvbs.inc에서에서 원하는 상수 선언을 붙여넣기 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
 웹 응용 프로그램에서은 일반적으로 사용 하려는 **adcFetchAsync** (기본값), 더 나은 성능을 제공 하기 때문에 있습니다. 컴파일된 클라이언트 응용 프로그램에서은 일반적으로 사용 하려는 **adcFetchBackground**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목  
 [ExecuteOptions 및 FetchOptions 속성 예 (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel 메서드(RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


