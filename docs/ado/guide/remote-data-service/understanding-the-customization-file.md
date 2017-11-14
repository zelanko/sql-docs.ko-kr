---
title: "사용자 지정 파일을 이해 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- customization file in RDS [ADO]
ms.assetid: 136f74bf-8d86-4a41-be66-c86cbcf81548
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cadf89ac579b11ab829ecd288fec77df81eb0603
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-the-customization-file"></a>사용자 지정 파일 이해
사용자 지정 파일의 각 섹션 헤더 대괄호로 구성 됩니다 (****) 형식 및 매개 변수를 포함 합니다. 4 개의 섹션 형식 리터럴 문자열으로 표시 됩니다 **연결**, **sql**, **userlist**, 또는 **로그**합니다. 리터럴 문자열, 기본값, 사용자 지정 식별자 또는 nothing입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 따라서 각 섹션은 기본적으로 다음 섹션 헤더 중 하나:  
  
```  
  
[ connect default ] [ connect    
identifier   
] [ sql  default ] [ sql    
identifier   
] [ userlist    
identifier   
] [ logs ]  
  
```  
  
 섹션 헤더는 다음과 같은 부분이 있어야 합니다.  
  
|부분|Description|  
|----------|-----------------|  
|**연결**|연결 문자열을 수정 하는 리터럴 문자열입니다.|  
|**sql**|명령 문자열을 수정 하는 리터럴 문자열입니다.|  
|**userlist**|특정 사용자의 액세스 권한을 수정 하는 리터럴 문자열입니다.|  
|**로그**|작업 오류를 기록 하는 로그 파일을 지정 하는 리터럴 문자열입니다.|  
|**기본값**|없는 식별자가 지정 되지 않았거나 경우 사용 되는 리터럴 문자열입니다.|  
|*식별자*|문자열에서 일치 하는 문자열은 **연결** 또는 **명령** 문자열입니다.<br /><br /> -섹션 헤더를 포함 하는 경우이 섹션에서는 **연결** 식별자 문자열이 연결 문자열에서 발견 되 고 있습니다.<br />-섹션 헤더를 포함 하는 경우이 섹션에서는 **sql** 식별자 문자열이 명령 문자열에서 발견 되 고 있습니다.<br />-섹션 헤더를 포함 하는 경우이 섹션에서는 **userlist** 식별자 문자열이 일치는 **연결** 섹션 식별자입니다.|  
  
 **DataFactory** 클라이언트 매개 변수를 전달 하는 처리기를 호출 합니다. 처리기를 적절 한 섹션 헤더에는 식별자와 일치 하는 클라이언트 매개 변수에서 전체 문자열을 검색 합니다. 일치 하는 항목이 있으면 해당 섹션의 내용은 클라이언트 매개 변수에 적용 됩니다.  
  
 특정 섹션은 다음과 같은 상황에서 사용 됩니다.  
  
-   A **연결** 섹션을 사용 하는 클라이언트의 값 부분 연결 문자열 키워드 "**데이터 원본 =***값*", 일치 하는 **연결** 섹션 식별자*합니다.*  
  
-   **sql** 섹션을 사용 하는 클라이언트 명령 문자열 일치 하는 문자열을 포함 하는 경우는 **sql** 섹션 식별자입니다.  
  
-   A **연결** 또는 **sql** 식별자가 없으면 일치 하는 기본 매개 변수를 사용 하는 섹션이 사용 됩니다.  
  
-   A **userlist** 섹션을 사용 하는 경우는 **userlist** 섹션 일치 하는 항목 식별자는 **연결** 섹션 식별자입니다. 내용을 일치 항목이 있는 경우는 **userlist** 섹션에 의해 제어 되는 연결에 적용 되는 **연결** 섹션.  
  
-   연결 나 명령 문자열의 문자열 식별자에서 일치 하지 않으면 **연결** 또는 **sql** 헤더 섹션 고 없습니다 **연결** 또는 **sql ** 아니면 클라이언트 문자열을 사용 하 여 수정 하지 않고 기본 매개 변수를 사용 하는 헤더 섹션.  
  
-   **로그** 섹션을 사용 될 때마다는 **DataFactory** 작업에 포함 되어 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [사용자 지정 파일 연결 섹션](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [사용자 지정 파일 로그 섹션](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [사용자 지정 파일 SQL 섹션](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [사용자 지정 파일 UserList 섹션](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 사용자 지정](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [필요한 클라이언트 설정](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [고유한 사용자 지정된 처리기 작성](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)





















