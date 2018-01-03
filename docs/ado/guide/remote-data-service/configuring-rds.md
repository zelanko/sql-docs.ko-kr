---
title: "RDS 구성 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: RDS configuration [ADO]
ms.assetid: 5dd48483-858a-48c2-98ce-f2359abe1f59
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fe82435c8d8a2d1c1f577a8190fabe60192dd351
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="configuring-rds"></a>RDS 구성
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 RDS를 효율적으로 구현 하 게 사용할 수 있는 다양 한 구성에 잘 알고 있다면 해야 합니다. 이 섹션 rds. 구현에 보안 및 확장성에 대 한 중요 한 정보를 포함합니다. Rds. 사용 하도록 컴퓨터를 구성 하는 방법에 대 한 내용은 다음 항목을 참조 하십시오  
  
-   [웹 서버 컴퓨터에 게스트 권한 부여](../../../ado/guide/remote-data-service/granting-guest-privileges-to-a-web-server-computer.md)  
  
-   [사용자 지정 비즈니스 개체 등록](../../../ado/guide/remote-data-service/registering-a-custom-business-object.md)  
  
-   [비즈니스 개체를 스크립팅하기에 안전하다고 표시합니다.](../../../ado/guide/remote-data-service/marking-business-objects-as-safe-for-scripting.md)  
  
-   [DCOM에서 사용할 클라이언트에서 비즈니스 개체 등록](../../../ado/guide/remote-data-service/registering-business-objects-on-the-client-for-use-with-dcom.md)  
  
-   [DCOM 스트림 마샬링 형식 설정](../../../ado/guide/remote-data-service/setting-dcom-stream-marshaling-format.md)  
  
-   [DCOM에서 실행하도록 DLL 사용](../../../ado/guide/remote-data-service/enabling-a-dll-to-run-on-dcom.md)  
  
-   [IIS에서 가상 서버 구성](../../../ado/guide/remote-data-service/configuring-virtual-servers-on-iis.md)  
  
-   [RDS 응용 프로그램 보안](../../../ado/guide/remote-data-service/securing-rds-applications.md)  
  
-   [안전 또는 무제한 모드에 대한 DataFactory 구성](../../../ado/guide/remote-data-service/configuring-datafactory-for-safe-or-unrestricted-modes.md)  
  
## <a name="see-also"></a>관련 항목:  
 [관련된 기술 RDS를 사용 하 여](../../../ado/guide/remote-data-service/using-related-technologies-with-rds.md)   
 [DataFactory 사용자 지정](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [RDS 문제 해결](../../../ado/guide/remote-data-service/troubleshooting-rds.md)


