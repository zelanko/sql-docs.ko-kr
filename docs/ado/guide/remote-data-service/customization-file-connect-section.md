---
description: 사용자 지정 파일 연결 섹션
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a8c712efc368d9b84158697d3b7e6eedfb4224ff
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759849"
---
# <a name="customization-file-connect-section"></a>사용자 지정 파일 연결 섹션
처리기의 기본 동작은 모든 연결을 거부 하는 것입니다. **Connect** 섹션에서는 해당 동작에 대 한 예외를 지정 합니다. 예를 들어 모든 **connect** 섹션이 없거나 비어 있는 경우 기본적으로 연결을 설정할 수 없습니다.  
  
 **Connect** 섹션에는 다음이 포함 될 수 있습니다.  
  
-   이 연결에서 허용 되는 기본 읽기 및 쓰기 작업을 지정 하는 기본 액세스 항목입니다. 섹션에 기본 액세스 항목이 없으면 섹션은 무시 됩니다.  
  
-   클라이언트 연결 문자열을 대체 하는 새 연결 문자열입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
 기본 액세스 항목의 형식은 다음과 같습니다.  
  
```console
  
Access=  
accessRight  
  
```  
  
 대체 연결 문자열 항목의 형식은 다음과 같습니다.  
  
```console
  
Connect=  
connectionString  
  
```  
  
## <a name="remarks"></a>설명  
  
|부분|설명|  
|----------|-----------------|  
|**연결**|연결 문자열 항목 임을 나타내는 리터럴 문자열입니다.|  
|**_connectionString_**|전체 클라이언트 연결 문자열을 대체 하는 문자열입니다.|  
|**Access**|이 항목이 액세스 항목 임을 나타내는 리터럴 문자열입니다.|  
|**_accessRight_**|다음 액세스 권한 중 하나입니다.<br /><br /> -   **NoAccess** -사용자가 데이터 원본에 액세스할 수 없습니다.<br />-   **ReadOnly** -사용자가 데이터 소스를 읽을 수 있습니다.<br />-   **ReadWrite** -사용자가 데이터 소스를 읽거나 쓸 수 있습니다.|  
  
 기본 처리기 동작을 사용 하지 않도록 설정 하 여 모든 연결을 허용 하려는 경우 **기본값 연결** 섹션에서 액세스 항목을로 설정 하 `Access=ReadWrite` 고 다른 모든 **연결** _식별자_ 섹션을 삭제 하거나 주석으로 처리 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [사용자 지정 파일 로그 섹션](./customization-file-logs-section.md)   
 [사용자 지정 파일 SQL 섹션](./customization-file-sql-section.md)   
 [사용자 지정 파일 UserList 섹션](./customization-file-userlist-section.md)   
 [DataFactory 사용자 지정](./datafactory-customization.md)   
 [필수 클라이언트 설정](./required-client-settings.md)   
 [사용자 지정 파일 이해](./understanding-the-customization-file.md)   
 [고유한 사용자 지정된 처리기 작성](./writing-your-own-customized-handler.md)