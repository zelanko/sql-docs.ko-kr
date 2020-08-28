---
description: 주소록 데이터 바인딩 개체
title: 주소록 데이터-바인딩 개체 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS scenarios [ADO], data-binding object
- address book application scenario [ADO], data-binding object
ms.assetid: 080c1925-d453-4b89-92ac-c93591490518
author: rothja
ms.author: jroth
ms.openlocfilehash: d6b6bb99ea218268a7ccb988acb2f49fb4898f32
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978444"
---
# <a name="address-book-data-binding-object"></a>주소록 데이터 바인딩 개체
주소록 응용 프로그램은 RDS를 사용 합니다 [. ](../../reference/rds-api/datacontrol-object-rds.md) 응용 프로그램의 클라이언트 HTML 페이지에서 SQL Server 데이터베이스의 시각적 개체 (이 경우 DHTML 테이블)에 데이터를 바인딩하는 DataControl 개체입니다. 이벤트 기반 VBScript 프로그램 논리는 RDS를 사용 합니다 [. DataControl](../../reference/rds-api/datacontrol-object-rds.md) :  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
-   데이터베이스를 쿼리하고 데이터베이스에 업데이트를 보내고 데이터 그리드를 새로 고칩니다.  
  
-   사용자가 데이터 표의 첫 번째, 다음, 이전 또는 마지막 레코드로 이동할 수 있도록 허용 합니다.  
  
 다음 코드에서는 RDS를 정의 합니다 **. DataControl** 구성 요소:  
  
```vb
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=DC1 Width=1 Height=1>  
   <PARAM NAME="SERVER" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=sqloledb;  
Initial Catalog=AddrBookDb;Integrated Security=SSPI;">  
</OBJECT>  
```  
  
 개체 태그는 RDS를 정의 합니다 **. ** 프로그램의 DataControl 구성 요소입니다. 태그에는 두 가지 유형의 매개 변수가 포함 되어 있습니다.  
  
-   제네릭 개체 태그와 연결 된 개체입니다.  
  
-   RDS와 관련 된 것 **입니다. DataControl** 개체입니다.  
  
## <a name="generic-object-tag-parameters"></a>일반 개체 태그 매개 변수  
 다음 표에서는 개체 태그와 연결 된 매개 변수에 대해 설명 합니다.  
  
|매개 변수|설명|  
|---------------|-----------------|  
|***CLASSID***|시스템에 포함 된 개체의 유형을 식별 하는 고유 128 비트 번호입니다. 이 식별자는 로컬 컴퓨터의 시스템 레지스트리에서 유지 관리 됩니다. (RDS의 클래스 Id에 해당 **합니다. DataControl** 개체 RDS를 참조 하십시오 [. DataControl 개체](../../reference/rds-api/datacontrol-object-rds.md)입니다.|  
|***ID***|코드에서이를 식별 하는 데 사용 되는 포함 된 개체의 문서 전체 식별자를 정의 합니다.|  
  
## <a name="rdsdatacontrol-tag-parameters"></a>RDS. DataControl 태그 매개 변수  
 다음 표에서는 RDS와 관련 된 매개 변수에 대해 설명 합니다 **. DataControl** 개체입니다. (RDS의 전체 목록은 ** DataControl** 개체 매개 변수 및이 매개 변수를 구현 하는 경우 RDS를 참조 하세요 [. DataControl 개체](../../reference/rds-api/datacontrol-object-rds.md)입니다.  
  
|매개 변수|설명|  
|---------------|-----------------|  
|[서버인](../../reference/rds-api/server-property-rds.md)|HTTP를 사용 하는 경우이 값은 앞에 오는 서버 컴퓨터의 이름입니다 `https://` .|  
|[CONNECT](../../reference/rds-api/connect-property-rds.md)|RDS에 필요한 연결 정보를 제공 합니다 **. ** SQL Server에 연결 하는 DataControl입니다.|  
|[SQL](../../reference/rds-api/sql-property.md)|[레코드 집합](../../reference/ado-api/recordset-object-ado.md)을 검색 하는 데 사용 되는 쿼리 문자열을 설정 하거나 반환 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [주소록 명령 단추](./address-book-command-buttons.md)