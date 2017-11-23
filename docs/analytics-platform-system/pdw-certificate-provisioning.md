---
title: "PDW 인증서 (분석 플랫폼 시스템) 프로비저닝"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a423b7d-c6ea-45c1-80b0-26758170594c
caps.latest.revision: "22"
ms.openlocfilehash: f0134ec239b938ee7ace6fc6dc05e130fb844b2f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="pdw-certificate-provisioning"></a>PDW 인증서 프로 비전
**PDW 인증서 프로 비전이** 분석 플랫폼 시스템의 페이지**Configuration Manager** 가져오거나 PDW 영역에 사용 된 인증서를 제거 합니다. 를 사용 하 여 연결을 암호화할 인증서를 도와 보안 통신 하는 제어 노드에 SQL Server 클라이언트에는 SQL Server PDW 드라이버를 사용 하는 도구를 통해는 [관리 콘솔](monitor-the-appliance-by-using-the-admin-console.md), Integration Services를 로드 합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
인증서를 설치 하기 전에 다음을 수행 합니다.  
  
1.  보안 인증서를 가져옵니다. 보안 인증서를 얻는 방법에 대 한 자세한 내용은 Microsoft 지원에 문의 합니다.  
  
2.  하는 제어 노드에 암호로 보호 된 PFX 파일에 인증서를 저장 합니다.  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>보안상의 이유로 신뢰할 수 있는 인증서를 가져오려면  
SQL Server PDW는 제어 노드에;에 대 한 연결을 암호화 하는 인증서를 사용 하 여 지원 에 대 한 연결을 포함 하는 **관리 콘솔**합니다.  
  
기본적으로는 **관리 콘솔** 개인 정보 보호 하지만 하지 서버 인증을 제공 하는 자체 서명 된 인증서를 포함 합니다. 이 있다면 통신 중간자 개입 공격에 취약 합니다. 사용자가 자체 서명 된 인증서를 사용 하 여 연결 하는 관리 콘솔 Internet Explorer는 오류 반환: "이 웹이 사이트의 보안 인증서에 문제가 있습니다."입니다.  
  
클라이언트와 서버 간에 진행 중인 데이터를 암호화 하는 자체 서명 된 인증서를 사용 하 여 연결 하지만 연결이 공격자 로부터 위험에 여전히 있습니다.  
  
> [!WARNING]  
> 기기 관리자 인증서 보안 연결 하 고 보고 하는 Internet Explorer는 오류를 제거 하기 위해 클라이언트에서 인식 하는 신뢰할 수 있는 인증 기관에 연결 된 획득 즉시 해야 합니다.  
  
인증 경로는 제어 노드에 (권장) 클러스터 IP 주소에 매핑되는 정규화 된 도메인 이름 또는 사용자가 액세스할 수 자신의 브라우저 주소 표시줄에 입력 된 이름을 포함 해야 합니다는 **관리 콘솔**합니다.  
  
분석 플랫폼 시스템을 사용 하 여**Configuration Manager** 를 추가 하 여 신뢰할 수 있는 인증서를 제거 합니다. Microsoft Windows HTTP 서비스 인증서 구성 도구를 사용 하 여 직접 (**winHttpCertCfg.exe**) 인증서를 관리 하는 지원 되지 않습니다.  
  
## <a name="import-or-remove-the-certificate"></a>가져오기 또는 인증서 제거  
다음 지침에는 가져오거나 어플라이언스 인증서를 제거 하는 방법을 보여 줍니다.  
  
### <a name="to-import-the-certificate"></a>인증서를 가져오려면  
  
1.  시작 된 **Configuration Manager**합니다. 자세한 내용은 참조 [구성 관리자 &#40; 시작 분석 플랫폼 시스템 &#41; ](launch-the-configuration-manager.md).  
  
2.  왼쪽된 창에는 **Configuration Manager**, 확장 **병렬 데이터 웨어하우스 토폴로지**, 클릭 하 고 **인증서**합니다.  
  
3.  선택 **인증서 가져오기 및 사용 하는 어플라이언스 구성**, 클릭 하 고 **찾아보기** 를 찾아 인증서 파일을 선택 합니다.  
  
4.  인증서에 대 한 암호를 입력의 **암호** 필드입니다.  
  
5.  클릭 **적용** 어플라이언스에 대 한 인증서를 구성 합니다.  
  
SQL Server PDW 가져온된 인증서를 사용 하 여 현재 연결을 암호화 하지 않습니다 되지만 새 연결에 대 한 인증서를 사용 합니다.  
  
### <a name="to-remove-the-previously-imported-certificate"></a>이전에 가져온된 인증서를 제거 하려면  
  
1.  시작 된 **Configuration Manager**합니다. 자세한 내용은 참조 [구성 관리자 &#40; 시작 분석 플랫폼 시스템 &#41; ](launch-the-configuration-manager.md).  
  
2.  왼쪽된 창에는 **Configuration Manager**, 확장 **병렬 데이터 웨어하우스 토폴로지**, 클릭 하 고 **인증서**합니다.  
  
3.  선택 **기기에서 사용자를 프로 비전 인증서를 제거**합니다.  
  
4.  클릭 **적용** 기기에서 이전에 가져온된 인증서를 제거 합니다.  
  
SQL Server PDW는 현재 연결을 암호화 하려면 계속 하지만 새 연결에 대 한 인증서를 제거를 사용 하지 않습니다.  
  
![DWConfig 어플라이언스 PDW 인증서](./media/pdw-certificate-provisioning/SQL_Server_PDW_DWConfig_ApplPDWCert.png "SQL_Server_PDW_DWConfig_ApplPDWCert")  
  
## <a name="see-also"></a>관련 항목:  
[구성 관리자 &#40; 시작 분석 플랫폼 시스템 &#41;](launch-the-configuration-manager.md)  
<!-- MISSING LINKS [HDInsight Certificate Provisioning &#40;Analytics Platform System&#41;](hdinsight-certificate-provisioning.md)  -->  
  
