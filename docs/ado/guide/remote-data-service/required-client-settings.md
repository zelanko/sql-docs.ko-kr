---
description: 필수 클라이언트 설정
title: 필수 클라이언트 설정 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
ms.assetid: e776b4e3-fcc4-4bfb-a7e8-5ffae1d83833
author: rothja
ms.author: jroth
ms.openlocfilehash: 5263da344d39b828b431efd99a4171f74d2552db
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759383"
---
# <a name="required-client-settings"></a>필수 클라이언트 설정
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 사용자 지정 **DataFactory** 처리기를 사용 하려면 다음 설정을 지정 합니다.  
  
-   [Connection 개체 (ado)](../../reference/ado-api/connection-object-ado.md) 개체 [공급자 속성 (ado)](../../reference/ado-api/provider-property-ado.md) 속성 또는 **연결** 개체 연결 문자열 "**provider**=" 키워드에 "provider = MS Remote"를 지정 합니다.  
  
-   [CursorLocation 속성 (ADO)](../../reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**로 설정 합니다.  
  
-   [DataControl 개체 (RDS)](../../reference/rds-api/datacontrol-object-rds.md) 개체의 **Handler** 속성 또는 [레코드 집합 개체 (ADO)](../../reference/ado-api/recordset-object-ado.md) 개체의 연결 문자열 "**handler**=" 키워드에 사용할 처리기의 이름을 지정 합니다. **연결** 개체 연결 문자열에는 처리기를 설정할 수 없습니다.  
  
 RDS는 Msdfmap 이라는 서버에 기본 처리기를 제공 합니다 **. 처리기**. 기본 사용자 지정 파일의 이름은 MSDFMAP.INI입니다.  
  
 **예제**  
  
 **MSDFMAP.INI** 및 데이터 원본 이름인 AdvWorks의 다음 섹션이 이전에 정의 되어 있다고 가정 합니다.  
  
```console
[connect CustomerDataBase]  
Access=ReadWrite  
Connect="DSN=AdvWorks"  
  
[sql CustomerById]  
SQL="SELECT * FROM Customers WHERE CustomerID = ?"  
```  
  
 다음 코드 조각은 Visual Basic 작성 됩니다.  
  
## <a name="rdsdatacontrol-version"></a>RDS. DataControl 버전  
  
```vb
Dim dc as New RDS.DataControl  
Set dc.Handler = "MSDFMAP.Handler"  
Set dc.Server = "https://yourServer"  
Set dc.Connect = "Data Source=CustomerDatabase"  
Set dc.SQL = "CustomerById(4)"  
dc.Refresh  
```  
  
## <a name="recordset-version"></a>레코드 집합 버전  
  
```vb
Dim rs as New ADODB.Recordset  
rs.CursorLocation = adUseClient  
```  
  
 [Handler 속성 (RDS)](../../reference/rds-api/handler-property-rds.md) 속성 또는 키워드를 지정 합니다. [공급자 속성 (ADO)](../../reference/ado-api/provider-property-ado.md) 속성 또는 키워드 *CustomerById* 및 *customerdatabase* 식별자가 있습니다. 그런 다음 **레코드 집합** 개체를 엽니다.  
  
 dvd-r. "CustomerById (4)", "Handler = MSDFMAP을 엽니다. Handler; "& _  
  
```vb
"Provider=MS Remote;Data Source=CustomerDatabase;" & _  
"Remote Server=https://yourServer"  
```  
  
## <a name="see-also"></a>관련 항목  
 [사용자 지정 파일 연결 섹션](./customization-file-connect-section.md)   
 [사용자 지정 파일 SQL 섹션](./customization-file-sql-section.md)   
 [사용자 지정 파일 UserList 섹션](./customization-file-userlist-section.md)   
 [DataFactory 사용자 지정](./datafactory-customization.md)   
 [필수 클라이언트 설정]()   
 [사용자 지정 파일 이해](./understanding-the-customization-file.md)   
 [고유한 사용자 지정된 처리기 작성](./writing-your-own-customized-handler.md)