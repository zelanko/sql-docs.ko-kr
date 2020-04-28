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
ms.openlocfilehash: a7423879b8263d87575d913c4863143faf3573e5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67964001"
---
# <a name="handler-property-rds"></a>Handler 속성(RDS)
DataFactory의 기능과 *처리기*에서 사용 하는 매개 변수를 확장 하는 서버 쪽 사용자 지정 프로그램 (처리기)의 이름을 나타냅니다 [RDSServer.](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
 **적용 대상:** [DATACONTROL 개체 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.Handler = String  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 RDS를 나타내는 개체 변수입니다 [. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
 *String*  
 처리기의 이름과 모든 매개 변수를 쉼표로 구분 하 여 포함 하는 **문자열** 값입니다 (예: `"handlerName,parm1,parm2,...,parm` *N*`"`).  
  
## <a name="remarks"></a>설명  
 이 속성은 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**로 설정 해야 하는 기능인 [사용자 지정](../../../ado/guide/remote-data-service/datafactory-customization.md)을 지원 합니다.  
  
 처리기의 이름과 해당 매개 변수 (있는 경우)는 쉼표 (",")로 구분 됩니다. *문자열*내의 아무 곳에 나 세미콜론 (";")이 나타나면 예측할 수 없는 동작이 발생 합니다. **IDataFactoryHandler** 인터페이스를 지 원하는 경우 고유한 처리기를 작성할 수 있습니다.  
  
 기본 처리기의 이름은 **Msdfmap입니다. 처리기**및 기본 매개 변수는 Msdfmap 이라는 사용자 지정 파일입니다 **. INI**. 서버 관리자가 만든 대체 사용자 지정 파일을 호출 하려면이 속성을 사용 합니다.  
  
 **Handler** 속성을 설정 하는 대신 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성에 처리기와 매개 변수를 지정할 수 있습니다. 즉, "**Handler =**_handlerName, parameter1, parameter2,...;_"입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [Handler 속성 예제 (VB)](../../../ado/reference/rds-api/handler-property-example-vb.md)   
 [DataFactory 사용자 지정](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [DataFactory 개체(RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


