---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77ad00d9c21a7f7558f8f5cafc66464c1ffc54f7
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600183"
---
# <a name="server-property-rds"></a>Server 속성(RDS)
인터넷 정보 서비스 (IIS) 이름 및 통신 프로토콜을 나타냅니다.  
  
 설정할 수 있습니다 합니다 **Server** 의 OBJECT 태그에서 디자인 타임에 속성을[rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체 또는 런타임에 코드를 스크립팅 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
 **HTTP**  
  
 디자인 타임 구문  
  
```  
  
<PARAM NAME="Server" VALUE="http:  
//awebsrvr:port  
">  
  
```  
  
 실행 타임 구문  
  
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
  
 실행 타임 구문  
  
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
  
 실행 타임 구문  
  
```  
  
DataControl.Server="computername"  
```  
  
 **In process**  
  
 디자인 타임 구문  
  
```  
  
<PARAM NAME="Server" VALUE="">  
  
```  
  
 실행 타임 구문  
  
```  
  
DataControl.Server=""  
```  
  
## <a name="parameters"></a>매개 변수  
 *awebsrvr*또는 *computername*  
 A **문자열** 서버에 있으면 원격 컴퓨터 또는 빈 문자열 서버가 로컬 컴퓨터의 경우는 인터넷 또는 인트라넷 경로 또는 컴퓨터 이름을 포함 하는 값입니다.  
  
 *port*  
 선택 사항입니다. IIS를 실행 하는 서버에 연결 하는 데 사용 되는 포트입니다. 포트 번호는 Internet Explorer에서 설정 됩니다 (에 **뷰** 메뉴에서 클릭 **옵션**를 선택한 후는 **연결** 탭) 또는 IIS에서.  
  
 *DataControl*  
 나타내는 개체 변수는 **rds. DataControl** 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 서버 위치를 위치는 **rds. DataControl** (즉, 쿼리 또는 업데이트) 요청이 처리 됩니다. 기본적으로 모든 요청이 처리 되는 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체를 [MSDFMAP 합니다. 처리기](../../../ado/guide/remote-data-service/datafactory-customization.md) 구성 요소 및 [MSDFMAP 합니다. INI](../../../ado/guide/remote-data-service/understanding-the-customization-file.md) 지정된 된 서버에서 파일입니다. 이전 및 새 설정을 조정 하는 서버를 변경 하는 경우 사용자에 게 유의 **MSDFMAP 합니다. INI** 파일입니다. 호환 되지 않는 다른 하나의 서버에서 성공 하는 요청을 발생할 수 있습니다. 서버 속성을 빈 문자열로 설정 된 경우 "", 로컬 컴퓨터에서 이러한 개체를 사용할 수는 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목  
 [서버 속성 예제 (VBScript)](../../../ado/reference/rds-api/server-property-example-vbscript.md)   
 [Connect 속성 (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [SQL 속성](../../../ado/reference/rds-api/sql-property.md)   
 [SubmitChanges 메서드(RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


