---
description: Server 속성(RDS)
title: 서버 속성 (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- RDS::IBindMgr21::Server
helpviewer_keywords:
- Server property [RDS]
ms.assetid: d2727ce7-da9f-4271-ae3c-9334ef477c14
author: rothja
ms.author: jroth
ms.openlocfilehash: 0c7d2c095c9f10e95df54849ce729ffdcbbca135
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767522"
---
# <a name="server-property-rds"></a>Server 속성(RDS)
인터넷 정보 서비스 (IIS) 이름 및 통신 프로토콜을 나타냅니다.  
  
 RDS의 개체 태그에서 디자인 타임에 **서버** 속성을 설정할 수 있습니다[. DataControl](./datacontrol-object-rds.md) 개체 또는 런타임 시 스크립팅 코드에서  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
 **HTTP**  
  
 디자인 타임 구문  
  
```  
  
<PARAM NAME="Server" VALUE="http:  
//awebsrvr:port  
">  
  
```  
  
 런타임 구문  
  
```  
  
DataControl  
.Server="https://  
awebsrvr:port  
"  
  
```  
  
 **HTTPS**  
  
 디자인 타임 구문  
  
```  
  
<PARAM NAME="Server" VALUE="https://awebsrvr:port">  
```  
  
 런타임 구문  
  
```  
  
DataControl.Server="https://awebsrvr:port"  
```  
  
 **DCOM**  
  
 디자인 타임 구문  
  
```  
  
<PARAM NAME="Server" VALUE="  
computername  
">  
  
```  
  
 런타임 구문  
  
```  
  
DataControl.Server="computername"  
```  
  
 **In-Process**  
  
 디자인 타임 구문  
  
```  
  
<PARAM NAME="Server" VALUE="">  
  
```  
  
 런타임 구문  
  
```  
  
DataControl.Server=""  
```  
  
## <a name="parameters"></a>매개 변수  
 *awebsrvr*또는 *computername*  
 서버가 원격 컴퓨터에 있는 경우 인터넷 또는 인트라넷 경로 또는 컴퓨터 이름을 포함 하는 **문자열** 값입니다. 또는 서버가 로컬 컴퓨터에 있는 경우 빈 문자열입니다.  
  
 *port*  
 선택 사항입니다. IIS를 실행 하는 서버에 연결 하는 데 사용 되는 포트입니다. 포트 번호는 Internet Explorer에서 설정 됩니다 ( **보기** 메뉴에서 **옵션**을 클릭 한 다음 **연결** 탭 선택) 또는 IIS에서 설정 합니다.  
  
 *DataControl*  
 RDS를 나타내는 개체 변수입니다 **. DataControl** 개체입니다.  
  
## <a name="remarks"></a>설명  
 서버는 RDS가 있는 위치입니다 **. DataControl** 요청 (즉, 쿼리 또는 업데이트)이 처리 됩니다. 기본적으로 모든 요청은 [RDSServer](./datafactory-object-rdsserver.md) 개체, Msdfmap에 의해 처리 됩니다. [ ](../../guide/remote-data-service/datafactory-customization.md) 지정 된 서버에서 처리기 구성 요소 및 [MSDFMAP.INI](../../guide/remote-data-service/understanding-the-customization-file.md) 파일 서버를 변경 하 여 이전 및 새 **MSDFMAP.INI** 파일의 설정을 조정 하는 경우를 고려 합니다. 비 호환성으로 인해 한 서버에서 성공한 요청이 다른 서버에서 실패할 수 있습니다. 서버 속성이 빈 문자열 ""로 설정 된 경우 이러한 개체는 로컬 컴퓨터에서 사용 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [서버 속성 예제 (VBScript)](./server-property-example-vbscript.md)   
 [Connect 속성 (RDS)](./connect-property-rds.md)   
 [SQL 속성](./sql-property.md)   
 [SubmitChanges 메서드(RDS)](./submitchanges-method-rds.md)