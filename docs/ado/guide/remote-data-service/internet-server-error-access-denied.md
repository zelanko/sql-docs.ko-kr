---
description: '인터넷 서버 오류: 액세스가 거부되었습니다.'
title: '인터넷 서버 오류: 액세스가 거부 되었습니다. Microsoft Docs'
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8daeb97bd4bcb8a01556f6ece38e977f1cf0068f
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759744"
---
# <a name="internet-server-error-access-denied"></a>인터넷 서버 오류: 액세스가 거부되었습니다.
이 오류가 발생 하는 경우 일반적으로 Microsoft 인터넷 정보 서비스 (IIS)에서 다음 상태를 반환 했음을 의미 합니다.  
  
 HTTP_STATUS_DENIED 401  
  
 IIS에서 액세스 하는 디렉터리에 적절 한 사용 권한이 있는지 확인 합니다. RDS는 세 가지 암호 인증 모드인 익명, 기본 또는 NT 챌린지/Response (Windows 2000의 windows 통합 인증 이라고 함) 중 하나에서 실행 되는 IIS 웹 서버와 통신할 수 있습니다. 또한 Windows NT/Windows 2000 컴퓨터인 경우에는 웹 서버에 데이터 원본 컴퓨터에 대 한 사용 권한이 있어야 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [RDS 기본 사항](./rds-fundamentals.md)