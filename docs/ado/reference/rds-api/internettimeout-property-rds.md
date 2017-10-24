---
title: "InternetTimeout 속성 (RDS) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- InternetTimeout property [ADO]
ms.assetid: 4d1c8892-4bbc-4e71-bf4b-ba52c0ea9549
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2320ba200cf8343a32e2a0d00589a80014517260
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="internettimeout-property-rds"></a>InternetTimeout 속성 (RDS)
요청이 시간 초과 전까지 대기 하는 시간 (밀리초)의 수를 나타냅니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **긴** 시간이 초과 (밀리초)는 요청 수를 나타내는 값입니다.  
  
## <a name="remarks"></a>주의  
 HTTP 또는 HTTPS 프로토콜에 보낸 요청에만이 속성이 적용 됩니다.  
  
 3 계층 환경에서 요청을 실행 하는 데 몇 분 정도 걸릴 수 있습니다. 이 속성을 사용 하 여 장기 실행 요청에 대 한 추가 시간을 지정 합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[DataSpace 개체(RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [InternetTimeout 속성 예제 (VB)](../../../ado/reference/rds-api/internettimeout-property-example-vb.md)   
 [InternetTimeout 속성 예제(VC++)](../../../ado/reference/rds-api/internettimeout-property-example-vc.md)   
 


