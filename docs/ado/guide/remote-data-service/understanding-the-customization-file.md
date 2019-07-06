---
title: 사용자 지정 파일 이해 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- customization file in RDS [ADO]
ms.assetid: 136f74bf-8d86-4a41-be66-c86cbcf81548
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d58edcfae92c94cfc635d3539f81faf834e382c7
ms.sourcegitcommit: d9c5b9ab3c282775ed61712892eeb3e150ccc808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67597567"
---
# <a name="understanding-the-customization-file"></a>사용자 지정 파일 이해
사용자 지정 파일의 각 섹션 헤더 대괄호로 구성 됩니다 ( **[]** ) 형식 및 매개 변수를 포함 합니다. 네 가지 섹션 유형은 리터럴 문자열에 표시 됩니다 **연결**, **sql**합니다 **userlist**, 또는 **로그**합니다. 리터럴 문자열, 기본, 사용자가 지정한 식별자를 또는 nothing입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 따라서 각 섹션의 다음 섹션 헤더 중 하나를 사용 하 여 표시 됩니다.  
  
```console
  
[ connect default ] [ connect    
identifier   
] [ sql  default ] [ sql    
identifier   
] [ userlist    
identifier   
] [ logs ]  
  
```  
  
 섹션 헤더 같은 부분이 포함 됩니다.  
  
|부분|설명|  
|----------|-----------------|  
|**connect**|연결 문자열을 수정 하는 리터럴 문자열입니다.|  
|**sql**|명령 문자열을 수정 하는 리터럴 문자열입니다.|  
|**userlist**|특정 사용자의 액세스 권한을 수정 하는 리터럴 문자열입니다.|  
|**logs**|작업 오류를 기록 하는 로그 파일을 지정 하는 리터럴 문자열입니다.|  
|**default**|지정 되었거나 찾을 식별자가 없는 경우 사용 되는 리터럴 문자열입니다.|  
|*identifier*|문자열을 일치 하는 문자열을 **연결** 또는 **명령** 문자열입니다.<br /><br /> -섹션 헤더를 포함 하는 경우이 섹션을 사용 **연결** 연결 문자열에 식별자 문자열이 발견 되 고 있습니다.<br />-섹션 헤더를 포함 하는 경우이 섹션을 사용 **sql** 명령 문자열에 식별자 문자열이 발견 되 고 있습니다.<br />-섹션 헤더를 포함 하는 경우이 섹션을 사용 **userlist** 식별자 문자열 일치는 **연결** 섹션 식별자입니다.|  
  
 합니다 **DataFactory** 클라이언트 매개 변수를 전달 하는 처리기를 호출 합니다. 처리기를 적절 한 섹션 헤더에는 식별자와 일치 하는 클라이언트 매개 변수에서 전체 문자열을 검색 합니다. 일치 하는 항목이 있으면 해당 섹션의 내용은 클라이언트 매개 변수에 적용 됩니다.  
  
 특정 섹션은 다음 상황에서 사용 됩니다.  
  
-   **연결** 클라이언트의 값 부분 연결 문자열 키워드 섹션은 "**데이터 원본 =** _값_"를 일치 하는 **연결** 섹션 식별자입니다. 
  
-   **sql** 섹션 클라이언트 명령 문자열을 일치 하는 문자열을 포함 하는 경우 사용 되는 **sql** 섹션 식별자입니다.  
  
-   A **연결** 하거나 **sql** 기본 매개 변수를 사용 하 여 섹션은 일치 하는 식별자가 없는 경우 사용 됩니다.  
  
-   A **userlist** 섹션이 사용 됩니다 합니다 **userlist** 식별자 일치 섹션을 **연결** 섹션 식별자입니다. 일치 하는 내용의 경우 합니다 **userlist** 섹션에 따라 연결에 적용 되는 **연결** 섹션.  
  
-   연결이 나 명령 문자열에서 문자열에 식별자를 일치 하지 않는 경우 **연결** 하거나 **sql** 헤더 섹션 및 방법이 없음 **연결** 또는 **sql**  클라이언트 문자열 수정 하지 않아도 되는 기본 매개 변수를 사용 하 여 헤더 섹션입니다.  
  
-   **로그** 섹션을 사용 하 때마다 합니다 **DataFactory** 이 작동 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [사용자 지정 파일 연결 섹션](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [사용자 지정 파일 로그 섹션](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [사용자 지정 파일 SQL 섹션](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [사용자 지정 파일 UserList 섹션](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 사용자 지정](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [필수 클라이언트 설정](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [고유한 사용자 지정된 처리기 작성](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)

