---
title: 필요한 클라이언트 설정 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
ms.assetid: e776b4e3-fcc4-4bfb-a7e8-5ffae1d83833
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9323561f533cf4d7f0b11aa23ed5da5b8cdce768
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="required-client-settings"></a>필요한 클라이언트 설정
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 사용자 지정을 사용 하려면 다음 설정을 지정한 **DataFactory** 처리기입니다.  
  
-   지정 "Provider = MS 원격"에 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) 개체 [공급자 속성 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) 속성 또는 **연결** 개체 연결 문자열 "**공급자**= "키워드입니다.  
  
-   설정의 [앞 속성 (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**합니다.  
  
-   사용 하는 처리기의 이름을 지정는 [DataControl 개체 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 **처리기** 속성 또는 [Recordset 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) "개체의연결문자열 **처리기**= "키워드입니다. (처리기 설정할 수 없습니다는 **연결** 개체 연결 문자열입니다.)  
  
 명명 된 서버에서 기본 처리기를 제공 하는 RDS **MSDFMAP 합니다. 처리기**합니다. (기본 사용자 지정 파일 MSDFMAP 이름은입니다. INI입니다.)  
  
 **예제**  
  
 다음 섹션에 가정 **MSDFMAP 합니다. INI** AdvWorks, 데이터 소스 이름, 이전에 정의한 및:  
  
```  
[connect CustomerDataBase]  
Access=ReadWrite  
Connect="DSN=AdvWorks"  
  
[sql CustomerById]  
SQL="SELECT * FROM Customers WHERE CustomerID = ?"  
```  
  
 다음 코드 조각은 Visual Basic로 작성 됩니다.  
  
## <a name="rdsdatacontrol-version"></a>.RDS DataControl 버전  
  
```  
Dim dc as New RDS.DataControl  
Set dc.Handler = "MSDFMAP.Handler"  
Set dc.Server = "http://yourServer"  
Set dc.Connect = "Data Source=CustomerDatabase"  
Set dc.SQL = "CustomerById(4)"  
dc.Refresh  
```  
  
## <a name="recordset-version"></a>레코드 집합 버전  
  
```  
Dim rs as New ADODB.Recordset  
rs.CursorLocation = adUseClient  
```  
  
 지정 된 [처리기 속성 (RDS)](../../../ado/reference/rds-api/handler-property-rds.md) 속성 또는 키워드입니다;는 [공급자 속성 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) 속성 또는 키워드입니다; 및 *CustomerById* 및  *CustomerDatabase* 식별자입니다. 다음 열은 **레코드 집합** 개체  
  
 rs.Open "CustomerById(4)", "Handler=MSDFMAP.Handler;" & _  
  
```  
"Provider=MS Remote;Data Source=CustomerDatabase;" & _  
"Remote Server=http://yourServer"  
```  
  
## <a name="see-also"></a>관련 항목:  
 [사용자 지정 파일 연결 섹션](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [사용자 지정 파일 SQL 섹션](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [사용자 지정 파일 UserList 섹션](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 사용자 지정](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [필요한 클라이언트 설정](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [사용자 지정 파일 이해](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [고유한 사용자 지정된 처리기 작성](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)






















