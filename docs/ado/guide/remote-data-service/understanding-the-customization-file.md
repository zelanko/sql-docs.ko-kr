---
description: 사용자 지정 파일 이해
title: 사용자 지정 파일 이해 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- customization file in RDS [ADO]
ms.assetid: 136f74bf-8d86-4a41-be66-c86cbcf81548
author: rothja
ms.author: jroth
ms.openlocfilehash: 9b097d54015d9f48140aafb6feb360b8013edeaf
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977394"
---
# <a name="understanding-the-customization-file"></a>사용자 지정 파일 이해
사용자 지정 파일의 각 섹션 헤더는 형식 및 매개 변수를 포함 하는 대괄호 (**[]**)로 구성 됩니다. 네 가지 섹션 형식은 **connect**, **sql**, **userlist**또는 **logs**리터럴 문자열로 표시 됩니다. 매개 변수는 리터럴 문자열, 기본값, 사용자 지정 식별자 또는 nothing입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 따라서 각 섹션은 다음 섹션 헤더 중 하나로 표시 됩니다.  
  
```console
  
[ connect default ] [ connect    
identifier   
] [ sql  default ] [ sql    
identifier   
] [ userlist    
identifier   
] [ logs ]  
  
```  
  
 섹션 헤더에는 다음과 같은 부분이 있습니다.  
  
|부분|설명|  
|----------|-----------------|  
|**connect**|연결 문자열을 수정 하는 리터럴 문자열입니다.|  
|**sql**|명령 문자열을 수정 하는 리터럴 문자열입니다.|  
|**userlist**|특정 사용자의 액세스 권한을 수정 하는 리터럴 문자열입니다.|  
|**로그온**|작업 오류를 기록 하는 로그 파일을 지정 하는 리터럴 문자열입니다.|  
|**default**|지정 된 식별자가 없거나 없는 경우 사용 되는 리터럴 문자열입니다.|  
|*identifier*|**Connect** 또는 **command** 문자열의 문자열과 일치 하는 문자열입니다.<br /><br /> -섹션 헤더에 **connect** 가 있고 식별자 문자열이 연결 문자열에 있는 경우이 섹션을 사용 합니다.<br />-섹션 헤더에 **sql** 이 포함 되어 있고 식별자 문자열이 명령 문자열에 있는 경우이 섹션을 사용 합니다.<br />-섹션 헤더에 **userlist** 가 포함 되어 있고 식별자 문자열이 **connect** 섹션 식별자와 일치 하는 경우이 섹션을 사용 합니다.|  
  
 **DataFactory** 는 클라이언트 매개 변수를 전달 하 여 처리기를 호출 합니다. 처리기는 해당 섹션 헤더의 식별자와 일치 하는 클라이언트 매개 변수에서 전체 문자열을 검색 합니다. 일치 하는 항목이 발견 되 면 해당 섹션의 내용이 클라이언트 매개 변수에 적용 됩니다.  
  
 특정 섹션은 다음과 같은 경우에 사용 됩니다.  
  
-   Connect **섹션은** 클라이언트 연결 문자열 키워드인 "**Data Source =**_value_"의 값 부분이 **connect** 섹션 식별자와 일치 하는 경우에 사용 됩니다. 
  
-   Sql **섹션은** 클라이언트 명령 문자열에 **sql** 섹션 식별자와 일치 하는 문자열이 포함 된 경우에 사용 됩니다.  
  
-   일치 하는 식별자가 없는 경우 기본 매개 변수가 있는 **connect** 또는 **sql** 섹션이 사용 됩니다.  
  
-   **Userlist** 섹션 식별자가 **connect** 섹션 식별자와 일치 하는 경우 **userlist** 섹션이 사용 됩니다. 일치 하는 항목이 있으면 **userlist** 섹션의 내용이 **connect** 섹션에서 제어 하는 연결에 적용 됩니다.  
  
-   연결 또는 명령 문자열의 문자열이 **connect** 또는 **sql** 섹션 헤더의 식별자와 일치 하지 않는 경우 및 기본 매개 변수를 사용 하는 **connect** 또는 **sql** 섹션 헤더가 없으면 클라이언트 문자열이 수정 없이 사용 됩니다.  
  
-   **로그** 섹션은 **DataFactory** 가 작업 중일 때마다 사용 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [사용자 지정 파일 연결 섹션](./customization-file-connect-section.md)   
 [사용자 지정 파일 로그 섹션](./customization-file-logs-section.md)   
 [사용자 지정 파일 SQL 섹션](./customization-file-sql-section.md)   
 [사용자 지정 파일 UserList 섹션](./customization-file-userlist-section.md)   
 [DataFactory 사용자 지정](./datafactory-customization.md)   
 [필수 클라이언트 설정](./required-client-settings.md)   
 [고유한 사용자 지정된 처리기 작성](./writing-your-own-customized-handler.md)