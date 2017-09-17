---
title: "IIS에서 가상 서버 구성 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- virtual servers in RDS [ADO]
ms.assetid: 2b4786c6-40c4-4ce1-9ad4-03df436e0aff
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 10edd98f77c0aaeae05d25e76ad76a15b99bc1ed
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="configuring-virtual-servers-on-iis"></a>IIS에서 가상 서버를 구성합니다.
인터넷 정보 서비스 4.0에서 가상 서버를 만들 때 다음 두 가지 추가 단계 RDS를 사용 하도록 가상 서버를 구성 하는 데 필요 합니다.  
  
1.  서버를 설정할 때 확인 "Execute 액세스 허용 합니다."  
  
2.  탭 이동 *vroot*\msadc, 여기서 *vroot* 홈 디렉터리 가상 서버입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)



