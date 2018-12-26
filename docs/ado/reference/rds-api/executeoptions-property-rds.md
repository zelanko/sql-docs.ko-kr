---
title: ExecuteOptions 속성 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ExecuteOptions property [ADO], VBScript example
ms.assetid: 62a4fd88-afc3-4f1f-b978-40710a30c4e9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ac7ee6c1f996294c1f8aa353719deb11d698e47
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51603323"
---
# <a name="executeoptions-property-rds"></a>ExecuteOptions 속성(RDS)
비동기 실행 사용 되는지 여부를 나타냅니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 다음 값 중 하나를 반환 합니다.  
  
|상수|설명|  
|--------------|-----------------|  
|**adcExecSync**|다음 새로 고침을 실행 합니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 동기적으로 합니다.|  
|**adcExecAsync**|기본. 다음 새로 고침을 실행 합니다 **레코드 집합** 비동기적으로 합니다.|  
  
> [!NOTE]
>  이러한 상수를 사용 하는 각 실행 파일에 대 한 선언을 제공 해야 합니다. 잘라내기 및 Adcvbs.inc, RDS 라이브러리에 대 한 기본 설치 폴더에 있는 파일에서 원하는 상수 선언을 붙여넣기 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
 경우 **ExecuteOptions** 로 설정 된 **adcExecAsync**,이 다음을 비동기적으로 실행 한 다음 **새로 고침** 호출 합니다 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 **레코드 집합**합니다.  
  
 호출 하려고 하면 [재설정](../../../ado/reference/rds-api/reset-method-rds.md), [새로 고침](../../../ado/reference/rds-api/refresh-method-rds.md)를 [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)를 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md), 또는 [레코드 집합](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) 변경 될 수 있는 다른 비동기 작업을 하는 동안는 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 **레코드 집합** 실행에서 오류가 발생 합니다.  
  
 비동기 작업 중에 오류가 발생 하는 경우는 **rds. DataControl** 개체의 [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) 의 값이 변경 **adcReadyStateLoaded** 하 **adcReadyStateComplete**, 및  **레코드 집합** 속성 값은 그대로 *Nothing*합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목  
 [ExecuteOptions 및 FetchOptions 속성 예제 (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel 메서드(RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


