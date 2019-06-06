---
title: 사용자 지정 파일 UserList 섹션 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- UserList section in rds [ADO]
- customization file in RDS [ADO]
ms.assetid: 42e8ec20-eaac-4a95-8cb8-4bba93a75bcb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e38b253cdebcc5ab976de8c8eb355f7f6fb03aec
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66699536"
---
# <a name="customization-file-userlist-section"></a>사용자 지정 파일 UserList 섹션
**userlist** 관련 된 섹션의 **연결** 의 동일한 영역 *식별자* 매개 변수입니다.  
  
 이 섹션에 포함 될 수는 *사용자 액세스 항목*, 재정의 및 지정된 된 사용자에 대 한 대 한 액세스를 지정 하는 합니다 *기본* *항목에 액세스할* 에서 일치 하는 **연결** 섹션입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
 사용자 액세스 항목을 폼입니다.  
  
 _userName_ **=**    
 **_accessRights_**  
  
|부분|설명|  
|----------|-----------------|  
|*userName*|합니다 *사용자 이름* 이 연결을 사용 하는 사용자입니다. IIS를 사용 하 여 올바른 사용자 이름이 설정 됩니다 **Service Manager** 대화 합니다.|  
|**_accessRights_**|다음 액세스 권한 중 하나입니다.<br /><br /> -   **액세스 권한 없음** -사용자 데이터 원본에 액세스할 수 없습니다.<br />-   **읽기 전용** -사용자는 데이터 소스를 읽을 수 있습니다.<br />-   **ReadWrite** -사용자 읽기 또는 데이터 원본에 쓸 수 있습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [사용자 지정 파일 연결 섹션](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [사용자 지정 파일 로그 섹션](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [사용자 지정 파일 SQL 섹션](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [DataFactory 사용자 지정](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [필수 클라이언트 설정](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [사용자 지정 파일 이해](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [고유한 사용자 지정된 처리기 작성](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


