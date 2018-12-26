---
title: '인터넷 서버 오류: 액세스가 거부 | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- access denied error in RDS [ADO]
ms.assetid: e5b43cfa-da8d-430d-a2ab-5443dda47a16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b7c562e57341dd027a4cd9bdc3a0fa4bbe51ae5
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51558400"
---
# <a name="internet-server-error-access-denied"></a>인터넷 서버 오류: 액세스가 거부되었습니다.
이 오류가 발생할 경우에 일반적으로 Microsoft 인터넷 정보 서비스 (IIS) 다음 상태를 반환 하는 의미 합니다.  
  
 401 HTTP_STATUS_DENIED  
  
 IIS에서 액세스 한 디렉터리에 적절 한 권한이 있는지 확인 합니다. RDS는 세 가지 암호 인증 모드 중 하나로 실행 되는 IIS 웹 서버와 통신할 수: Anonymous, Basic 또는 NT Challenge/Response (Windows 2000에서 Windows 통합 인증 이라고 함). 또한 웹 서버는 Windows NT/Windows 2000 컴퓨터 하는 경우에 데이터 원본 컴퓨터에 권한이 있어야 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)




