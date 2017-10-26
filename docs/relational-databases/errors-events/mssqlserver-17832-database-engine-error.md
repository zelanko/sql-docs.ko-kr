---
title: "MSSQLSERVER_17832 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 17828 (Database Engine error)
- maxtokensize
- 17832 (Database Engine error)
- login packet (bad)
ms.assetid: bd56ffe4-0855-4ada-8aca-251fbc6ff2ce
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 29d2c1f1af2ccd6f04c16d5152458010a5f5bc7e
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver17832"></a>MSSQLSERVER_17832
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|17832|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SRV_BAD_LOGIN_PKT|  
|메시지 텍스트|연결을 여는 데 사용한 로그인 패킷이 구조적으로 잘못되었습니다. 연결이 닫혔습니다. 클라이언트 라이브러리 공급업체에 문의하십시오.%.*ls|  
  
## <a name="explanation"></a>설명  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에서 클라이언트 로그인 패킷을 처리하지 못했습니다. 이 문제는 패킷이 잘못 만들어졌거나 전송 중에 손상되었기 때문에 발생할 수 있습니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터의 구성 때문에 이 문제가 발생할 수도 있습니다. 나열된 IP 주소는 클라이언트 컴퓨터의 주소입니다.  
  
### <a name="more-information"></a>추가 정보  
Kerberos 환경에서 Windows 인증을 사용할 경우 클라이언트는 PAC(Privilege Attribute Certificate)가 포함된 Kerberos 티켓을 수신합니다. PAC에는 사용자가 속한 그룹, 사용자가 가지고 있는 권한, 사용자에게 적용되는 정책 등 다양한 유형의 인증 데이터가 포함되어 있습니다. 클라이언트가 Kerberos 티켓을 수신하면 PAC에 포함된 정보가 사용자의 액세스 토큰을 만드는 데 사용됩니다. 클라이언트는 이 토큰을 로그인 패킷의 일부로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 제공합니다.  
  
패킷이 잘못 만들어졌거나 전송 중에 손상된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 문제에 대한 추가 정보를 제공할 수 없습니다.  
  
사용자가 여러 그룹의 멤버이거나 많은 정책을 사용하는 경우 이러한 것들을 모두 나열하기 위해 토큰이 정상보다 커질 수 있습니다. 토큰이 서버 컴퓨터의 **MaxTokenSize** 값보다 커질 경우 클라이언트가 GNE(일반 네트워크 오류)에 연결하지 못하고 오류 17832가 발생할 수 있습니다. 이 문제는 그룹이나 정책이 많은 일부 사용자에게만 영향을 줄 수 있습니다. 서버 컴퓨터의 **MaxTokenSize** 값에 문제가 있을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그의 오류 17832와 함께 상태가 9인 오류가 표시됩니다. Kerberos 및 **MaxTokenSize**에 대한 자세한 내용은 [KB327825](http://support.microsoft.com/kb/327825)를 참조하세요.  
  
## <a name="user-action"></a>사용자 동작  
이 문제를 해결하려면 서버 컴퓨터의 **MaxTokenSize** 값을 조직에 있는 모든 사용자의 토큰 중 가장 큰 토큰을 포함할 수 있는 충분한 크기로 늘립니다. 조직에 맞는 올바른 토큰 크기를 조사하려면 **Tokensz** 응용 프로그램을 사용합니다.  
  
> [!CAUTION]  
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
**서버 컴퓨터에서 MaxTokenSize** **를 변경하려면**  
  
1.  **시작** 메뉴에서 **실행**을 클릭합니다.  
  
2.  **regedit**를 입력한 다음 **확인**을 클릭합니다. **사용자 계정 컨트롤** 대화 상자가 열리면 **계속**을 클릭합니다.  
  
3.  **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa\Kerberos\Parameters**로 이동합니다.  
  
4.  **MaxTokenSize** 매개 변수가 없으면 **Parameters**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **DWORD(32비트) 값**을 클릭합니다. 이 레지스트리 항목의 이름을 **MaxTokenSize**로 지정합니다.  
  
5.  **MaxTokenSize**를 마우스 오른쪽 단추를 클릭한 다음 **수정**을 클릭합니다.  
  
6.  **값 데이터** 상자에 원하는 **MaxTokenSize** 값을 입력합니다.  
  
    > [!NOTE]  
    > 권장되는 최대 토큰 크기는 16진수 값 ffff(10진수 값 65535)입니다. 이 값을 제공하면 문제가 해결될 수도 있지만 컴퓨터 성능이 저하될 수 있습니다. 조직에 있는 모든 사용자의 토큰 중 가장 큰 토큰을 허용하는 최소 **MaxTokenSize** 값을 설정하고 이 값을 입력하는 것이 좋습니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  **레지스트리 편집기**를 닫습니다.  
  
9. 컴퓨터를 다시 시작합니다.  
  

