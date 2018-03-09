---
title: "주소록 데이터 바인딩 개체 주소 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS scenarios [ADO], data-binding object
- address book application scenario [ADO], data-binding object
ms.assetid: 080c1925-d453-4b89-92ac-c93591490518
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9689d8c41a899c9446f3f21ede83ea88c68b77a3
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="address-book-data-binding-object"></a>주소록 데이터 바인딩 개체
주소록 응용 프로그램이 사용 하 여 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 에서 데이터를 바인딩할 SQL Server 데이터베이스 (이 경우 DHTML 테이블)에 시각적 개체를 응용 프로그램의 HTML 클라이언트 페이지 개체입니다. 이벤트 기반 VBScript 프로그램 논리를 사용 하 여는 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 에:  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
-   데이터베이스를 쿼리하고 업데이트를 데이터베이스로 보내는 데이터 표를 새로 고칩니다.  
  
-   데이터 표의 사용자가을 이전, 첫 번째, 다음으로 이동 하거나 마지막 레코드를 허용 합니다.  
  
 다음 코드 정의 **.rds입니다 DataControl** 구성 요소:  
  
```  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=DC1 Width=1 Height=1>  
   <PARAM NAME="SERVER" VALUE="http://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=sqloledb;  
Initial Catalog=AddrBookDb;Integrated Security=SSPI;">  
</OBJECT>  
```  
  
 OBJECT 태그를 정의 고 **.rds입니다 DataControl** 프로그램에 구성 요소입니다. 두 가지 유형의 매개 변수를 포함 하는 태그:  
  
-   일반 개체 태그와 연결 된 것입니다.  
  
-   에 특정 하는 것은 **.rds입니다 DataControl** 개체입니다.  
  
## <a name="generic-object-tag-parameters"></a>일반 개체 태그 매개 변수  
 다음 표에서 OBJECT 태그와 연결 된 매개 변수를 설명 합니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|***CLASSID***|시스템에 포함 된 개체의 형식을 식별 하는 고유, 128 비트 수입니다. 이 식별자는 로컬 컴퓨터의 시스템 레지스트리에 유지 됩니다. (의 클래스 id는 **.rds입니다 DataControl** 개체, 참조 [.rds입니다 DataControl 개체](../../../ado/reference/rds-api/datacontrol-object-rds.md).)|  
|***ID***|코드에서 식별 하는 데 사용 되는 포함된 된 개체에 대 한 문서 차원의 식별자를 정의 합니다.|  
  
## <a name="rdsdatacontrol-tag-parameters"></a>.RDS DataControl 태그 매개 변수  
 다음 표에서 설명 하는 특정 매개 변수에 **.rds입니다 DataControl** 개체입니다. (전체 목록은 **.rds입니다 DataControl** 매개 변수 및 구현, 참조 하는 경우 개체 [.rds입니다 DataControl 개체](../../../ado/reference/rds-api/datacontrol-object-rds.md).)  
  
|매개 변수|Description|  
|---------------|-----------------|  
|[SERVER](../../../ado/reference/rds-api/server-property-rds.md)|값은 앞에 서버 컴퓨터의 이름 HTTP를 사용 하는 경우 `http://`합니다.|  
|[CONNECT](../../../ado/reference/rds-api/connect-property-rds.md)|에 대 한 필요한 연결 정보를 제공는 **.rds입니다 DataControl** SQL Server에 연결 합니다.|  
|[SQL](../../../ado/reference/rds-api/sql-property.md)|설정 하거나 검색 하는 데 쿼리 문자열을 반환 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [주소록 명령 단추](../../../ado/guide/remote-data-service/address-book-command-buttons.md)


