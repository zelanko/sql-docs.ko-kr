---
description: 사용자 지정 파일 UserList 섹션
title: 사용자 지정 파일 UserList 섹션 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- UserList section in rds [ADO]
- customization file in RDS [ADO]
ms.assetid: 42e8ec20-eaac-4a95-8cb8-4bba93a75bcb
author: rothja
ms.author: jroth
ms.openlocfilehash: b09e5f9356ad196e03c970623369d4918a6f5506
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724754"
---
# <a name="customization-file-userlist-section"></a>사용자 지정 파일 UserList 섹션
**Userlist** 섹션은 동일한 section *식별자* 매개 변수를 사용 하는 **connect** 섹션과 관련이 있습니다.  
  
 이 섹션에는 지정 된 사용자에 대 한 액세스 권한을 지정 하 고 일치 하는 **연결** 섹션의 *기본* *액세스 항목* 을 재정의 하는 *사용자 액세스 항목이*포함 될 수 있습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](/dotnet/framework/wcf/)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
 사용자 액세스 항목의 형식은 다음과 같습니다.  
  
 _사용자 이름_**=**   
 **_accessRights_**  
  
|부분|Description|  
|----------|-----------------|  
|*userName*|이 연결을 사용 하는 *사용자의 사용자 이름* 입니다. 올바른 사용자 이름은 IIS **Service Manager** 대화 상자를 사용 하 여 설정 됩니다.|  
|**_accessRights_**|다음 액세스 권한 중 하나입니다.<br /><br /> -   **NoAccess** -사용자가 데이터 원본에 액세스할 수 없습니다.<br />-   **ReadOnly** -사용자가 데이터 소스를 읽을 수 있습니다.<br />-   **ReadWrite** -사용자가 데이터 소스를 읽거나 쓸 수 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [사용자 지정 파일 연결 섹션](./customization-file-connect-section.md)   
 [사용자 지정 파일 로그 섹션](./customization-file-logs-section.md)   
 [사용자 지정 파일 SQL 섹션](./customization-file-sql-section.md)   
 [DataFactory 사용자 지정](./datafactory-customization.md)   
 [필수 클라이언트 설정](./required-client-settings.md)   
 [사용자 지정 파일 이해](./understanding-the-customization-file.md)   
 [고유한 사용자 지정된 처리기 작성](./writing-your-own-customized-handler.md)