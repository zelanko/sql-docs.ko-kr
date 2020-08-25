---
description: 사용자 지정 파일 로그 섹션
title: 사용자 지정 파일 로그 섹션 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- logs section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: a368e264-865c-41ee-be00-d9097255c2ea
author: rothja
ms.author: jroth
ms.openlocfilehash: f478a1e1c18e9182d2effe77d37c0c329ba22c54
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759837"
---
# <a name="customization-file-logs-section"></a>사용자 지정 파일 로그 섹션
**Logs** 섹션에는 **DataFactory**작업 중에 오류를 기록 하는 파일의 이름을 지정 하는 로그 파일 항목이 포함 되어 있습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
 로그 파일 항목의 형식은 다음과 같습니다.  
  
```console
  
err=  
FileName  
  
```  
  
## <a name="remarks"></a>설명  
  
|부분|설명|  
|----------|-----------------|  
|**err**|로그 파일 항목 임을 나타내는 리터럴 문자열입니다.|  
|*FileName*|전체 경로 및 파일 이름입니다. 일반적인 파일 이름은 **c:\msdfmap.log**입니다.|  
  
 로그 파일에는 각 오류의 사용자 이름, HRESULT, 날짜 및 시간이 포함 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [사용자 지정 파일 연결 섹션](./customization-file-connect-section.md)   
 [사용자 지정 파일 SQL 섹션](./customization-file-sql-section.md)   
 [사용자 지정 파일 UserList 섹션](./customization-file-userlist-section.md)   
 [DataFactory 사용자 지정](./datafactory-customization.md)   
 [필수 클라이언트 설정](./required-client-settings.md)   
 [사용자 지정 파일 이해](./understanding-the-customization-file.md)   
 [고유한 사용자 지정된 처리기 작성](./writing-your-own-customized-handler.md)