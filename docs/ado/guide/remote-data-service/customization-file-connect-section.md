---
title: 사용자 지정 파일 연결 섹션 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connect section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: d50eb3cc-a822-486f-b80b-65bb50547ecd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c9ec47ffb89724e8a7991dae1d2296aa813e0c5e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704316"
---
# <a name="customization-file-connect-section"></a>사용자 지정 파일 연결 섹션
처리기의 기본 동작은 모든 연결을 거부 합니다. 합니다 **연결** 섹션에서는 해당 동작에 대 한 예외를 지정 합니다. 예를 들어, 모든 경우는 **연결** 없거나 비어 있는 경우 섹션 된 다음 기본적으로 없습니다 연결을 만들 수 없습니다.  
  
 합니다 **연결** 섹션에 포함 될 수 있습니다.  
  
-   기본값을 지정 하는 기본 액세스 항목을이 연결에서 허용 되는 작업을 읽고 설정 합니다. 섹션에서 기본 액세스 항목이 없는 경우 섹션 무시 됩니다.  
  
-   클라이언트 연결 문자열을 대체 하는 새 연결 문자열입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
 기본 액세스 항목을 폼입니다.  
  
```console
  
Access=  
accessRight  
  
```  
  
 대체 연결 문자열 항목은 다음과 폼입니다.  
  
```console
  
Connect=  
connectionString  
  
```  
  
## <a name="remarks"></a>Remarks  
  
|부분|설명|  
|----------|-----------------|  
|**연결**|이 나타내는 리터럴 문자열은 연결 문자열 입력입니다.|  
|**_connectionString_**|전체 클라이언트 연결 문자열을 대체 하는 문자열입니다.|  
|**액세스 권한**|이 나타내는 리터럴 문자열에 대 한 액세스 항목입니다.|  
|**_accessRight_**|다음 액세스 권한 중 하나입니다.<br /><br /> -   **액세스 권한 없음** -사용자 데이터 원본에 액세스할 수 없습니다.<br />-   **읽기 전용** -사용자는 데이터 소스를 읽을 수 있습니다.<br />-   **ReadWrite** -사용자 읽기 또는 데이터 원본에 쓸 수 있습니다.|  
  
 (기본 처리기 동작을 사용 하지 않도록 설정 적용)에서 모든 연결을 허용 하려는 경우에서 액세스 항목을 설정 합니다 **기본 연결** 섹션을 `Access=ReadWrite`, 및 삭제 하거나 다른 주석 **연결** _식별자_ 섹션입니다.  
  
## <a name="see-also"></a>관련 항목  
 [사용자 지정 파일 로그 섹션](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [사용자 지정 파일 SQL 섹션](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [사용자 지정 파일 UserList 섹션](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 사용자 지정](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [필수 클라이언트 설정](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [사용자 지정 파일 이해](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [고유한 사용자 지정된 처리기 작성](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



