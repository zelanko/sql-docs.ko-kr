---
title: "사용자 지정 파일 연결 섹션 | Microsoft Docs"
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
- connect section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: d50eb3cc-a822-486f-b80b-65bb50547ecd
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d6ec65ea217935e007427a087f2a05162649f226
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="customization-file-connect-section"></a>사용자 지정 파일 연결 섹션
처리기의 기본 동작은 모든 연결을 거부 하는 것입니다. **연결** 섹션 해당 동작에 대 한 예외를 지정 합니다. 예를 들어 모든는 **연결** 섹션 된 absent 이거나 비어 있는 경우 다음 기본적으로 없습니다 연결을 만들 수 없습니다.  
  
 **연결** 섹션에 포함 될 수 있습니다.  
  
-   기본값을 지정 하는 기본 액세스 항목 읽기 및 쓰기이 연결에 허용 되는 작업입니다. 섹션의 섹션에서 기본 액세스 항목이 없는 경우 무시 됩니다.  
  
-   클라이언트 연결 문자열을 대체 하는 새 연결 문자열입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
 기본 액세스 항목 형식입니다.  
  
```  
  
Access=  
accessRight  
  
```  
  
 대체 연결 문자열 항목 형식입니다.  
  
```  
  
Connect=  
connectionString  
  
```  
  
## <a name="remarks"></a>주의  
  
|부분|Description|  
|----------|-----------------|  
|**연결**|이 설정에 리터럴 문자열은 연결 문자열 항목입니다.|  
|***연결 문자열***|전체 클라이언트 연결 문자열을 대체 하는 문자열입니다.|  
|**액세스 권한**|이 나타내는 리터럴 문자열에 대 한 액세스 항목입니다.|  
|***accessRight***|다음 액세스 권한 중 하나입니다.<br /><br /> -   **액세스 권한 없음** -사용자 데이터 원본에 액세스할 수 없습니다.<br />-   **읽기 전용** -사용자는 데이터 소스를 읽을 수 있습니다.<br />-   **ReadWrite** -사용자 읽기 또는 데이터 원본에 쓸 수 있습니다.|  
  
 (효과 기본 처리기 동작을 사용 하지 않도록 설정)의 모든 연결을 허용 하려는 경우 액세스 항목에 설정 된 **기본 연결** 섹션을 `Access=ReadWrite`, 삭제 하거나 다른 주석 및 **연결** *식별자* 섹션.  
  
## <a name="see-also"></a>관련 항목:  
 [사용자 지정 파일 로그 섹션](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [사용자 지정 파일 SQL 섹션](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [사용자 지정 파일 UserList 섹션](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 사용자 지정](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [필요한 클라이언트 설정](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [사용자 지정 파일 이해](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [고유한 사용자 지정된 처리기 작성](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)




