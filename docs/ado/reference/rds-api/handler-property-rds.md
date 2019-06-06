---
title: Handler 속성 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Handler property [ADO]
ms.assetid: fdc34362-6d47-4727-b171-8d033159408e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6b538767f62a3d80b9cf2cd9b558f14c5de91549
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712463"
---
# <a name="handler-property-rds"></a>Handler 속성(RDS)
기능을 확장 하는 서버 쪽 사용자 지정 프로그램 (처리기)의 이름을 나타내는 합니다 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), 및에서 사용 하는 매개 변수를 *처리기*합니다.  
  
 **적용 대상:** [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.Handler = String  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 나타내는 개체 변수는 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
 *String*  
 A **문자열** 쉼표로 구분 된 모든 처리기 및 모든 매개 변수의 이름을 포함 하는 값 (예를 들어 `"handlerName,parm1,parm2,...,parm` *N*`"`).  
  
## <a name="remarks"></a>Remarks  
 이 속성은 지원 [사용자 지정](../../../ado/guide/remote-data-service/datafactory-customization.md)를 설정 해야 하는 기능을 합니다 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**합니다.  
  
 처리기 및 해당 매개 변수의 이름이 있는 경우 쉼표로 구분 됩니다 (","). 있는 경우 세미콜론으로 예기치 않은 동작이 발생 합니다 (";") 내의 모든 위치에 나타납니다 *문자열*합니다. 지원 한다면 사용자 고유의 처리기를 작성할 수 있습니다 합니다 **예기치 않은** 인터페이스입니다.  
  
 기본 처리기의 이름은 **MSDFMAP 합니다. 처리기**, 기본 매개 변수는 명명 된 사용자 지정 파일 및 **MSDFMAP 합니다. INI**합니다. 이 속성을 사용 하 여 서버 관리자가 만든 대체 사용자 지정 파일을 호출 합니다.  
  
 설정에 대 한 대체는 **처리기** 속성 처리기 및 매개 변수를 지정 하는 것은 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성 즉, "**처리기 =** _handlerName, parameter1, parameter2;..._ ".  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목  
 [Handler 속성 예제 (VB)](../../../ado/reference/rds-api/handler-property-example-vb.md)   
 [DataFactory 사용자 지정](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [DataFactory 개체(RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


