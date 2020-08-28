---
description: ExecuteOptions 속성(RDS)
title: ExecuteOptions 속성 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ExecuteOptions property [ADO], VBScript example
ms.assetid: 62a4fd88-afc3-4f1f-b978-40710a30c4e9
author: rothja
ms.author: jroth
ms.openlocfilehash: c363333e7e88fa0bedbb8cddc126d7ad62f0e2d3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982254"
---
# <a name="executeoptions-property-rds"></a>ExecuteOptions 속성(RDS)
비동기 실행을 사용 하는지 여부를 나타냅니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 다음 값 중 하나를 설정 하거나 반환 합니다.  
  
|상수|설명|  
|--------------|-----------------|  
|**adcExecSync**|[레코드 집합](../ado-api/recordset-object-ado.md) 의 다음 새로 고침을 동기적으로 실행 합니다.|  
|**adcExecAsync**|기본값 **레코드 집합** 의 다음 새로 고침을 비동기적으로 실행 합니다.|  
  
> [!NOTE]
>  이러한 상수를 사용 하는 각 실행 파일은 이러한 상수에 대 한 선언을 제공 해야 합니다. RDS 라이브러리의 기본 설치 폴더에 있는 Adcvbs. i n c. i n t. i n t.  
  
## <a name="remarks"></a>설명  
 **Executeoptions** 를 **Adcexecasync**로 설정 하면 RDS에서 다음 **새로 고침** 호출을 비동기적으로 실행 합니다 [. DataControl](./datacontrol-object-rds.md) 개체의 **레코드 집합**입니다.  
  
 [다시 설정](./reset-method-rds.md), [새로 고침](./refresh-method-rds.md), [SubmitChanges](./submitchanges-method-rds.md), [CancelUpdate](../ado-api/cancelupdate-method-ado.md)또는 [레코드 집합](./recordset-sourcerecordset-properties-rds.md) 을 호출 하려고 시도 하는 경우에는 다른 비동기 작업에서 RDS를 변경할 수 있습니다 [. DataControl](./datacontrol-object-rds.md) 개체의 **레코드 집합이** 실행 중 이므로 오류가 발생 합니다.  
  
 비동기 작업 중에 오류가 발생 하는 경우 **RDS. DataControl** 개체의 [ReadyState](./readystate-property-rds.md) 값이 **Adcreadystateloaded** 에서 **adcReadyStateComplete**로 변경 되 고 **레코드 집합** 속성 값은 *아무 것도*유지 되지 않습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [ExecuteOptions 및 FetchOptions 속성 예제 (VBScript)](./executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel 메서드(RDS)](./cancel-method-rds.md)