---
description: IIS에서 가상 서버 구성
title: IIS에서 가상 서버 구성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- virtual servers in RDS [ADO]
ms.assetid: 2b4786c6-40c4-4ce1-9ad4-03df436e0aff
author: rothja
ms.author: jroth
ms.openlocfilehash: 53d22155f8e7af894419a28ddf01bf3fe80e34f3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978284"
---
# <a name="configuring-virtual-servers-on-iis"></a>IIS에서 가상 서버 구성
인터넷 정보 서비스 4.0에서 가상 서버를 만들 때 다음 두 가지 추가 단계를 수행 하 여 RDS와 작동 하도록 virtual server를 구성 합니다.  
  
1.  서버를 설정 하는 경우 "실행 액세스 허용"을 선택 합니다.  
  
2.  msadcs.dll를 *vroot*\msadc로 이동 합니다. 여기서 *vroot* 는 가상 서버의 홈 디렉터리입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [RDS 기본 사항](./rds-fundamentals.md)