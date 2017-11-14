---
title: "사용자 지정 파일 기록 섹션 | Microsoft Docs"
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
- logs section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: a368e264-865c-41ee-be00-d9097255c2ea
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 99d22cd98548548463f1cbd5516d26faaf4b9bf1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="customization-file-logs-section"></a>사용자 지정 파일 로그 섹션
**로그** 섹션의 작업 중 오류를 기록 하는 파일의 이름을 지정 하는 로그 파일 항목에 포함 되어는 **DataFactory**합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
 로그 파일 항목은 양식입니다.  
  
```  
  
err=  
FileName  
  
```  
  
## <a name="remarks"></a>주의  
  
|부분|Description|  
|----------|-----------------|  
|**오류**|이 설정에 리터럴 문자열은 로그 파일 항목입니다.|  
|*FileName*|전체 경로 및 파일 이름입니다. 일반적인 파일 이름은 **c:\msdfmap.log**합니다.|  
  
 로그 파일에는 사용자 이름, HRESULT, 날짜 및 시간 각 오류의 포함 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [사용자 지정 파일 연결 섹션](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [사용자 지정 파일 SQL 섹션](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [사용자 지정 파일 UserList 섹션](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 사용자 지정](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [필요한 클라이언트 설정](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [사용자 지정 파일 이해](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [고유한 사용자 지정된 처리기 작성](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



