---
title: 프로 비전 인증서 Analytics Platform System | Microsoft Docs
description: Analytics Platform System에 프로 비전 인증서입니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0da49afe13ab0f8cc92e8dd58e78f40564ff53c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960225"
---
# <a name="certificate-provisioning-in-analytics-platform-system"></a>Analytics Platform System에 프로 비전 인증서
합니다 **PDW 인증서 프로 비전** Analytics Platform System의 페이지**Configuration Manager** 가져옵니다 또는 PDW에서 사용 된 인증서를 제거 합니다. 

를 사용 하 여 연결을 암호화 하려면 인증서 수 통신 보호 도움말 SQL Server 클라이언트, SQL Server PDW 드라이버를 사용 하는 도구를 통해 제어 노드에 [관리 콘솔](monitor-the-appliance-by-using-the-admin-console.md), Integration Services를 로드 합니다. 
  
## <a name="prerequisites"></a>사전 요구 사항  
인증서를 설치 하기 전에 다음을 수행 합니다.  
  
1.  보안 인증서를 가져옵니다. 에 보안 인증서를 얻는 방법에 대 한 자세한 정보가 필요한 경우 Microsoft 지원에 문의 합니다.  
  
2.  암호로 보호 된 PFX 파일에 제어 노드에 인증서를 저장 합니다.  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>보안상의 이유로 신뢰할 수 있는 인증서 가져오기  
SQL Server PDW에서는 인증서를 사용 하 여 제어 노드에;에 대 한 연결 암호화 에 대 한 연결을 포함 하는 **관리 콘솔**합니다.  
  
기본적으로 **관리 콘솔** 개인 정보 보호 하지 않습니다 서버를 제공 하는 자체 서명 된 인증서를 포함 합니다. 이 상태로 통신 중간자 개입 공격에 취약 합니다. 사용자가 자체 서명 된 인증서를 사용 하 여 관리 콘솔에 연결 하는 경우 Internet Explorer 오류를 반환 합니다. "이 웹이 사이트의 보안 인증서에 문제가 있습니다".  
  
자체 서명 된 인증서를 통한 연결이 클라이언트와 서버 간에 진행 중인 데이터를 암호화 하지만 공격자 로부터 위험이 여전히 연결이입니다.  
  
> [!WARNING]  
> 어플라이언스 관리자는 인증서 보안에 연결 하 고 Internet Explorer를 보고 하는 오류를 제거 하기 위해 클라이언트에서 인식 하는 신뢰할 수 있는 인증 기관에 연결 된 획득 즉시 해야 합니다.  
  
제어 노드 (권장) 하는 클러스터 IP 주소에 매핑되는 정규화 된 도메인 이름 또는 사용자에 액세스 하려면 해당 브라우저 주소 표시줄에 입력 하는 이름을 인증 경로 있어야 합니다 **관리 콘솔**합니다.  
  
Analytics Platform System을 사용 하 여**Configuration Manager** 를 추가 하 여 신뢰할 수 있는 인증서를 제거 합니다. Microsoft Windows HTTP 서비스 인증서 구성 도구를 사용 하 여 직접 (**winHttpCertCfg.exe**) 인증서를 관리 하도록 지원 되지 않습니다.  
  
## <a name="import-or-remove-the-certificate"></a>가져오기 또는 인증서를 제거 합니다.  
다음 지침을 가져오거나 어플라이언스 인증서를 제거 하는 방법을 보여 줍니다.  
  
### <a name="to-import-the-certificate"></a>인증서를 가져오려면  
  
1.  시작 합니다 **Configuration Manager**합니다.  
자세한 내용은 [구성 관리자 시작 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)합니다.  

2.  왼쪽된 창에는 **Configuration Manager**, 확장 **병렬 데이터 웨어하우스 토폴로지**, 클릭 하 고 **인증서**합니다.  
  
3.  선택 **인증서를 가져오고 사용 하 여 어플라이언스 구성**를 클릭 하 고 **찾아보기** 이동 하 고 인증서 파일을 선택 합니다.  
  
4.  인증서에 대 한 암호를 입력 합니다 **암호** 필드입니다.  
  
5.  클릭 **적용** 어플라이언스에 대 한 인증서를 구성 합니다.  
  
SQL Server PDW 가져온된 인증서를 사용 하 여 현재 연결을 암호화 하지 않습니다 하지만 새 연결에 대 한 인증서를 사용 합니다.  
  
### <a name="to-remove-the-previously-imported-certificate"></a>이전에 가져온된 인증서를 제거 하려면  
  
1.  시작 합니다 **Configuration Manager**합니다. 

<!-- MISSING LINKS
For more information, see [Launch the Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager-analytics-platform-system.md).  
-->
  
2.  왼쪽된 창에는 **Configuration Manager**, 확장 **병렬 데이터 웨어하우스 토폴로지**, 클릭 하 고 **인증서**합니다.  
  
3.  선택 **기기에 프로 비전 된 모든 인증서를 제거**합니다.  
  
4.  클릭 **적용** 기기에서 이전에 가져온된 인증서를 제거 합니다.  
  
SQL Server PDW 현재 연결을 암호화는 계속 되지만 새 연결에 대 한 인증서를 제거를 사용 하지 않습니다.  
  
![DWConfig 어플라이언스 PDW 인증서](media/dwconfig-appl-pdw-cert.png "DWConfig 어플라이언스 PDW 인증서")  
  
## <a name="see-also"></a>관련 항목  
[Configuration Manager 시작 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
