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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963220"
---
# <a name="url-property-rds"></a>URL 속성(RDS)
상대 또는 절대 URL이 포함 된 문자열을 나타냅니다.  
  
 설정할 수 있습니다 합니다 **URL** 에서 디자인 타임에 속성을 [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 개체 태그 또는 런타임에 스크립트 코드에서.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Design time: <PARAM NAME="URL" VALUE="Server">  
Run time: DataControl.URL="Server"  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Server*  
 A **문자열** 올바른 URL을 포함 하는 값입니다.  
  
 *DataControl*  
 나타내는 개체 변수를 **DataControl** 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 URL을 생성 하 고 반환할 수 있는 Active Server Page (.asp) 파일을 식별 하는 일반적으로 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다. 따라서 사용자 얻을 수는 **레코드 집합** 서버 쪽 호출 하지 않고도 [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체 또는 사용자 지정 비즈니스 개체를 프로그래밍 합니다.  
  
 경우는 **URL** 속성이 설정 된 [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) 제출 URL에 의해 지정 된 위치로 변경 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목  
 [URL 속성 예제(VBScript)](../../../ado/reference/rds-api/url-property-example-vbscript.md)


