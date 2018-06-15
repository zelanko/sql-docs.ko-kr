---
title: Windows 2000에서 RDS 구성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS configuration [ADO], Windows 2000
ms.assetid: ef37e858-c05f-4f52-a65f-3ce6037e0d03
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 774309f4b120f3c475645574429d1b08af627f8b
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35273772"
---
# <a name="configuring-rds-on-windows-2000"></a>Windows 2000에서 RDS를 구성합니다.
Windows 2000으로 업그레이드 한 후 올바르게 작동 하려면 RDS를 시작 하는 데 문제가 발생 하는 경우 문제를 해결 하려면 다음이 단계를 수행 합니다.  
  
1.  Internet Explorer를 사용 하 여 http:// 서버로 이동 하 여 World Wide Web Publishing 서비스에서 첫 번째 실행 중인지 확인 합니다. 이런이 방식으로 웹 서버에 액세스할 수 없는 경우 명령 프롬프트 열고 "NET START W3SVC" 하 여 다음 명령을 입력 합니다.  
  
2.  시작 메뉴에서 실행을 선택 합니다. Msdfmap.ini를 입력 하 고 확인 msdfmap.ini 파일을 메모장에서 열을 클릭 합니다. [연결 기본] 섹션을 확인 하 고 액세스 권한 없음에 대 한 액세스 매개 변수를 설정, READONLY로 변경 합니다.  
  
3.  RegEdit 유틸리티를 사용 하 여 "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DataFactory\HandlerInfo"로 이동 하 고 있는지 확인 **HandlerRequired** 0으로 설정 하 고 **DefaultHandler** 은 "" (Null 문자열)입니다.  
  
     **참고** 중지 하 고 명령 프롬프트에서 다음 명령을 입력 하 여 World Wide Web Publishing 서비스를 다시 시작 해야이 섹션의 레지스트리를 변경 하는 변경 내용이: "NET 중지 W3SVC" 및 "NET START W3SVC"입니다.  
  
4.  "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch"를 레지스트리에서 이동한 라는 키 임을 확인 RegEdit 유틸리티를 사용 하 여 **업데이트할**합니다. 그렇지 않은 경우 만듭니다.  
  
5.  인터넷 서비스 관리자를 사용 하 여 기본 웹 사이트 찾아 MSADC 가상 루트의 속성을 봅니다. 디렉터리 보안/IP 주소 및 도메인 이름 제한을 검사 합니다. "액세스가 거부 되었습니다"을 선택 하는 경우에 "Granted"를 선택 합니다.  
  
 서버를 다시 부팅 하는 경우 반드시 변경 하려면 처음에 문제 해결을 위해 표시 되지 않습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다. Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상에 포함 Windows 운영 체제. RDS를 사용 하 여 응용 프로그램을 마이그레이션할 [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)


