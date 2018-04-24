---
title: 로그 파일 공간 사용을 최소화 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- log file space in RDS [ADO]
ms.assetid: 669662a0-e20f-483e-ab28-53f66c524c98
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b333875afe103eb0438b567666e54c9985c51997
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="minimizing-log-file-space-usage"></a>로그 파일 공간 사용을 최소화합니다.
로그 파일을 빠르게 채울 수 있습니다 (따라서 서버 중지) SQL Server 데이터베이스에 볼륨이 큰 경우. 로그 파일 설정할 수 있습니다 **검사점에서 Truncate** 현저 하 게 늘릴 데이터베이스에 대 한 로그 파일의 수명을 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-65"></a>Truncate Microsoft SQL Server 6.5에서 검사점을 사용 하도록 설정 하려면  
  
1.  Microsoft SQL Server 엔터프라이즈 관리자를 시작, 트리는 서버에 대 한 연 다음 데이터베이스 장치 트리를 엽니다.  
  
2.  이 기능을 설정할 데이터베이스의 이름을 두 번 클릭 합니다.  
  
3.  **데이터베이스** 탭에서 **Truncate**합니다.  
  
4.  **옵션** 탭에서 **Truncate 로그온 검사점**, 클릭 하 고 **확인**합니다.  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-70"></a>Truncate에 Microsoft SQL Server 7.0에서 검사점을 사용 하도록 설정 하려면  
  
1.  Microsoft SQL Server 엔터프라이즈 관리자를 시작한 서버에 대 한 트리를 열고 데이터베이스 트리를 엽니다.  
  
2.  이 기능은 사용할 수 있으며 선택한 데이터베이스의 이름을 마우스 오른쪽 단추로 클릭 **속성**합니다.  
  
3.  **옵션** 탭에서 **Truncate 로그온 검사점**, 클릭 하 고 **확인**합니다.  
  
 에 대 한 자세한 내용은 **검사점에서 Truncate** 기능, Microsoft SQL Server 설명서를 참조 하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)


