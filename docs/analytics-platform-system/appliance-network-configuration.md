---
title: 어플라이언스 네트워크 구성
description: APS (분석 플랫폼 시스템) 어플라이언스는 모든 서버 전체의 픽스 집합 및 IHV의 팩터리 바닥에서 적용 가능한 장치를 사용 하 여 빌드 및 구성 됩니다. 어플라이언스를 배달 하면 특정 고객의 데이터 센터 요구 사항과 일치 하도록 외부 (이더넷) IP 주소를 다시 구성 해야 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: af892cbb43b42953732bda59d371e3e22855413b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401417"
---
# <a name="appliance-network-configuration-for-analytics-platform-system"></a>분석 플랫폼 시스템에 대 한 어플라이언스 네트워크 구성
APS (분석 플랫폼 시스템) 어플라이언스는 모든 서버 전체의 픽스 집합 및 IHV의 팩터리 바닥에서 적용 가능한 장치를 사용 하 여 빌드 및 구성 됩니다. 어플라이언스를 배달 하면 특정 고객의 데이터 센터 요구 사항과 일치 하도록 외부 (이더넷) IP 주소를 다시 구성 해야 합니다.  
  
> [!NOTE]  
> PDW V1은 각 제어 랙 노드에 대 한 외부 연결을 제공 하기 위해 8 개의 IP 외부 (*고객 연결*) 주소를 요구 합니다. PDW 2012 (V2) 네트워크 통신은 IP 주소를 통해 외부 기기의 모든 구성 요소를 노출 하 여 향상 되었습니다. 이 접근 방식은 더 강력한 디자인을 제공 하 여 비용을 줄이고 유연성을 높이고 데이터 이동, 데이터 로드 및 Hadoop 통합을 향상 시킵니다. 필요한 IP 주소 수는 어플라이언스의 노드 수에 따라 달라 집니다. 이 큰 IP 주소 블록을 수용 하기 위해 고객은 PDW에 대해 별도의 서브넷을 설정 해야 합니다. 이 서브넷 내에서 최대 5 개의 PDW 랙에 구성 요소를 수용할 수 있는 충분 한 IP 주소 공간 (최대 250 주소)이 있습니다.  
  
**네트워크 구성** 페이지에서 분석 플랫폼 시스템 어플라이언스의 노드에 대 한 외부 연결 네트워크 설정을 볼 수 있습니다. 이 페이지는 읽기 전용입니다.  
  
![DWConfig 어플라이언스 네트워크](./media/appliance-network-configuration/SQL_Server_PDW_DWConfig_ApplTopNetwork.png "SQL_Server_PDW_DWConfig_ApplTopNetwork")  
  
## <a name="to-update-the-network-configuration-on-your-appliance"></a>어플라이언스의 네트워크 구성을 업데이트 하려면  
**Aplianceinfo .xml** 파일을 편집한 다음 설치 프로그램을 실행 하 여 패브릭 도메인 및 워크 로드 도메인의 IP 주소를 변경 합니다. 이 작업은 오프라인 작업입니다. IP 주소를 변경 하는 동안 PDW 지역이 자동으로 중지 됩니다.  
  
> [!NOTE]  
> 도메인 이름은 설치 중에 제공 되며 문자에서 시작 하 여 최대 6 개의 영숫자 문자로 지정 됩니다. 자주 명명 시스템은 F로 시작 하는 패브릭 도메인 및 P로 시작 하는 PDW 워크 로드 도메인을 만듭니다. 이 형식은 도움말 파일 항목 전체에서 가정 되지만 반드시 필요한 것은 아닙니다. <!-- MISSING LINKS For more information about the domain structure, see [PDW Domain Security &#40;SQL Server PDW&#41;](../sqlpdw/pdw-domain-security-sql-server-pdw.md) and [Understanding the Security Model of the HDInsight Region &#40;Analytics Platform System&#41;](../hdinsight/understanding-the-security-model-of-the-hdinsight-region.md)  -->  
  
#### <a name="to-change-the-ip-addresses-of-the-analytics-platform-system"></a>분석 플랫폼 시스템의 IP 주소를 변경 하려면  
  
1.  **원격 데스크톱** 응용 프로그램을 사용 하 여 작업 도메인 관리자 계정으로 **HST01** 에 연결 합니다.  
  
2.  HST01 노드의 **c:\pdwinst\media\AplianceInfo.xml**에서 어플라이언스 정보 파일을 엽니다.  
  
    > [!NOTE]  
    > 파일이 없으면 새 파일을 만들어야 할 수 있습니다.  
  
3.  필요에 따라 이더넷 IP 값을 업데이트 하 고 파일을 저장 합니다.  
  
4.  명령 프롬프트 창에서 다음 설치 명령을 실행 하 여 P/F/H 도메인 이름 및 관리자 암호를 사용 하 여 PDW 지역에 대 한 IP 주소를 업데이트 합니다.  
  
    ```  
    c:\pdwinst\media\setup.exe /action="ConfigureEthernet" /DomainAdminPassword="<password>" /ApplianceInfoFile="C:\PDWINST\media\ApplianceInfo.xml"  
    ```  
  
## <a name="manufacturer-references"></a>제조업체 참조  
Dell 어플라이언스에 대 한 자세한 내용은 다음을 참조 하세요.  
  
-   PowerConnect 스위치 지침 [Dell powerconnect 6200 시리즈 시스템 CLI 참조 가이드](https://downloads.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_powerconnect/powerconnect-6224f_Reference%20Guide_en-us.pdf)  
  
-   iDRAC/BMC [통합 Dell 원격 액세스 컨트롤러 7 (iDRAC7) 버전 1.30.30 사용자 가이드](https://downloads.dell.com/Manuals/all-products/esuprt_electronics/esuprt_software/esuprt_remote_ent_sys_mgmt/integrated-dell-remote-access-cntrllr-7-v1.30.30_User%27s%20Guide_en-us.pdf?c=us&l=en&cs=555&s=biz)  
  
-   PDU의 **Dell 요금제 랙 PDU**`ftp://ftp.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_rack_infrastructure/dell-metered-pdu-led_User's%20Guide_en-us.pdf`  
  
## <a name="see-also"></a>참고 항목  
[Configuration Manager &#40;Analytics Platform System을 시작&#41;](launch-the-configuration-manager.md)  
  
