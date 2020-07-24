---
title: InternetTimeout 속성 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- InternetTimeout property [ADO]
ms.assetid: 4d1c8892-4bbc-4e71-bf4b-ba52c0ea9549
author: rothja
ms.author: jroth
ms.openlocfilehash: 30de657985eafdc5a601d61fedbd666455f3dbc9
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86941065"
---
# <a name="internettimeout-property-rds"></a>InternetTimeout 속성(RDS)
요청 시간이 초과 될 때까지 대기 하는 시간 (밀리초)을 나타냅니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 요청 시간이 초과 되기 전 까지의 시간 (밀리초)을 나타내는 **Long** 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 이 속성은 HTTP 또는 HTTPS 프로토콜을 사용 하 여 보낸 요청에만 적용 됩니다.  
  
 3 계층 환경의 요청은 실행 하는 데 몇 분 정도 걸릴 수 있습니다. 이 속성을 사용 하 여 장기 실행 요청에 대 한 추가 시간을 지정 합니다.  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
    :::column-end:::
    :::column:::
        [DataSpace 개체(RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [InternetTimeout 속성 예제 (VB)](../../../ado/reference/rds-api/internettimeout-property-example-vb.md)   
 [InternetTimeout 속성 예제(VC++)](../../../ado/reference/rds-api/internettimeout-property-example-vc.md)   
 

