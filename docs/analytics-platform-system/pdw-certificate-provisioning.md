---
title: PDW 인증서 프로비전
description: 분석 플랫폼 시스템의 PDW 인증서 프로 비전 페이지는 PDW 지역에서 사용 하는 인증서를 가져오거나 제거 Configuration Manager 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 676335fb8ee4aac5906c61084c28cd94cf8ea815
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400889"
---
# <a name="pdw-certificate-provisioning---analytics-platform-system"></a>PDW 인증서 프로 비전-분석 플랫폼 시스템
분석 플랫폼 시스템의 **Pdw 인증서 프로 비전** 페이지는 pdw 지역에서 사용 하는 인증서를 가져오거나 제거 **Configuration Manager** 합니다. 를 사용 하 여 연결을 암호화 하는 인증서는 SQL Server 클라이언트, SQL Server PDW 드라이버, [관리 콘솔](monitor-the-appliance-by-using-the-admin-console.md)및 Integration Services 로드를 사용 하는 도구를 통해 제어 노드에 대 한 통신을 보호 하는 데 도움이 될 수 있습니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
인증서를 설치 하기 전에 다음을 수행 합니다.  
  
1.  보안 인증서를 가져옵니다. 보안 인증서를 가져오는 방법에 대 한 자세한 정보가 필요한 경우 Microsoft 지원에 문의 하세요.  
  
2.  인증서를 암호로 보호 된 PFX 파일의 Control 노드에 저장 합니다.  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>보안상의 이유로 신뢰할 수 있는 인증서를 가져옵니다.  
SQL Server PDW는 인증서를 사용 하 여 제어 노드에 대 한 연결을 암호화 하는 것을 지원 합니다. **관리 콘솔**에 대 한 연결을 포함 합니다.  
  
기본적으로 **관리 콘솔** 에는 개인 정보를 제공 하지만 서버 인증은 제공 하지 않는 자체 서명 된 인증서가 포함 되어 있습니다. 이 경우 통신이 메시지 가로채기 (man-in-the-middle) 공격에 취약 해질 수 있습니다. 사용자가 자체 서명 된 인증서를 사용 하 여 관리 콘솔에 연결 하는 경우 Internet Explorer는 "이 웹 사이트의 보안 인증서에 문제가 있습니다." 라는 오류를 반환 합니다.  
  
자체 서명 된 인증서를 통한 연결은 클라이언트와 서버 간에 진행 중인 데이터를 암호화 하지만 공격자의 연결은 여전히 위험 합니다.  
  
> [!WARNING]  
> 어플라이언스 관리자는 보안 연결을 설정 하 고 Internet Explorer에서 보고 하는 오류를 제거 하기 위해 클라이언트에서 인식 하는 신뢰할 수 있는 인증 기관에 연결 된 인증서를 즉시 획득 해야 합니다.  
  
인증 경로에는 **관리 콘솔**에 액세스 하기 위해 사용자가 브라우저 주소 표시줄에 입력 하는 이름 또는 제어 노드 클러스터 IP 주소 (권장)에 매핑되는 정규화 된 도메인 이름이 포함 되어야 합니다.  
  
분석 플랫폼 시스템**Configuration Manager** 를 사용 하 여 신뢰할 수 있는 인증서를 추가 하거나 제거 합니다. Microsoft Windows HTTP 서비스 인증서 구성 도구 (**winHttpCertCfg**)를 사용 하 여 인증서를 관리 하는 것은 지원 되지 않습니다.  
  
## <a name="import-or-remove-the-certificate"></a>인증서 가져오기 또는 제거  
다음 지침에서는 어플라이언스 인증서를 가져오거나 제거 하는 방법을 보여 줍니다.

> [!WARNING]
> 만료 된 인증서를 갱신 하려면 새 인증서를 가져오기 전에 기존 인증서를 제거 해야 합니다.
  
### <a name="to-import-the-certificate"></a>인증서를 가져오려면  
  
1.  **Configuration Manager**를 시작 합니다. 자세한 내용은 [Configuration Manager &#40;Analytics Platform System&#41;시작 ](launch-the-configuration-manager.md)을 참조 하세요.  
  
2.  **Configuration Manager**왼쪽 창에서 **병렬 데이터 웨어하우스 토폴로지**를 확장 한 다음 **인증서**를 클릭 합니다.  
  
3.  인증서 가져오기를 선택 하 **고 어플라이언스를 사용 하도록 구성한**다음 **찾아보기** 를 클릭 하 여 인증서 파일을 찾아 선택 합니다.  
  
4.  **암호** 필드에 인증서에 대 한 암호를 입력 합니다.  
  
5.  **적용** 을 클릭 하 여 어플라이언스에 대 한 인증서를 구성 합니다.  
  
SQL Server PDW은 가져온 인증서를 사용 하 여 현재 연결을 암호화 하지 않지만 새 연결에는 인증서를 사용 합니다.  
  
### <a name="to-remove-the-previously-imported-certificate"></a>이전에 가져온 인증서를 제거 하려면  
  
1.  **Configuration Manager**를 시작 합니다. 자세한 내용은 [Configuration Manager &#40;Analytics Platform System&#41;시작 ](launch-the-configuration-manager.md)을 참조 하세요.  
  
2.  **Configuration Manager**왼쪽 창에서 **병렬 데이터 웨어하우스 토폴로지**를 확장 한 다음 **인증서**를 클릭 합니다.  
  
3.  **어플라이언스에서 프로 비전 된 모든 인증서 제거**를 선택 합니다.  
  
4.  **적용** 을 클릭 하 여 이전에 가져온 인증서를 어플라이언스에서 제거 합니다.  
  
SQL Server PDW은 현재 연결을 계속 암호화 하지만 제거 된 인증서를 새 연결에 사용 하지 않습니다.  
  
![DWConfig 어플라이언스 PDW 인증서](./media/pdw-certificate-provisioning/SQL_Server_PDW_DWConfig_ApplPDWCert.png "SQL_Server_PDW_DWConfig_ApplPDWCert")  
  
## <a name="see-also"></a>참고 항목  
[Configuration Manager &#40;Analytics Platform System을 시작&#41;](launch-the-configuration-manager.md)  
<!-- MISSING LINKS [HDInsight Certificate Provisioning &#40;Analytics Platform System&#41;](hdinsight-certificate-provisioning.md)  -->  
  
