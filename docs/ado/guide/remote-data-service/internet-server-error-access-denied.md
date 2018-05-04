---
title: '인터넷 서버 오류: 액세스가 거부 되었습니다. | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- access denied error in RDS [ADO]
ms.assetid: e5b43cfa-da8d-430d-a2ab-5443dda47a16
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34850832da71e66fffb751f0725d8f6f78ac18b6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="internet-server-error-access-denied"></a>인터넷 서버 오류: 액세스가 거부 되었습니다.
이 오류가 발생할 경우에 일반적으로 Microsoft 인터넷 정보 서비스 (IIS) 다음과 같은 상태를 반환 했음을 의미 합니다.  
  
 HTTP_STATUS_DENIED 401  
  
 IIS에서 액세스 한 디렉터리에 적절 한 권한이 있는지 확인 합니다. RDS 세 가지 암호 인증 모드 중 하나에서 실행 하는 IIS 웹 서버와 통신할 수: 익명, 기본 또는 NT Challenge/Response (Windows 2000에서 Windows 통합 인증 이라고 함). 또한 웹 서버 Windows Windows NT/2000 컴퓨터인 경우에 데이터 원본 컴퓨터에 권한이 있어야 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)




