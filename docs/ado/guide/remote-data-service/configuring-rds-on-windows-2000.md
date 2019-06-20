---
title: Windows 2000에서 RDS 구성 | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: a17ed52371a6c7eae057332a3e80bd215131d287
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704342"
---
# <a name="configuring-rds-on-windows-2000"></a>Windows 2000에서 RDS 구성
Windows 2000으로 업그레이드 한 후 제대로 작동 하려면 RDS를 시작 하는 문제를 발생 하면 문제를 해결 하려면 다음이 단계를 수행 합니다.  
  
1.  Internet Explorer를 사용 하 여 https:// 서버로 이동 하 여 World Wide Web Publishing 서비스가 첫 번째 실행 중인지 확인 합니다. 이 방식으로 웹 서버에 액세스할 수 없는 경우 명령 프롬프트를 열고 "NET START W3SVC" 다음 명령을 입력 합니다.  
  
2.  시작 메뉴의 실행을 선택 합니다. Msdfmap.ini 형식과 msdfmap.ini 파일을 메모장에서 열려면 확인을 클릭 합니다. [기본값 연결] 섹션을 확인 하 고 액세스 매개 변수 액세스 권한 없음으로 설정 된 경우 디스크 캐싱을 READONLY로 변경 합니다.  
  
3.  "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DataFactory\HandlerInfo"로 이동 하 고 있는지 확인 RegEdit 유틸리티를 사용 하 **HandlerRequired** 은 0으로 설정 하 고 **DefaultHandler** 은 "" (Null 문자열).  
  
     **참고** 이 섹션에서는 레지스트리를 변경한 경우 중지 하 고 명령 프롬프트에서 다음 명령을 입력 하 여 World Wide Web Publishing 서비스를 다시 시작 해야 합니다. "NET STOP W3SVC" 및 "NET START W3SVC"입니다.  
  
4.  "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch" 레지스트리의 이동한 라는 키 임을 확인 RegEdit 유틸리티를 사용 하 **업데이트할**합니다. 그렇지 않은 경우 만듭니다.  
  
5.  기본 웹 사이트를 찾아 MSADC 가상 루트의 속성을 보려면 인터넷 서비스 관리자를 사용 합니다. 디렉터리 보안/IP 주소 및 도메인 이름 제한을 검사 합니다. "액세스가 거부 되었습니다"을 선택 하는 경우에 "Granted"를 선택 합니다.  
  
 서버를 다시 부팅 하는 경우 해야 변경 내용이 처음에 문제를 해결 하는 표시 되지 않습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다. Windows 8 및 Windows Server 2012 부터는 Windows 운영 체제에서 RDS 서버 구성 요소는 더 이상 포함 된 합니다. RDS를 사용 하는 응용 프로그램을 마이그레이션할 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)


