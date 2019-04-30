---
title: 로그 파일 공간 사용 최소화 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- log file space in RDS [ADO]
ms.assetid: 669662a0-e20f-483e-ab28-53f66c524c98
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 061cae6b387611886943aabcfa3dfd99579a59d7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63134405"
---
# <a name="minimizing-log-file-space-usage"></a>로그 파일 공간 사용 최소화
로그 파일을 신속 하 게 채울 수 있습니다 (따라서 중단 되는 서버)는 작업량이 많은 SQL Server 데이터베이스에 없는 경우. 로그 파일을 설정할 수 있습니다 **검사점 Truncate** 현저 하 게 늘릴 데이터베이스에 대 한 로그 파일의 수명입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-65"></a>Microsoft SQL Server 6.5에서 검사점 Truncate를 사용 하도록 설정 하려면  
  
1.  Microsoft SQL Server 엔터프라이즈 관리자를 시작, 트리 서버용으로 연 다음 데이터베이스 장치 트리를 엽니다.  
  
2.  이 기능을 사용할 데이터베이스의 이름을 두 번 클릭 합니다.  
  
3.  **데이터베이스** 탭을 선택 **Truncate**합니다.  
  
4.  **옵션** 탭을 선택 **검사점에서 로그 자름**를 클릭 하 고 **확인**합니다.  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-70"></a>Microsoft SQL Server 7.0에서 검사점 Truncate를 사용 하도록 설정 하려면  
  
1.  Microsoft SQL Server 엔터프라이즈 관리자를 시작, 트리 서버용으로 연 다음 데이터베이스 트리를 엽니다.  
  
2.  이 기능은 사용할 수 있으며 선택 데이터베이스의 이름을 마우스 오른쪽 단추로 클릭 **속성**합니다.  
  
3.  **옵션** 탭을 선택 **검사점에서 로그 자름**를 클릭 하 고 **확인**합니다.  
  
 에 대 한 자세한 내용은 합니다 **검사점 Truncate** 기능, Microsoft SQL Server 설명서를 참조 하세요.  
  
## <a name="see-also"></a>관련 항목  
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)


