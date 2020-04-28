---
title: Windows에서 RDS 구성 2000 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS configuration [ADO], Windows 2000
ms.assetid: ef37e858-c05f-4f52-a65f-3ce6037e0d03
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6230fb7ffbaa1226bc65d391d988ad064617998
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67922892"
---
# <a name="configuring-rds-on-windows-2000"></a>Windows 2000에서 RDS 구성
Windows 2000로 업그레이드 한 후 RDS가 제대로 작동 하는 데 문제가 발생 하는 경우 다음 단계에 따라 문제를 해결 합니다.  
  
1.  Internet Explorer를 사용 하 여 https://server로 이동 하 여 World Wide Web Publishing 서비스가 먼저 실행 되 고 있는지 확인 합니다. 이런 방식으로 웹 서버에 액세스할 수 없는 경우 명령 프롬프트를 열고 다음 명령을 "NET START W3SVC" 명령을 입력 합니다.  
  
2.  시작 메뉴에서 실행을 선택 합니다. Msdfmap .ini를 입력 한 다음 확인을 클릭 하 여 메모장에서 msdfmap. n a n 파일을 엽니다. [기본값 연결] 섹션을 선택 하 고 ACCESS 매개 변수가 NOACCESS로 설정 되어 있는 경우 READONLY로 변경 합니다.  
  
3.  RegEdit 유틸리티를 사용 하 여 "HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\DataFactory\HandlerInfo"으로 이동 하 고, **Handlerrequired** 가 0으로 설정 되 고 **defaulthandler** 가 "" (Null 문자열)로 설정 되어 있는지 확인 합니다.  
  
     **참고** 레지스트리의이 섹션을 변경 하는 경우 명령 프롬프트에서 "NET STOP W3SVC" 및 "NET START W3SVC" 명령을 입력 하 여 World Wide Web Publishing 서비스를 중지 했다가 다시 시작 해야 합니다.  
  
4.  RegEdit 유틸리티를 사용 하 여 레지스트리에서 "HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch"로 이동 하 고 **RDSServer Datafactory**라는 키가 있는지 확인 합니다. 그렇지 않은 경우 만듭니다.  
  
5.  인터넷 서비스 관리자를 사용 하 여 기본 웹 사이트를 찾아 MSADC 가상 루트의 속성을 봅니다. 디렉터리 보안/i p 주소 및 도메인 이름 제한을 검사 합니다. "액세스가 거부 되었습니다."가 선택 된 경우 "부여 됨"을 선택 합니다.  
  
 에 대 한 변경 내용이 표시 되지 않는 경우에는 서버를 다시 부팅 하 여 문제를 먼저 해결 해야 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다. Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다. RDS를 사용 하는 응용 프로그램을 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션합니다.  
  
## <a name="see-also"></a>참고 항목  
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)


