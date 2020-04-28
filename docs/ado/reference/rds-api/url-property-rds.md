---
title: URL 속성 (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- URL property [ADO]
ms.assetid: 8c56b233-1be8-442c-8d0e-a4c96465bc99
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c88b8029ee5d96986cf9b366bd8faee53ca1393b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67963220"
---
# <a name="url-property-rds"></a>URL 속성(RDS)
상대 또는 절대 URL이 포함 된 문자열을 나타냅니다.  
  
 디자인 타임에 [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 개체 태그 또는 런타임에 스크립팅 코드에서 **URL** 속성을 설정할 수 있습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Design time: <PARAM NAME="URL" VALUE="Server">  
Run time: DataControl.URL="Server"  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Server*  
 유효한 URL을 포함 하는 **문자열** 값입니다.  
  
 *DataControl*  
 **DataControl** 개체를 나타내는 개체 변수입니다.  
  
## <a name="remarks"></a>설명  
 일반적으로 URL은 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)을 생성 하 고 반환할 수 있는 Active Server 페이지 (.asp) 파일을 식별 합니다. 따라서 사용자는 서버측 [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체를 호출 하거나 사용자 지정 비즈니스 개체를 프로그래밍 하지 않고도 **레코드 집합** 을 가져올 수 있습니다.  
  
 **Url** 속성이 설정 된 경우 [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) 는 url로 지정 된 위치에 변경 내용을 전송 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [URL 속성 예제(VBScript)](../../../ado/reference/rds-api/url-property-example-vbscript.md)


