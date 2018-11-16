---
title: 주소록 데이터 바인딩 개체 주소 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS scenarios [ADO], data-binding object
- address book application scenario [ADO], data-binding object
ms.assetid: 080c1925-d453-4b89-92ac-c93591490518
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da63965c867c56572956ca5400a4b9dcc1281abf
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51601914"
---
# <a name="address-book-data-binding-object"></a>주소록 데이터 바인딩 개체
주소록 응용 프로그램이 사용 하 여 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 응용 프로그램의 HTML 클라이언트 페이지에서 데이터를 SQL Server 데이터베이스에서 시각적 개체 (이 경우 DHTML 테이블)에 바인딩되는 개체입니다. 이벤트 구동 VBScript 프로그램 논리를 사용 하 여 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 에:  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
-   데이터베이스를 쿼리하고 업데이트를 데이터베이스로 보내는 데이터 그리드를 새로 고칩니다.  
  
-   데이터 그리드에서 사용자가 이전, 첫 번째, 다음으로, 이동 또는 마지막 레코드를 허용 합니다.  
  
 다음 코드는 정의 된 **rds. DataControl** 구성 요소:  
  
```vb
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=DC1 Width=1 Height=1>  
   <PARAM NAME="SERVER" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=sqloledb;  
Initial Catalog=AddrBookDb;Integrated Security=SSPI;">  
</OBJECT>  
```  
  
 OBJECT 태그 정의 **rds. DataControl** 프로그램의 구성 요소입니다. 태그는 두 가지 유형의 매개 변수를 포함 합니다.  
  
-   이러한 제네릭 OBJECT 태그를 사용 하 여 연결 합니다.  
  
-   관련 된는 **rds. DataControl** 개체입니다.  
  
## <a name="generic-object-tag-parameters"></a>제네릭 개체 Tag 매개 변수  
 다음 표에서 OBJECT 태그와 연결 된 매개 변수를 설명 합니다.  
  
|매개 변수|설명|  
|---------------|-----------------|  
|***CLASSID***|시스템에 포함 된 개체의 형식을 식별 하는 고유한, 128 비트 숫자입니다. 이 식별자는 로컬 컴퓨터의 시스템 레지스트리에 유지 됩니다. (의 클래스 id를 **rds. DataControl** 개체를 참조 하십시오 [rds. DataControl 개체](../../../ado/reference/rds-api/datacontrol-object-rds.md).)|  
|***ID***|코드에서 식별 하는 데 사용 되는 포함된 된 개체에 대 한 문서 차원의 식별자를 정의 합니다.|  
  
## <a name="rdsdatacontrol-tag-parameters"></a>RDS. DataControl Tag 매개 변수  
 다음 표에서 관련 된 매개 변수에 **rds. DataControl** 개체입니다. (전체 목록은 **rds. DataControl** 매개 변수 및 구현, 참조 하는 경우 개체 [rds. DataControl 개체](../../../ado/reference/rds-api/datacontrol-object-rds.md).)  
  
|매개 변수|설명|  
|---------------|-----------------|  
|[서버](../../../ado/reference/rds-api/server-property-rds.md)|값 앞에 서버 컴퓨터의 이름인 HTTP를 사용 하는 경우 `https://`합니다.|  
|[CONNECT](../../../ado/reference/rds-api/connect-property-rds.md)|필요한 연결 정보를 제공 합니다 **rds. DataControl** SQL Server에 연결 합니다.|  
|[SQL](../../../ado/reference/rds-api/sql-property.md)|설정 하거나 검색 하는 데 사용 하는 쿼리 문자열을 반환 합니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [주소록 명령 단추](../../../ado/guide/remote-data-service/address-book-command-buttons.md)


