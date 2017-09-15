---
title: "URL 속성 (RDS) | Microsoft Docs"
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
- URL property [ADO]
ms.assetid: 8c56b233-1be8-442c-8d0e-a4c96465bc99
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: feda106c2ce5450fa86550dbc83fd40c928c1510
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="url-property-rds"></a>URL 속성 (RDS)
상대 또는 절대 URL이 포함 된 문자열을 나타냅니다.  
  
 설정할 수 있습니다는 **URL** 에서 디자인 타임에 속성의 [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 개체 태그 또는 런타임 시 스크립트 코드에 있습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Design time: <PARAM NAME="URL" VALUE="Server">  
Run time: DataControl.URL="Server"  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Server*  
 A **문자열** 유효한 URL이 포함 된 값입니다.  
  
 *DataControl*  
 개체 변수를 나타내는 **DataControl** 개체입니다.  
  
## <a name="remarks"></a>주의  
 URL을 생성 하 고 반환할 수 있는 Active Server Page (.asp) 파일을 식별 하는 일반적으로 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다. 따라서 사용자를 가져올 수는 **레코드 집합** 를 서버 쪽을 호출할 필요 없이 [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체 또는 사용자 지정 비즈니스 개체를 프로그래밍 합니다.  
  
 경우는 **URL** 속성이 설정 되어 [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) 변경 내용을 URL에서 지정한 위치에 전송 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목:  
 [URL 속성 예제(VBScript)](../../../ado/reference/rds-api/url-property-example-vbscript.md)



