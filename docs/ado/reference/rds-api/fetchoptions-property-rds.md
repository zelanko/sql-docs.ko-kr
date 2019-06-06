---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a85f6938ec0f97ff69eab1782c0a24b78a5a6e8b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712687"
---
# <a name="fetchoptions-property-rds"></a>FetchOptions 속성(RDS)
비동기 가져오기의 유형을 나타냅니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="setting-and-return-values"></a>설정 및 반환 값  
 설정 하거나 다음 값 중 하나를 반환 합니다.  
  
|상수|설명|  
|--------------|-----------------|  
|**adcFetchUpFront**|모든 레코드를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 컨트롤 응용 프로그램에 반환 되기 전에 페치됩니다. 전체 **레코드 집합** 무언가를 수행 하는 응용 프로그램 허용 하기 전에 페치됩니다.|  
|**adcFetchBackground**|컨트롤은 레코드의 첫 번째 일괄 처리를 가져온 즉시 응용 프로그램에 반환할 수 있습니다. 후속 읽기 작업은 **레코드 집합** 는 첫 번째 일괄 처리에서 반입 되지 않은 레코드에 액세스 하려고는 검색된 된 레코드는 실제로 인출 될 때까지 지연 됩니다, 이때 컨트롤 응용 프로그램에 반환 합니다.|  
|**adcFetchAsync**|기본. 컨트롤이는 백그라운드에서 레코드 인출 하는 동안 응용 프로그램에 즉시 반환 합니다. 응용 프로그램을 인출 아직 하지 않은 레코드를 읽을 하려고 읽을 검색된 된 레코드에 가장 가까운 레코드 및 컨트롤 즉시 반환 되며 나타내는 현재 끝 합니다 **레코드 집합** 에 도달 했습니다. 에 대 한 호출 예를 들어 [MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) 채우는 데 더 많은 레코드를 계속 하는 경우에 현재 레코드 위치 실제로 인출 된 마지막 레코드로 이동 합니다 **레코드 집합**합니다.|  
  
> [!NOTE]
>  이러한 상수를 사용 하는 각 클라이언트 쪽 실행 파일에 대 한 선언을 제공 해야 합니다. 잘라내기 및 Adcvbs.inc, RDS 라이브러리에 대 한 기본 설치 폴더에 있는 파일에서 원하는 상수 선언을 붙여넣기 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
 웹 응용 프로그램에서은 일반적으로 사용 하려는 **adcFetchAsync** (기본값), 더 나은 성능을 제공 하기 때문입니다. 컴파일된 클라이언트 응용 프로그램에 일반적으로 사용 하려는 **adcFetchBackground**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목  
 [ExecuteOptions 및 FetchOptions 속성 예제 (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel 메서드(RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


