---
title: "사용자 지정 비즈니스 개체를 등록 하는 중 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- custom business object in RDS [ADO]
- registering custom business objects in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: e9032ad8-d14c-42e3-ba13-cb5f00084a79
caps.latest.revision: "19"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c121ddf9e271f4dfb67490d77a719267cfa11a3b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="registering-a-custom-business-object"></a>사용자 지정 비즈니스 개체를 등록 하는 중
이 절차에 설명 된 대로 비즈니스 개체의 ProgID (.dll 또는.exe)에 사용자 지정 비즈니스 개체를 통해 웹 서버를 성공적으로 시작 하려면 레지스트리에 입력 해야 합니다. 이 RDS 기능 승인된 실행 파일만 실행 하 여 웹 서버의 보안을 보호 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
> [!NOTE]
>  MDAC 2.0 이상 및 Windows DAC, 기본 비즈니스 개체에 대 한 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), MDAC/Windows DAC 설치 하는 동안 기본적으로 등록 되지 않았습니다. 그러나 경우 **업데이트할** 등록를 설치 하기 전에 컴퓨터에서 실행을 위한 안전한 것으로, 레지스트리 항목이 새 설치에 유지 됩니다.  
  
### <a name="to-register-a-custom-business-object"></a>사용자 지정 비즈니스 개체를 등록 합니다.  
  
1.  클릭 **시작** 클릭 하 고 **실행**합니다.  
  
2.  형식 **RegEdit** 클릭 **확인**합니다.  
  
3.  레지스트리 편집기에서 이동 된 **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch** 레지스트리 키입니다.  
  
4.  선택 된 **ADCLaunch** 키를 한 다음는 **편집**메뉴에서 **새로** 클릭 하 고 **키**합니다.  
  
5.  사용자 지정 비즈니스 개체의 ProgID를 입력 하 고 클릭 **Enter**합니다. 유지 된 **값** 빈 항목입니다.


